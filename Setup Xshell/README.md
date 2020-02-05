# SSH를 이용해 AWS에 접속하는 방법

### 1. 먼저 xshell을 다운로드 한다.
- https://www.netsarang.com/ko/free-for-home-school/

netsarang 접속           |  하단의 비상업용 버전 정보 입력 후 다운로드
:-------------------------:|:-------------------------:
![alt-text-10](https://github.com/tenjumh/GraduateSchool/blob/master/BigData_Platform/images/setup%20Xshell/1.%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C.PNG)  |  ![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/2.%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C2.PNG)
"사이트 접속"|"개인정보 입력 후 다운로드"

### 2. 메일을 통한 Xshell 다운로드
등록한 메일 확인            |  메일 링크를 통한 다운로드
:-------------------------:|:-------------------------:
![3](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/3.%EB%A9%94%EC%9D%BC%ED%99%95%EC%9D%B8.PNG) |![4](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/4.%EB%A7%81%ED%81%AC%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C.PNG)
"등록한 메일로 설치링크가 도착"|"메일 내용 중 다운로드 링크를 통해 다운로드"

### 3. 다운로드 후 설치
다운로드 받은 설치파일 실행            |  바탕화면에 바로가기 아이콘 표시
:-------------------------:|:-------------------------:
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/5.%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C.PNG)  |  ![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/5_1.%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C%20%EC%84%A4%EC%B9%98.PNG)
"다운로드된 exe파일을 실행한다."|"바탕화면에 "Xshell6" 바로가기" 선택

### 4. AWS 인스턴스에서 IPv4 퍼블릭 IP 확인
AWS에 인스턴스에서 퍼블릭 IP를 복사            |
:-------------------------:|
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/5_2.%ED%8D%BC%ED%94%8C%EB%A6%ADIP%ED%99%95%EC%9D%B8.PNG) 
"Xshell 설정에 필요한 퍼블릭 IP를 복사한다."|

### 5. Xshell 실행 및 설정
Xshell을 실행하고 "새로만들기"            |  "범주" - "연결"에서 "이름"과 "호스트"입력
:-------------------------:|:-------------------------:
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/6.xshall%EC%8B%A4%ED%96%89.PNG)  |  ![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/7.%EC%9D%B4%EB%A6%84%EC%84%A4%EC%A0%95.PNG)
"세션에 "새로만들기"를 선택|"새 세션 등록 정보"-"연결"-"일반"에 이름(본인 설정)과 호스트(복사한 퍼블릭 IP)를 입력한다.

### 6. Xshell 사용자 인증 설정 (1)
"사용자 인증"을 선택            |
:-------------------------:|
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/9.xshell%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%9D%B8%EC%A6%9D.PNG)
좌측 범주에서 "사용자 인증"에서 "방법", "사용자이름", "사용자키" 설정|


### 7. Xshell 사용자 인증 설정 (2)
Public Key 선택            |  "사용자 키" 생성 및 가져오기
:-------------------------:|:-------------------------:
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/9_1.xshell%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%9D%B8%EC%A6%9D_1.PNG)  |  ![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/9_2.xshell%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%9D%B8%EC%A6%9D_2.PNG)
"방법"에서 Public Key를 선택하면 "사용자 키"항목이 생성| "사용자 키" 찾아보기를 선택

### 8. Xshell 사용자 인증 설정 (3)
"사용자 키" 가져오기          |  "사용자이름" 설정
:-------------------------:|:-------------------------:
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/9_3.xshell%20%EC%82%AC%EC%9A%A9%EC%9E%90%EC%9D%B8%EC%A6%9D_3.PNG)  |  ![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/9_4.%EC%9D%B4%EB%A6%84%EC%84%A4%EC%A0%95.PNG)
"가져오기"를 선택하여 AWS 인스턴스 생성이 만든 키를 선택하고 "확인"합니다. | "사용자이름" 을 기입(원하는대로)합니다.

### 9. Xshell 살정 완료
설정 완료 및 연결            |
:-------------------------:|
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/10.%EC%84%A4%EC%A0%95%EC%9D%B4%20%EB%81%9D%EB%82%AC%EC%9C%BC%EB%A9%B4%20%EC%97%B0%EA%B2%B0.PNG)
사용자 인증 설정이 완료되면 하단의 "연결"을 선택합니다.|

### 10. Xshell 연결 및 접속
연결 및 호스트키 수락          |  접속 확인
:-------------------------:|:-------------------------:
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/11.%EC%97%B0%EA%B2%B0%ED%9B%84%20%ED%98%B8%EC%8A%A4%ED%8A%B8%ED%82%A4%20%EC%88%98%EB%9D%BD.PNG)  |  ![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup%20Xshell/12.Xshell%EC%A0%91%EC%86%8D%EC%99%84%EB%A3%8C.PNG)
연결을 시도하면 "호스트키" 수락이 나오고 "수락 및 저장"을 선택 | 그림같이 접속 이력이 나오면 "성공"

## 축하드립니다. Xshell을 통하여 AWS인스턴스에 접속했습니다.!!!