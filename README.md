# MySQL

SQL을 사용하는 Database의 대표주자 MySQL을 배워보고 작성하는 일기장입니다.

## SQL vs MySQL

SQL은 Structured Query Language 즉 데이터베이스와 대화할때 사용하는 언어임.
MySQL은 DBMS 즉 데이터베이스 관리 시스템이다.

## MySQL 설치

설치는 아래 링크에서 OS에 맞게 설치해주면 된다.  
https://dev.mysql.com/downloads/mysql/

## MySQL 경로 설정

최초 설치 후 MySQL의 경로를 아래와 같이 `.zshrc` 또는 `.bash_profile` 사용하는 터미널에 맞춰 경로를 설정해준다.

```shell
export PATH=${PATH}:/usr/local/mysql/bin
export PATH=${PATH}:/usr/local/mysql/support-files/
```

## MySQL 실행

MySQL을 설치 후 처음 사용하려하면 아래와 같은 에러가 발생하게 된다.  
`ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)`

위 에러는 주로 실행중인 MySQL server가 없을때 나타는 에러라 아래 명령어로 MySQL을 실행해주면된다.  
`sudo mysql.server start`

이후 아래 명령어를 통해 MySQL server에 접속한다.  
`mysql -u root -p`

그러면 설치 간 설정해둔 root의 비밀번호를 입력하라는 프롬프트가 나타나고 입력하면 접속이 된다.

## 편리한 도구인 MySQL Workbench

MySQL Workbench는 MySQL을 편리하게 사용하기 위한 그래픽 인터페이스라고 보면된다.

설치는 아래 링크에서 가능하다.  
https://dev.mysql.com/downloads/workbench/

## 따옴표

SQL에서는 큰따옴표를 사용하지않고 작은 따옴표를 사용한다.  
MySQL에서는 큰따옴표도 작동은 하지만 SQL을 이용하는 다른 DBMS에서는 작동 안할수 있으니 작은 따옴표를 쓸 수 있도록 습관을 들여야함

## 데이터베이스 표시하기

```SQL
SHOW DATABASES;
```

## 데이터베이스 생성하기

```SQL
CREATE DATABASE <name>;
```

## 데이터베이스 삭제하기

```SQL
DROP DATABASE <name>;
```

## 데이터베이스 이용하기

```SQL
-- 사용할 데이터베이스 선택
USE <database name>;
-- 선택된 데이터베이스 출력
SELECT database();
```

## 테이블

데이터의 형식과 형태를 작성하고, 그 형태를 따르는 데이터 컬렉션을 뜻함.  
즉 데이터베이스 안에서 구조화된 형식으로 관련된 데이터를 담고있는 것을 테이블이라고함.

## 데이터 타입

수많은 데이터 타입이 존재하기 때문에 이를 전부 파악하고 있는것도 좋겠지만 Docs에 더 자세히 설명이 나와있으니 아래 링크를 참조.  
https://dev.mysql.com/doc/refman/8.3/en/data-types.html

## 테이블 생성하기

```SQL
CREATE TABLE <table_name>
(
  <column_name> <data_type>,
  <column_name> <data_type>
);
--example
CREATE TABLE cats
(
  name VARCHAR(100),
  age INT
);
```

## 테이블 검사

```SQL
-- table의 현재 리스트를 가져옴
SHOW TABLES;
-- table_name column의 정보를 가져옴
SHOW COLUMNS FROM <table_name>;
DESCRIBE <table_name>;
DESC <table_name>;
```

## 테이블 삭제

```SQL
DROP TABLE <table_name>;
```

## 데이터 삽입

```SQL
INSERT INTO <table_name>(<column_name>)
VALUES (value);
--example
INSERT INTO cats(name, age)
VALUES ('나비', 1);
```

## 데이터 조회

```SQL
SELECT * FROM <table_name>;
--example
SELECT * FROM cats;
```

## 데이터 다중 삽입

```SQL
INSERT INTO <table_name>(<column_name>)
VALUES
  (value),
  (value),
  (value);
--example
INSERT INTO cats (name, age)
VALUES
  ('Meatball', 5),
  ('Turkey', 1),
  ('Potato Face', 15);
```

## NULL, NOT_NULL

기본값은 NULL로 설정되나 Table 생성 시 NOT NULL을 선언해줄수 있다.

```SQL
CREATE TABLE <table_name>
(
  <column_name> <data_type> NOT NULL,
  <column_name> <data_type> NOT NULL
);
--example
CREATE TABLE cats2
(
  name VARCHAR(100) NOT NULL,
  age INT NOT NULL
);
```

## DEFAULT Values

```SQL
CREATE TABLE <table_name>
(
  <column_name> <data_type> DEFAULT <value>,
  <column_name> <data_type> DEFAULT <value>
);
--example
CREATE TABLE cats3
(
  name VARCHAR(100) DEFAULT 'mystery',
  age INT DEFAULT 99
);
```

## Key

흔히 말하는 고유 식별자임(Primary Key, PK)

```SQL
CREATE TABLE <table_name>
(
  <column_name> <data_type> PRIMARY KEY,
  <column_name> <data_type> DEFAULT <value>,
  <column_name> <data_type> DEFAULT <value>
);
--example
CREATE TABLE unique_cats (
	cat_id INT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  age INT NOT NULL
);
--example2
CREATE TABLE unique_cats2 (
	cat_id INT,
  name VARCHAR(100) NOT NULL,
  age INT NOT NULL,
  PRIMARY KEY (cat_id)
);
```

## AUTO_INCREMENT

```SQL
CREATE TABLE unique_cats3 (
	cat_id INT AUTO_INCREMENT,
  name VARCHAR(100),
  age INT,
  PRIMARY KEY (cat_id)
);
```
