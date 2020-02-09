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
tar - xzvf hadoop-3.1.3.tar.gz
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
아래에 그림 같이            |
:-------------------------:|
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/hadoop_spark%20install/5.nano%20.bashrc.PNG) 
```
"export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre" 
"export HADOOP_HOME=/usr/local/hadoop"
"export PATH=$PATH:$HADOOP_HOME/bin"
"export PATH=$PATH:$HADOOP_HOME/sbin"
```
추가 |

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

### 8. 인스턴스 구성하기
인스턴스 OS 설정            |  인스턴스 유형 선택
:-------------------------:|:-------------------------:
![8-1](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/11.machine%20image%20selection.PNG) | ![8-2](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/12%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%9C%A0%ED%98%95.PNG)
"AWS에 적용할 OS를 선택하고 하단 "다음""|"프리티어 사용가능(기본설정) 선택하고 하단 "다음""

스토리지 추가            |  보안 그룹 구성
:-------------------------:|:-------------------------:
![8-3](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/13.%EC%8A%A4%ED%86%A0%EB%A6%AC%EC%A7%80.PNG) | ![8-4](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/14.%EB%B3%B4%EC%95%88%EA%B7%B8%EB%A3%B9%EC%84%A4%EC%A0%95.PNG)
"스토리지 크기를 지정하고 하단 "다음""|"자신의 보안 그룹 이름을 생성하고 하단 "다음""

### 9. 인스턴스 시작 검토
인스턴스 구성 검토            |  인택
:-------------------------:|:-------------------------:
![9-1](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/15.%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%20%EC%8B%9C%EC%9E%91%20%EA%B2%80%ED%86%A0.PNG) | ![9-2](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/16.%EC%83%88%ED%82%A4%ED%8E%98%EC%96%B4%EC%83%9D%EC%84%B1.PNG)
"세부 정보를 확인하고 하단의 "시작""|"인증은 키페어로 진행되며 기존 키페어가 없으면 새키페어생성으로 다운로드"

키페어 선택             |  인스턴스 생성 완료
:-------------------------:|:-------------------------:
![9-3](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/17.%ED%82%A4%ED%8E%98%EC%96%B4%EC%84%A0%ED%83%9D%20%EC%A0%91%EC%86%8D.PNG) | ![9-4](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/19.%ED%8D%BC%ED%94%8C%EB%A6%ADIP%ED%99%95%EC%9D%B8.PNG)
"기존 키 페어 선택으로 생성된 키페어를 선택하고 "인스턴스 시작""|"인스턴스 생성이 완료 확인"

### 10. 인스턴스 완료
- 인스턴스 상태가 Runing이라면 완료가 된 것이며, 해당 인스턴스의 **IPv4 퍼블릭 IP**를 체크
- 다음은 Xshell을 통해서 AWS에 접속하고
- Hadoop을 설치하여 운영해본다. 