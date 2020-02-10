# AWS환경에 hadoop Spark 설치하기

- AWS에 인스턴스를 만든다.
https://github.com/tenjumh/Big_data_Platform/tree/master/Create%20AWS%20Instance
- Xshell을 이용하여 AWS 환경에 접속한다.
https://github.com/tenjumh/Big_data_Platform/tree/master/Setup%20Xshell

### 1. SSH(Xshell)로 AWS에 접속한다.
SSH를 통합 AWS 접속            |
:-------------------------:|
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/hadoop_spark%20install/0.PNG) 
"SSH를 통합 AWS 접속"|

### 2. jdk를 다운로드 한다.
하기와 같이 실행            |  하기와 같이 실행  
:-------------------------:|:-------------------------:
![3](https://github.com/tenjumh/Big_data_Platform/blob/master/images/hadoop_spark%20install/1.PNG) |![4](https://github.com/tenjumh/Big_data_Platform/blob/master/images/hadoop_spark%20install/2.PNG) 
"sudo add-apt-repository ppa:webupd8team/java" 입력|"sudo apt install openjdk-8-sudo apt install openjdk-8-jdk-headless"입력

### 3. hadoop 최신 버전을 다운로드 한다.
최신 버전 다운로드            |
:-------------------------:|
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/hadoop_spark%20install/3.PNG) 
"wget http://apache.claz.org/hadoop/common/hadoop-3.1.3/hadoop-3.1.3.tar.gz" 입력|

### 4. hadoop 압축 풀기 및 디렉터리 이동
- 압축 풀기 
```
tar -xzvf hadoop-3.1.3.tar.gz
```
- 파일 이동
```
sudo mv hadoop-3.1.3 /usr/local/hadoop
```

### 5-1. 환경 변수 설정
- 환경 변수 설정 열기
```
sudo nano /etc/environment
```
- nano 편집창이 열림
- 기존 경로 뒤에 JAVA_HOME 경로를 추가
```
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/local/h$
```
```
JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"
```
nano 편집창에서 기존 경로뒤에 경로 추가            |
:-------------------------:|
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/hadoop_spark%20install/4.PNG) 
"JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"" 추가 및 Ctrl-x로 저장(Y) 후 나옴|

### 5-2. 환경 변수 설정
- 환경 변수 설정 열기
```
source /etc/evnironment
nano .bashrc
```
- nano 편집창이 열림
- 아래에 그림 같이
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/hadoop_spark%20install/5.nano%20.bashrc.PNG) 
- PATH 추가
```
"export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre" 
"export HADOOP_HOME=/usr/local/hadoop"
"export PATH=$PATH:$HADOOP_HOME/bin"
"export PATH=$PATH:$HADOOP_HOME/sbin"
```
- 실행
```
source .bashrc

```

### 6. hadoop test
- hadoop test
```
hadoop jar /usr/local/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.1.3.jar wordcount /usr/local/hadoop/LICENSE.txt output
```
- output 폴더 안의 part-r-00000확인
아래에 그림 같이 나오면            |
:-------------------------:|
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/hadoop_spark%20install/6.part-r-00000.PNG) 
나오면 성공 |

### 7. Spark 다운로드 한다.
- 다운로드
``` 
wget http://mirror.apache-kr.org/spark/spark-2.4.5/spark-2.4.5-bin-hadoop2.7.tgz
```
- 만약 "Permission denied"나오면 
```
sudo wget http://mirror.apache-kr.org/spark/spark-2.4.5/spark-2.4.5-bin-hadoop2.7.tgz
```
- 압축 풀기 
```
sudo tar -xzvf spark-2.4.5-bin-hadoop2.7.tgz
```
- 파일 이동
```
sudo mv spark-2.4.5-bin-hadoop2.7 /usr/local/spark
```

### 8. 환경 변수 설정
- 환경 변수 설정 열기
```
sudo vim ~/.bashrc, bashrc
```
- 편집창 열리고 PATH 추가
```
export SPARK_HOME=/usr/local/spark
export PATH=$PATH:$SPARK_HOME/bin
```
- 'Esc'키 누르고 ':'누르고 편집기 하단에서 'wq'로 빠져 나온다.
- 실행
```
source ~/.bashrc

```

### 9. spark-env.sh 수정
- 경로 이동
```
cd /usr/local/spark/conf
```
- cp를 통해 파일 생성
```
cp spark-env.sh.template spark-env.sh
```
- 생성된 파일을 nano편집기를 통해 경로를 추가
```
nano spark-env.sh
```
- 편집기 하단에 하기와 같이 입력
```
export HADOOP_HOME=/usr/local/hadoop
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
```
- "Ctrl-x"를 누르고 "Y"를 선택해 저장 후 나옴

### 10. 단일 노드 Spark Test
```
spark-submit --class org.apache.spark.examples.SparkPi --master local /$SPARK_HOME/examples/jars/spark-examples_2.11-2.4.5.jar 5
```
아래에 그림 같이 여러 줄에 걸쳐서 현 상태가 출력            |
:-------------------------:|
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/hadoop_spark%20install/7.PNG) 
종료되기 전에 계산된 pi값이 나타나면 성공 |