# mysql 접속
1. service mysql start
2. mysql -u root -p
3. 비밀번호 입력

# 데이터베이스 조회
show databases;
# 데이터베이스 선택
use mysql;
# 선택된 데이터베이스에 테이블 조회
show tables;
# 데이터베이스 생성
create database flyai;
# 생성한 데이터베이스 선택
use flyai;
# 선택한 데이터베이스에 테이블 조회
show tables;

# 테이블 생성
create table friend(
num int not null,
name varchar(10),
address varchar(80),
tel varchar(20),
email varchar(20),
primary key(num)
);

# 테이블 구조 보기
desc friend;

# 테이블 삭제
- drop table friend;

# 테이블 생성 (auto_Increment)
- create table friend(
num int not null auto_Increment,
name varchar(10),
address varchar(80),
tel varchar(20),
email varchar(20),
primary key(num)
);
  - `auto_Increment` 값은 테이블에서 PK(Primary Key)로 많이 사용됨
  - 데이터가 입력될 때 자동으로 값이 1개씩 증가되는 칼럼 속성이기 때문에 데이터 중복이 발생하지 않기 때문

# 필드 추가하기
- alter table friend add age int;

# 필드 삭제하기
- alter table friend drop email;
- alter table friend drop age;

# 필드 변경하기
- alter table friend change tel phone int;

# 필드 타입 변경
- alter table friend modify name int;

# 테이블 이름 변경
- alter table friend rename student;
- show tables;

# 테이블 삭제
- drop table student;
- show tables;

# 테이블 생성
- create table mem (
num int not null auto_Increment,
id char(15) not null,
name char(10) not null,
sex char(1),
post_num char(8),
address char(80),
tel char(20),
age int,
primary key(num)
);
