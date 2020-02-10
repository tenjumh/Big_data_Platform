# Anaconda 설치하기
### (1) wget로 다운로드 (최신버전)
```
wget https://repo.continuum.io/archive/Anaconda3-2019.10-Linux-x86_64.sh
```
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup_anaconda/1.PNG)
### (2) bash 명령어로 설치
```
bash Anaconda3-2019.10-Linux-x86_64.sh
```
- 실행후 enter를 입력이 표시되면 enter를 한다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup_anaconda/2.PNG)
- 동의서를 계속 enter로 넘기면 yes/no가 나오고 'yes'를 입력하면 완료된다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup_anaconda/3.PNG)
- 기본 경로로 설치 "Enter"
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup_anaconda/4.PNG)

### (3) nano 편집기로 경로 설정
```
sudo nano ~/.bash_profile
```
```
# Anaconda
export ANACONDA_HOME="/home/ubuntu/anaconda3"
export PATH=${ANACONDA_HOME}/bin:$PATH
```
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup_anaconda/5.PNG)

### (4) 업데이트
```
source ~/.bash_profile
```

# Jupyter 설정하기

### (1) home으로 복귀
```
cd ~
```
### (2) jupyter 설정 파일 생성
```
jupyter notebook --generate-config
```
### (3) password 설정
```
jupyter notebook password
```
### (4) 비밀번호 사용할 때 암호화 하기
```
cd ~
mkdir ~/certs
cd ~/certs
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout mykey.key -out mycert.pem
```
- nano 편집기 열기
```
cd ~
sudo nano ~/.jupyter/jupyter_notebook_config.py
```
- 하기 내용 추가
```
c = get_config()
# Notebook config this is where you saved your pem cert
c.NotebookApp.certfile = u'/home/ubuntu/certs/mycert.pem'
c.NotebookApp.keyfile = u'/home/ubuntu/certs/mykey.key'
 
# Set ip to '*' to bind on all interfaces (ips) for the public server
c.NotebookApp.ip = '*'
# Don't open browser by default
c.NotebookApp.open_browser = False
# Fix port to 10001
c.NotebookApp.port = 10001
```
- "Ctrl+x" 후 "Y" 저장하고 나옴

### (5) jupyter 실행
```
juptyer notebook
```
### (6) 보안그룹 설정
- 외부에서 AWS EC2 인스턴스의 퍼블릭 IP를 이용해 jupyter web에 접근하기 위해서
- Port를 열어둬야 함
- AWS EC2 보안그룹 인바운드 설정
- 모든 TCP 추가 후 저장
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup_anaconda/6.PNG)
### (7) jupyter notebook 웹 접속
```
https://{jupyter를 실행한 인스턴스의 퍼블릭 ip}:10001 접속
```
- 패스워드 입력 화면
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup_anaconda/7.PNG)
- 입력하면 jupyter notebook에 접속이 된다.
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup_anaconda/8.PNG)

# pyspark와 연동

### (1) 경로 설정
- nano 편집기를 연다.
```
sudo nano ~/.bash_profile
```
- 내용을 입력
```
# PySpark
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS='notebook'
```
- "Ctrl+x" 후 "Y" 저장하고 나옴
```
source ~/.bash_profile
```
- pyspark 실행, jupyter notebook 자동 실행
### (2) python 파일 생성 및 sc 입력/ 출력
- 실행 후 python 파일 하나를 생성한다.
- sc입력 후 다음과 같이 출력되면 성공
![alt-text-10](https://github.com/tenjumh/Big_data_Platform/blob/master/images/setup_anaconda/9.PNG)

