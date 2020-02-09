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

### 3. AWS Educate의 Main 화면 접속된다.
AWS Educate의 Main            |
:-------------------------:|
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/4.%EC%95%84%EB%A7%88%EC%A1%B4%20%EC%95%A0%EB%93%80%EB%A9%94%EC%9D%B8.PNG) 
"상단 중간 My Classrooms를 선택"|

### 4. My Classrooms에 접속
확인 팝업            |  My Classrooms 접속
:-------------------------:|:-------------------------:
![3](.PNG) |![4](4.PNG) 
"계속을 선택"|"go to classroom 선택"

### 5. AWS Account status 확인
AWS Account status            |
:-------------------------:|
![5](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/7.aws%20console.PNG) 
"현재 계정 상태, 크레딧, 세션 시간 확인" and "AWS Console" 선택|

### 6. AWS Management console 접속 및 EC 접속
Management console            |  EC2 접속
:-------------------------:|:-------------------------:
![6](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/8.aws%20console2.PNG) |![6](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/8_1.aws%20console3_EC2.PNG) 
"콘솔 접속"|"상단 서비스 - 컴퓨팅 - EC2 선택"

### 7. EC2 대쉬보드
EC2 대쉬보드            |  EC2 인스턴스 시작
:-------------------------:|:-------------------------:
![7](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/9.EC2.PNG) | ![7](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/10.%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%EC%8B%9C%EC%9E%91.PNG)
"대쉬보드에서는 리소스 등 다양한 정보확인"|"Main화면 인스턴스 시작" - "인스턴스 시작 선택"

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