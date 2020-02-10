# Multinode 및 HA 설정하기

- 멀티 노드 등 서버 구성은 하기와 같이 한다.
nn1: QuorumPeerMain(zookeeper), JournalNode, DFSZKFailoverController, NameNode(active), Resourcemanager
nn2: QuorumPeerMain(zookeeper), JournalNode, DFSZKFailoverController, NameNode(standby)
dn1: QuorumPeerMain(zookeeper), JournalNode, DataNode, Nodemanager
dn2: DataNode, Nodemanager
dn3: DataNode, Nodemanager

## 1. zookeeper 설치 및 설정하기
```
sudo wget http://mirror.apache-kr.org/zookeeper/zookeeper-3.4.14/zookeeper-3.4.14.tar.gz
```


### 1). zookeeper 다운로드
- 참고로 대학생에게는 등록된 학교에 대해서 일부 크레딧을 제공해준다.
- 계정이 있다고 생각하고 인스턴스 생성 방법을 기술한다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/1_download.PNG)

### 2). 압축해제 및 샘플 설정 파일 복사
- tar : 압축을 해제한다.
```
sudo tar xvfz zookeeper-3.4.14.tar.gz
```
- mv : 파일을 이동한다.
```
sudo mv zookeeper-3.4.14 /usr/local/zookeeper
```
- cd 경로로 이동한다.
```
cd /usr/local/zookeeper
```
- 설정파일 복사한다.
```
sudo cp conf/zoo_sample.cfg conf/zoo.cfg
```

### 3). zoo.cfg 설정하기
- nano 편집기로 편집한다.
```
sudo nano conf/zoo.cfg
```
- zoo.cfg파일 편집한다. (그림 참조)
```
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/usr/local/zookeeper/data
clientPort=2181
maxClientCnxns=0
maxSessionTimeout=180000
server.1=nn1:2888:3888
server.2=nn2:2888:3888
server.3=dn1:2888:3888
```
- "Ctrl-x"후 "Y" 저장하고 나온다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/2_nano_conf.PNG)

### 4). zoo.cfg에서 설정한 dataDir폴더 생성 및 id 생성하기
- 생성을 위해 경로 이동한다.
```
cd /usr/local/zookeeper
```
- mkdir : data 폴더를 생성한다.
```
sudo mkdir data
```
- nano 편집기로 myid 생성 저장한다.
```
sudo nano /usr/local/zookeeper/data/myid
```
- 1 입력하고 저장한다. (그림 참조)
- "Ctrl-x"후 "Y" 저장하고 나온다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/3.PNG)

## 2. hadoop 환경 설정하기

### 1). hdfs-site.xml 편집
- nano 편집기로 **hdfs-site.xml** 편집 저장한다.
```
sudo nano /usr/local/hadoop/etc/hadoop/hdfs-site.xml
```
- 하기 코드를 입력한다.
```
<configuration>
  <property>
    <name>dfs.namenode.name.dir</name>
    <value>/usr/local/hadoop/data/nameNode</value>
  </property>
  <property>
    <name>dfs.datanode.data.dir</name>
    <value>/usr/local/hadoop/data/dataNode</value>
  </property>
  <property>
    <name>dfs.replication</name>
    <value>2</value>
  </property>
  <!-- configuration zookeeper -->
  <property>
    <name>dfs.journalnode.edits.dir</name>
    <value>/usr/local/hadoop/data/dfs/journalnode</value>
  </property>
  <property>
    <name>dfs.nameservices</name>
    <value>my-hadoop-cluster</value>
  </property>
  <property>
    <name>dfs.ha.namenodes.my-hadoop-cluster</name>
    <value>namenode1,namenode2</value>
  </property>
  <property>     
    <name>dfs.namenode.rpc-address.my-hadoop-cluster.namenode1</name>
    <value>nn1:8020</value>
  </property>
  <property>
    <name>dfs.namenode.rpc-address.my-hadoop-cluster.namenode2</name>
    <value>nn2:8020</value>
  </property>
  <property>
    <name>dfs.namenode.http-address.my-hadoop-cluster.namenode1</name>
    <value>nn1:50070</value>
  </property>
  <property>
    <name>dfs.namenode.http-address.my-hadoop-cluster.namenode2</name>
    <value>nn2:50070</value>
  </property>
  <property>
    <name>dfs.namenode.shared.edits.dir</name>
    <value>qjournal://nn1:8485;nn2:8485;dn1:8485/my-hadoop-cluster</value>
  </property>
  <property>
    <name>dfs.client.failover.proxy.provider.my-hadoop-cluster</name>
    <value>org.apache.hadoop.hdfs.server.namenode.ha.ConfiguredFailoverProxyProvider</value>
  </property>
  <property>
    <name>dfs.ha.fencing.methods</name>
    <value>sshfence</value>
  </property>
  <property>
    <name>dfs.ha.fencing.ssh.private-key-files</name>
    <value>/home/ubuntu/.ssh/id_rsa</value>
    </property>
  <property>
    <name>dfs.ha.automatic-failover.enabled</name>
    <value>true</value>
  </property>
  <property>
    <name>dfs.name.dir</name>
    <value>/usr/local/hadoop/data/name</value>
  </property>
  <property>
    <name>dfs.data.dir</name>
    <value>/usr/local/hadoop/data/data</value>
  </property>
</configuration>	
```	
- "Ctrl-x"후 "Y" 저장하고 나온다.
<br>
- nano 편집기로 **core-site.xml** 편집 저장한다.
```
sudo nano /usr/local/hadoop/etc/hadoop/core-site.xml
```
- 하기 코드를 입력한다.
```
<configuration>
  <property>
    <name>fs.default.name</name>
    <value>hdfs://nn1:9000</value>
  </property>
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://my-hadoop-cluster</value>
  </property>
  <property>
    <name>ha.zookeeper.quorum</name>
    <value>nn1:2181,nn2:2181,dn1:2181</value>
  </property>
</configuration>
```	
- "Ctrl-x"후 "Y" 저장하고 나온다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/4.PNG)
<br>
- nano 편집기로 **yarn-site.xml** 편집 저장한다.
```
sudo nano /usr/local/hadoop/etc/hadoop/yarn-site.xml
```
- 하기 코드를 입력한다.
```
<configuration>
  <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
  </property>
  <property>
    <name>yarn.nodemanager.aux-services.mapreduce_shuffle.class</name>
    <value>org.apache.hadoop.mapred.ShuffleHandler</value>
  </property>
  <property>
    <name>yarn.resourcemanager.hostname</name>
    <value>nn1</value>
  </property>
  <property>
    <name>yarn.nodemanager.vmem-check-enabled</name>
    <value>false</value>
  </property>
</configuration>
```	
- "Ctrl-x"후 "Y" 저장하고 나온다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/5.PNG)
<br>
- nano 편집기로 **mapred-site.xml** 편집 저장한다.
```
sudo nano /usr/local/hadoop/etc/hadoop/mapred-site.xml
```
- 하기 코드를 입력한다.
```
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
    <property>
        <name>yarn.app.mapreduce.am.env</name>
        <value>HADOOP_MAPRED_HOME=${HADOOP_HOME}</value>
    </property>
    <property>
        <name>mapreduce.map.env</name>
        <value>HADOOP_MAPRED_HOME=${HADOOP_HOME}</value>
    </property>
    <property>
        <name>mapreduce.reduce.env</name>
        <value>HADOOP_MAPRED_HOME=${HADOOP_HOME}</value>
    </property>
</configuration>
```	
- "Ctrl-x"후 "Y" 저장하고 나온다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/6.PNG)
<br>
- nano 편집기로 **workers** 편집 저장한다.
```
sudo nano /usr/local/hadoop/etc/hadoop/workers
```	
- 하기 코드를 입력한다.
```
dn1
dn2
dn3
```	
- "Ctrl-x"후 "Y" 저장하고 나온다.
<br>
- nano 편집기로 **masters** 편집 저장한다.
```
sudo nano /usr/local/hadoop/etc/hadoop/masters
```	
- 하기 코드를 입력한다.
```
nn1
nn2
```	
- "Ctrl-x"후 "Y" 저장하고 나온다.

## 3. ssh 설정
- master node가 worker node로 비밀번호 없이 접근할 수 있는 권한을 주기위해 설정한다.
### 1). 키 생성(추가적으로 입력하지 않고 계속 엔터)
```
ssh-keygen -t rsa
```
- 커서들 입력하지 않고 계속 엔터를 치면 하기와 같이 그림이 나온다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/7.PNG)
### 2). 생성된 키를 'authorized_keys'에 붙이기
```
cat >> ~/.ssh/authorized_keys < ~/.ssh/id_rsa.pub
```
### 3). 테스트 하기
```
ssh localhost
```
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/8.PNG)
- yes를 입력하면 하기와 같이 추가적인 비밀번호 입력없이 바로 접속이 되면 성공
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/9.PNG)

## 4. AMI 생성 및 인스턴스 4개 더 실행

### 1). aws 인스턴스 창에서 이미지 생성 클릭
- 인스턴스 "연결"-"이미지"-"이미지생성"
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/10.PNG)
### 2). 이미지 생성
- 이름설정 후, 이미지 생성 클릭한다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/11.PNG)
### 3). AMI 페이지 클릭
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/12.PNG)
### 4). 생성이 완료되면 시작하기
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/13.PNG)
### 5). 기존 인스턴스 생성과 동일하게 진행
### 6). 단계 2 변경없이 "다음"
### 7). 단계 3 인스턴스 개수 4개로 변경
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/14.PNG)
### 8). 단계 6까지 변경없이 "다음"
### 9). 단계 6 기존 보안 그룹으로 선택
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/15.PNG)
### 10). 기존 키 페어 선택 및 체크박스에 체크박스에
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/16.PNG)
### 11). 완료 후 인스턴스 보기 선택
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/17.PNG)
### 12). 인스턴스의 이름을 설정한다.
- Master와 Worker1~4로 설정파일
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/18.PNG)
### 13). 좌측 네비게이션바에서 "보안그룹"페이지로 이동하고 "hadoop" 보안그룹을 클릭한다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/19.PNG)
### 14). 보안그룹 하단의 인바운트 탭에서 "편집"클릭한다
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/20.PNG)
### 15). "인바운드 규칙 편집"
- "규칙 추가"하고, 유형 - "모든 트래픽", 소스에 "hadoop"을 치면 자동완성된다.
- 자동완성 선택하고 "저장"하고 완료한다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/21.PNG)

## 5. 서버에서 ssh를 위한 hostname 설정하기
### 1). nn1에 연결
### 2). nano로 hosts 편집
```
sudo nano /etc/hosts
```
### 3). 편집기에서 인스턴스의 privat IP 설정파일
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/23.PNG)
### 4). ssh 접속 확인
```
ssh nn2
ssh dn1
ssh dn2
ssh dn3
```
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/24.PNG)
- master로 복귀하려면 "exit"
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/25.PNG)
### 5). hosts 파일 전체 인스턴스에 배포
```
cat /etc/hosts | ssh nn2 "sudo sh -c 'cat >/etc/hosts'"
cat /etc/hosts | ssh dn1 "sudo sh -c 'cat >/etc/hosts'"
cat /etc/hosts | ssh dn2 "sudo sh -c 'cat >/etc/hosts'"
cat /etc/hosts | ssh dn3 "sudo sh -c 'cat >/etc/hosts'"
cat /usr/local/hadoop/etc/hadoop/hdfs-site.xml | ssh nn2 "sudo sh -c 'cat >/usr/l
ocal/hadoop/etc/hadoop/hdfs-site.xml'"
```
### 6). myid 파일 수정
- zoo.cfg에 있는 서버 id값으로 바꿔주는 과정이다.
```
ssh nn2
sudo nano /usr/local/zookeeper/data/myid
```
- nano 편집기에서 "2"로 수정
```
exit
```
```
ssh dn1
sudo nano /usr/local/zookeeper/data/myid
```
- nano 편집기에서 "3"로 수정
```
exit
```

## 6. 실행
### 1). nn1, nn2, dn1에서 zookeeper 실행
```
cd /usr/local/zookeeper
sudo ./bin/zkServer.sh start
```
- 서버 실행상태 확인
```
sudo ./bin/zkServer.sh status
```
- follower 또는 leader라고 표시
### 2). nn1에서 zookeeper 초기화
```
hdfs zkfc -formatZK
```
- 초기화 확인
- zookeeper폴더에서
```
./bin/zkCli.sh
```
- 실행되면
```
ls /hadoop-hadoop
```
- [my-hadoop-cluster]가 출력되면 
```
quit
```
### 3). nn1, nn2, dn1 journalnode실행
```
hdfs --daemon start journalnode
```
### 4). nn1 namenode 초기화
```
hdfs namenode -format
```
### 5). nn1 namenode 실행되면
```
hdfs --daemon start namenode
```
### 6). nn2에서 standby namenode 준비
```
hdfs namenode -bootstrapStandby
```
### 7). start-dfs.sh
```
start-dfs.sh
```
### 8). yarn, JobHistoryServer 실행되면
```
start-yarn.sh
mapred --daemon start historyserver
```
### 9). active, standby 확인
```
hdfs haadmin -getServiceState namenode1
hdfs haadmin -getServiceState namenode2
```
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/26.PNG)
### 10). process 확인
```
ssh nn1
jps
```
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/27.PNG)
```
ssh nn2
jps
```
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/28.PNG)
```
ssh dn1
jps
```
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/29.PNG)
```
ssh dn2
jps
```
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/30.PNG)
```
ssh dn3
jps
```
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/31.PNG)

### 11). wordCount 예제로 동작 확인
```
hadoop fs -mkdir /test
hadoop fs -put /usr/local/hadoop/LICENSE.txt /test/
yarn jar /usr/local/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.1.3.jar wordcount hdfs:///test/LICENSE.txt /test/output
```
```
hadoop fs text /test/output/*–
hadoop fs -text /test/output/*
```
### 12). Spark cluster 모드 예제 실행해 작동 확인
```
spark-submit --class org.apache.spark.examples.SparkPi --master yarn --deploy-mode cluster --driver-memory 512m --executor-memory 512m --executor-cores 1 /$SPARK_HOME/examples/jars/spark-examples_2.11-2.4.5.jar 5
```

## 7. Failover Test
- nn1에서 jps로 namenode id확인
```
jps
```
```
1096 NameNode
1650 DFSZKFailoverController
1456 JournalNode
2505 QuorumPeerMain
1523 JobHistoryServer
2346 ResourceManager
```
```
kill -9 1096
```
- nn2의 namenode가 active 확인
```
hdfs haadmin -getServiceState namenode2
```
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/Setup_multinode_HA/32.PNG)

## 8. 중지
```
stop-dfs.sh 
stop-yarn.sh
```

## 9. 재실행
```
start-dfs.sh 
start-yarn.sh
```

## 10. Node 확인
```
hdsf dfsadmin -report
yarn node -list
```