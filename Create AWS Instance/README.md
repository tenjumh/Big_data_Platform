# Create AWS Instance

- AWS에서 나만의 가상화 환경을 만들기 위해서는 인스턴스를 생성해야한다.
- 인스턴스에는 OS, 사양, 보안 등의 설정과 함께 가상환경을 생성한다.
- AWS Educate 가입 영상(학생편): (https://youtu.be/upUaxMaPxm0)
### 1. 먼저 AWS에 계정을 생성해야 한다.
- 참고로 대학생에게는 등록된 학교에 대해서 일부 크레딧을 제공해준다.
- 계정이 있다고 생각하고 인스턴스 생성 방법을 기술한다.

### 2. AWS에 접속한다.
Google AWS 검색            |  **[AWS Educate]**(https://www.awseducate.com/)
:-------------------------:|:-------------------------:
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/2.%EC%95%84%EB%A7%88%EC%A1%B4%20%EC%95%A0%EB%93%80%EB%A1%9C%EA%B7%B8%EC%9D%B82.PNG)  |  ![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/3.%EC%95%84%EB%A7%88%EC%A1%B4%20%EC%95%A0%EB%93%80%EB%A1%9C%EA%B7%B8%EC%9D%B83.PNG "[AWS Educate]")
"Google AWS 검색"|"아래의 AWS Educate에 로그인" 선택

### 3. AWS Educate의 Main 화면 접속된다.
AWS Educate의 Main            |
:-------------------------:|
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/4.%EC%95%84%EB%A7%88%EC%A1%B4%20%EC%95%A0%EB%93%80%EB%A9%94%EC%9D%B8.PNG) 
"상단 중간 My Classrooms를 선택"|

### 4. My Classrooms에 접속
확인 팝업            |  My Classrooms 접속
:-------------------------:|:-------------------------:
![3](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/5.%EB%A7%88%EC%9D%B4%ED%81%B4%EB%9E%98%EC%8A%A4%20%ED%8C%9D%EC%97%85.PNG) |![4](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/6.%EB%A7%88%EC%9D%B4%ED%81%B4%EB%9E%98%EC%8A%A4.PNG) 
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
키페어 선택            |  인스턴스 생성 완료
:-------------------------:|:-------------------------:
![9-3](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/17.%ED%82%A4%ED%8E%98%EC%96%B4%EC%84%A0%ED%83%9D%20%EC%A0%91%EC%86%8D.PNG) | ![9-4](https://github.com/tenjumh/Big_data_Platform/blob/master/images/create%20aws/18.%EC%83%9D%EC%84%B1%ED%99%95%EC%9D%B8.PNG)
"기존 키 페어 선택으로 생성된 키페어를 선택하고 "인스턴스 시작""|"이제는 인스턴스 생성이 완료, 인스턴스 상태가 running임을 확인하고 **IPv4 퍼블릭 IP**를 체크"