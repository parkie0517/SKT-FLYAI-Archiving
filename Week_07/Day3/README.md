# Day3

# 오전
[https://hub.docker.com/repository/docker/apptools/chatbot-db/general](https://hub.docker.com/repository/docker/apptools/chatbot-db/general) 

![image](https://user-images.githubusercontent.com/51157811/215958198-0584f019-9a2d-482a-a1c2-8e9c022a198a.png)

## ****apptools/chatbot-db****

### 도커 이미지 받아오기

```bash
docker pull apptools/chatbot-db:1.0
```

### 도커 이미지 조회

```bash
docker images
```

### 도커 이미지 실행 - 생성하기

```bash
docker run -d -i -it --name chatbot-db -p 3306:3306 apptools/chatbot-db:1.0
```

### 도커 컨테이너 조회

```bash
docker ps
```

### 도커 컨테이너 안으로 들어가기

```bash
docker exec -e LC_ALL=C.UTF-8 -it chatbot-db /bin/bash
```

### MySQL 접속하기

```bash
mysql -u root -p
```

### MySQL 패스워드 입력

```bash
password : apptools
```

### 데이터베이스 생성

```sql
create database flyai;
```

### 데이터베이스 선택

```sql
use flyai;
```

### 테이블 생성

```sql
create table mem (num int not null auto_Increment,userid varchar(10) not null,userpw varchar(200),name varchar(200) not null,sex varchar(1),post_num varchar(8),address varchar(80),tel varchar(20),age int,img varchar(200),primary key(num));
```

### 테이블 구조보기

```sql
desc mem;
```

### 테이블 데이터 조회하기

```sql
select * from mem;
```

### 챗봇 메시지 저장할 테이블 추가

```sql
create table chatbot(num int not null auto_increment, type varchar(4), msg varchar(200), indate varchar(50), primary key(num));
```

```sql
desc chatbot();
```

### 챗봇 메시지 샘플 저장해보기

```sql
insert into chatbot set type = 'bot', msg = '안녕하세요! 저는 귀염둥이 챗봇 입니다.', indate = now();
```

```sql
select * from chatbot;
```

## apptools/chatbot-webserver

### 도커 이미지 받아오기

```bash
docker pull apptools/chatbot-webserver:1.0
```

### 도커 이미지 조회

```bash
docker images
```

### 도커 이미지 실행 - 생성하기

```bash
docker run -d --privileged -i -it --name chatbot-webserver -p 80:80 -p 22:22 apptools/chatbot-webserver:1.0
```

### 도커 컨테이너 조회

```bash
docker ps
```

### 도커 컨테이너 안으로 들어가기

```bash
docker exec -e LC_ALL=C.UTF-8 -it chatbot-webserver /bin/bash
```

### 내용 수정

```bash
nano chatbot.pyDB 접속 IP를 본인 PC IP로 수정DB 접속 계정 수정
```

### 챗봇 소스 경로로 이동

```bash
cd /root/mental-health-chatbot-master
```

### 챗봇 실행

```bash
streamlit run chatbot.py --server.port 80
```

### 브라우저에서 본인 PC IP 접속

```bash
iqconfig
```

## 챗봇 테이블 생성 (CMD | mysql 접속 후)

```bash
docker exec -e LC_ALL=C.UTF-8 -it mysql-container /bin/bash
```

```bash
docker exec -e LC_ALL=C.UTF-8 -it chatbot-db /bin/bash
```

```bash
mysql -u root -p
```

```bash
password : apptools
```

```sql
use flyai
```

```sql
create table chatbot(
num int not null auto_increment,
type varchar(4),
msg varchar(200),
indate varchar(50),
primary key(num)
);

desc chatbot();
```

- 한국 시간 설정
    
    ```sql
    SET GLOBAL time_zone='Asia/Seoul';
    ```
    
    ```sql
    SET GLOBAL time_zone='Asia/Seoul';
    SET time_zone='Asia/Seoul';
    ```
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c8d4b848-fc45-4a36-8d02-bd502e430c12/Untitled.png)
    

```sql
insert into chatbot set
type = 'bot',
msg = '안녕하세요! 저는 귀염둥이 챗봇 입니다.',
indate = now();
```

```sql
select * from chatbot;
```

### 챗봇 실행

```bash
streamlit run chatbot.py --server.port 80
```

### 브라우저에서 본인 PC IP 접속

```bash
iqconfig
```

## SQL 실습

### 11시 이후에 한 챗봇 대화 데이터 가져오기 (SQL 문)

```sql
select * from chatbot where indate like '2023-02-01 11:%'
```

### 11시 이후에 한 챗봇 대화 데이터에서 유저 데이터만 가져오기 (SQL 문)

```sql
select * from chatbot where indate like '2023-02-01 11:%' and type = 'user';
```

![image](https://user-images.githubusercontent.com/51157811/215958472-497ffc79-b10e-443a-9a95-d707aace79a5.png)

### 과거 채팅 대화 내용 가져오

## 과거 채팅 대화 내용 가져오기 (VS code)

```python
with st.form('form', clear_on_submit=True):
    user_input = st.text_input('당신: ', '')
    submitted = st.form_submit_button('전송')
    
**# 과거 대화내용 저장
cursor = db.cursor()
sql = "select * from chatbot;"
cursor.execute(sql)
rows =cursor.fetchall()

for msg in rows:
    if msg[1] == 'user':
        message(msg[2], is_user = True)
    else:
        message(msg[2])**

if submitted and user_input:
    embedding = model.encode(user_input)
```

✔️  num | type | msg | indate  → type num : 0 | 1 | 2 | 3 

![image](https://user-images.githubusercontent.com/51157811/215958510-36222b17-38c0-4bd6-a27f-0e6f699a30da.png)

## 도커 내부 파일 가져오기

로컬에 폴더를 하나 생성 

C:\WORK\Project\Ai\Chatbot\ 경로로 폴더 생성

```bash
docker cp chatbot-webserver:/root/mental-health-chatbot-master C:\WORK\Project\Ai\Chatbot\
```

chatbot-webserver 컨테이너의 /root/mental-health-chatbot-master 폴더를 로컬의 C:\WORK\Project\Ai\Chatbot\ 에 복사가 된다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f5a82a71-db11-4391-bec8-8781e2e837f5/Untitled.png)

이후 VSCode와 같은 에디터에서 수정 가능

수정된 파일을 다시 도커 컨테이너를 저장해 보자.

pymysql.connect(host='172.23.243.67' 에서 IP를 변경 후 저장 해보자.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/363a841b-7e00-4411-9cd4-4ab4e74c5aae/Untitled.png)

```bash
docker cp C:\WORK\Project\Ai\Chatbot\mental-health-chatbot-master chatbot-webserver:/root/
```

```bash
# 챗봇 웹서버 도커 컨테이너 접속
cd /root/mental-health-chatbot-master/
nano [chatbot.py](http://chatbot.py/)
```

### +) 도커와 window 연결 방법 (volume)

PS C:\Users\042> docker run -d -it -p 80:80 -p 22:22 -v C:\Users\042\Downloads\chatbot\mental-health-chatbot-master:/root/content/chatbot --name chatbot-webserver apptools/chatbot-webserver:1.0 /bin/bash

호스트 경로(공유하고자 하는 로컬 컴퓨터 폴더 경로)
C:\Users\042\Downloads\chatbot\mental-health-chatbot-master 

컨테이너 내부의 공유 폴더

:/root/content/chatbot 

- : 은 구분자

내가 만들 컨테이너 이름

chatbot-webserver apptools/chatbot-webserver:1.0 /bin/bash  

유저네임/레퍼지토리(가져올 image) / 태그(컨테이너를 만들 때 쓰는 명령어)

❗초기 컨테이너 생성시에만 볼륨 명령어 사용가능

볼륨을 사용하면 따로 cp 할 필요 없이 동기화 가능 (매우 유용!) 

만약 이미 컨테이너를 띄운 상태면 적용하기 어려움(방법은 있음. 그러나 초기 컨테이너 생성시 하는 것 추천)
