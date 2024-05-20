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

## 데이터 CRUD Deep Dive

- 데이터 셋팅

  ```SQL
  CREATE TABLE cats (
    cat_id INT AUTO_INCREMENT,
    name VARCHAR(100),
    breed VARCHAR(100),
    age INT,
    PRIMARY KEY (cat_id)
  );

  INSERT INTO cats(name, breed, age)
  VALUES
        ('Ringo', 'Tabby', 4),
        ('Cindy', 'Maine Coon', 10),
        ('Dumbledore', 'Maine Coon', 11),
        ('Egg', 'Persian', 4),
        ('Misty', 'Tabby', 13),
        ('George Michael', 'Ragdoll', 9),
        ('Jackson', 'Sphynx', 7);
  ```

- SELECT 공식

  ```SQL
  -- cats 테이블의 모든 열을 조회
  SELECT * FROM cats;
  -- cats 테이블의 name 열만 조회
  SELECT name FROM cats;
  -- cats 테이블의 name, age 열을 조회
  SELECT name, age FROM cats;
  ```

- WHERE

  ```SQL
  -- cats 테이블의 age가 4인 행을 조회
  SELECT * FROM cats WHERE age=4;
  -- cats 테이블의 name이 'Egg'인 행을 조회
  SELECT * FROM cats WHERE name='Egg';
  -- cats 테이블의 cat_id와 age가 같은 행 중 cat_id, age 열을 조회
  SELECT cat_id, age FROM cats WHERE cat_id=age;
  ```

- Aliases

  ```SQL
  -- cats 테이블의 cat_id를 id로 명명하고 name 열과 같이 조회
  SELECT cat_id AS id, name FROM cats;
  ```

- UPDATE

  ```SQL
  -- cats 테이블의 breed가 Teddy인 행의 breed를 Shorthair로 변경
  UPDATE cats SET breed='Shorthair' WHERE breed='Teddy';
  -- cats 테이블의 name이 Misty인 행의 age를 14로 변경
  UPDATE cats SET age=14 WHERE name='Misty';
  ```

- DELETE

  ```SQL
  -- cats 테이블의 name이 Egg인 행을 삭제
  DELETE FROM cats WHERE name='Egg';
  ```

## String Functions

수많은 String Function이 있는데 필요할때 아래 링크를 참고하여 찾아서 사용하면 될 것 같다.  
https://dev.mysql.com/doc/refman/8.3/en/string-functions.html

- CONCAT, CONCAT_WS

  - CONCAT : Combine Data For Cleaner Output
  - CONCAT_WS : CONCAT With Seperator

  ```SQL
  -- books 테이블의 author_fname,  ' ',  author_lname을 합친 후 author_name으로 명명함
  SELECT CONCAT(author_fname,' ', author_lname) AS author_name FROM books;
  -- books 테이블의 title, author_fname, author_lname을 합치고 seperator로 '-'를 넣어줌
  SELECT CONCAT_WS('-',title, author_fname, author_lname) FROM books;
  ```

- SUBSTRING, SUBSTR

  - SUBSTRING : Work With Parts Of Strings
  - SUBSTR : SUBSTRING의 축약어ㄴ

  ```SQL
  -- 'Hello World'의 1번째 글짜에서 4글자를 선택(Hell)
  SELECT SUBSTRING('Hello World', 1, 4);
  -- 'Hello World'의 7번째 글자에서 끝까지 선택(World)
  SELECT SUBSTRING('Hello World', 7);
  -- 'Hello World'의 끝에서 3글자를 선택(rld)
  SELECT SUBSTRING('Hello World', -3);
  -- books 테이블의 title 컬럼의 1번째 글자에서 10글자를 선택한 후 'short title'로 명명함
  SELECT SUBSTRING(title, 1, 10) AS 'short title' FROM books;
  -- 위 SUBSTRING 명령의 축약어 SUBSTR 사용
  SELECT SUBSTR(title, 1, 10) AS 'short title' FROM books;
  ```

- 문자열 함수 조합(CONCAT, SUBSTRING)

  ```SQL
  -- books 테이블의 title 컬럼 1번째 글자에서 10글자를 선택 후 '...'과 합친 후 'short title'로 명명함
  SELECT CONCAT
    (
      SUBSTRING(title, 1, 10),
      '...'
    ) AS 'short title'
  FROM books;
  ```

- REPLACE

  ```SQL
  -- 'Hello World'에서 'Hell'을 '%$#@'로 변경
  SELECT REPLACE('Hello World', 'Hell', '%$#@');
  -- 'Hello World'에서 'l'을 '7'로 변경
  SELECT REPLACE('Hello World', 'l', '7');
  -- 'Hello World'에서 'o'를 '0'으로 변경
  SELECT REPLACE('Hello World', 'o', '0');
  -- 'Hello World'에서 'o'를 '*'로 변경
  SELECT REPLACE('HellO World', 'o', '*');
  -- 'cheese bread coffee milk'의 공백을 ' and '로 변경
  SELECT
    REPLACE('cheese bread coffee milk', ' ', ' and ');
  -- books 테이블의 title 컬럼에서 'e'를 '3'으로 변경
  SELECT REPLACE(title, 'e ', '3') FROM books;
  -- books 테이블의 title 컬럼에서 공백을 '-'로 변경
  SELECT REPLACE(title, ' ', '-') FROM books;
  ```

- REVERSE

  ```SQL
  -- 'Hello World'를 거꾸로
  SELECT REVERSE('Hello World');
  -- 'meow meow'를 거꾸로
  SELECT REVERSE('meow meow');
  -- books 테이블의 author_fname을 거꾸로
  SELECT REVERSE(author_fname) FROM books;
  -- 'woof'를 거꾸로 한 후 'woof'와 결합
  SELECT CONCAT('woof', REVERSE('woof'));
  -- books 테이블의 author_fname을 거꾸로 한 후 author_fname과 결합
  SELECT CONCAT(author_fname, REVERSE(author_fname)) FROM books;
  ```

- CHAR_LENGTH

  ```SQL
  -- 'Hello World'의 글자수를 세어줌
  SELECT CHAR_LENGTH('Hello World');
  -- books 테이블의 title의 글자수를 센 후 'length'로 명명함
  SELECT CHAR_LENGTH(title) as 'length', title FROM books;
  -- books 테이블의 author_lname의 글자수를 센 후 'length'로 명명함
  SELECT author_lname, CHAR_LENGTH(author_lname) AS 'length' FROM books;
  -- books 테이블의 author_lname의 글자수를 센 후 author_lname, ' is ', ' characters long'와 병합
  SELECT CONCAT(author_lname, ' is ', CHAR_LENGTH(author_lname), ' characters long') FROM books;
  ```

- UPPER(UCASE), LOWER(LCASE)

  ```SQL
  -- 'Hello World'를 Upper Case로 변경
  SELECT UPPER('Hello World');
  -- 'Hello World'를 Lower Case로 변경
  SELECT LOWER('Hello World');
  -- books 테이블의 title을 Upper Case로 변경
  SELECT UPPER(title) FROM books;
  -- books 테이블의 title을 Upper Case로 변경 후 'MY FAVORITE BOOK IS '와 병합
  SELECT CONCAT('MY FAVORITE BOOK IS ', UPPER(title)) FROM books;
  -- books 테이블의 title을 Lower Case로 변경 후 'MY FAVORITE BOOK IS '와 병합
  SELECT CONCAT('MY FAVORITE BOOK IS ', LOWER(title)) FROM books;
  ```

- 기타 함수

  ```SQL
  -- 'Hello Bobby'의 6번째 글자에 'There'을 삽입(HelloThere Bobby)
  SELECT INSERT('Hello Bobby', 6, 0, 'There');
  -- 'omghahalol!'의 왼쪽에서 3글자 선택(omg)
  SELECT LEFT('omghahalol!', 3);
  -- 'omghahalol!'의 오른쪽에서 4글자 선택(lol!)
  SELECT RIGHT('omghahalol!', 4);
  -- 'ha'를 4번 반복(hahahaha)
  SELECT REPEAT('ha', 4);
  -- '  pickle  '의 공백 제거(pickle)
  SELECT TRIM('  pickle  ');
  ```

## 정교화

- DISTINCT

  중복된 데이터를 제거해줌.  
  JavaScript, Python, Java, C++ 등의 프로그래밍 언어의 자료구조인 Set와 동일한 개념.

  ```SQL
  -- books 테이블의 author_lname이 중복되지 않게 선택
  SELECT DISTINCT author_lname FROM books;
  -- books 테이블의 author_fname, ' ', author_lname을 CONCAT으로 병합한 결과를 중복되지 않게 선택
  SELECT DISTINCT CONCAT(author_fname,' ', author_lname) FROM books;
  -- books 테이블의 author_fname, author_lname 모두 중복되지 않게 선택
  SELECT DISTINCT author_fname, author_lname FROM books;
  ```

- ORDER BY

  ORDER BY는 기본적으로 ASCENDING 즉 내림차순으로 되어있음.

  ```SQL
  -- books 테이블의 행을 author_lname의 내림차순으로 정렬 후 선택
  SELECT * FROM books ORDER BY author_lname;
  -- books 테이블의 행을 author_lname의 오름차순으로 정렬 후 선택
  SELECT * FROM books ORDER BY author_lname DESC;
  -- books 테이블의 행을 released_year의 내림차순으로 정렬 후 선택
  SELECT * FROM books ORDER BY released_year;
  -- books 테이블의 book_id, author_fname, author_lname, pages를 선택 후 2번째 선택한 author_fname을 기준으로 오름차순 정렬
  SELECT book_id, author_fname, author_lname, pages FROM books ORDER BY 2 desc;
  -- books 테이블의 book_id, author_fname, author_lname, pages를 선택 후 author_lname을 기준으로 정렬 후 author_fname을 기준으로 다시 정렬
  SELECT book_id, author_fname, author_lname, pages FROM books ORDER BY author_lname, author_fname;
  ```

- LIMIT

  반환되는 결과의 수를 정해줌

  ```SQL
  -- books 테이블의 title 행을 3개 반환
  SELECT title FROM books LIMIT 3;
  -- books 테이블의 전체 행을 1개 반환
  SELECT * FROM books LIMIT 1;
  -- books 테이블의 title, released_year 행을 released_year을 기준으로 오름차순 정렬 후 5개를 반환
  SELECT title, released_year FROM books ORDER BY released_year DESC LIMIT 5;
  -- books 테이블의 title, released_year 행을 released_year을 기준으로 오름차순 정렬 후 0번째부터 5개를 반환
  SELECT title, released_year FROM books ORDER BY released_year DESC LIMIT 0,5;
  -- books 테이블의 title 행을 5번째부터 50개를 반환
  SELECT title FROM books LIMIT 5, 50;
  ```

- LIKE

  `WHERE`만 사용하면 주어진 값에 정확하게 일치해야 반환이 되었지만 `LIKE`는 주어진 `WILDCARD`를 포함하는 결과를 반환해줌

  ```SQL
  -- books 테이블의 title, author_fname, author_lname, pages를 선택하고 author_fname에 'da' 앞뒤에 0개 이상의 글자가 포함되는 행만 반환
  SELECT title, author_fname, author_lname, pages FROM books WHERE author_fname LIKE '%da%';
  -- books 테이블의 title, author_fname, author_lname, pages를 선택하고 title에 ':' 앞뒤에 0개 이상의 글자가 포함되는 행만 반환
  SELECT title, author_fname, author_lname, pages FROM books WHERE title LIKE '%:%';
  -- books 테이블의 모든 행에 author_fname이 4글자인 행만 반환
  SELECT * FROM books WHERE author_fname LIKE '____';
  -- books 테이블의 모든 행에 author_fname이 a를 포함하고 앞뒤에 1개 글자를 추가로 가지고있는 행 즉 a가 가운데에 있고 3글자인 행만 반환
  SELECT * FROM books WHERE author_fname LIKE '_a_';
  ```

- ESCAPE

  `%`, `_` 등과 같이 SQL의 규칙이 적용되어 있는 문자는 ESCAPE 즉 역슬래쉬 처리를 해주어 문자라고 인지를 시켜주어야 검색이 가능하다.

  ```SQL
  -- books 테이블의 모든 행에 title에 '%' 앞뒤로 0개 글자 이상을 포함하고있는 행
  SELECT * FROM books WHERE title LIKE '%\%%';
  -- books 테이블의 모든 행에 title에 '_' 앞뒤로 0개 글자 이상을 포함하고있는 행
  SELECT * FROM books WHERE title LIKE '%\_%';
  ```

## Aggregate Functions(집계 함수)

필요한 집계 함수가 있다면 아래 링크에서 찾아 사용하면 된다.  
https://dev.mysql.com/doc/refman/8.3/en/aggregate-functions.html

- COUNT

  행의 개수를 세어줌

  ```SQL
  -- books 테이블의 전체 행의 개수
  SELECT COUNT(*) FROM books;
  -- books 테이블의 author_lname에 NULL이 아닌 값이 들어있는 행의 개수
  SELECT COUNT(author_lname) FROM books;
  -- books 테이블의 author_lname이 NULL이 아닌 값이며 중복되지 않는 행의 개수
  SELECT COUNT(DISTINCT author_lname) FROM books;
  ```

- GROUP BY

  ```SQL
  -- books 테이블의 author_lname을 기준으로 그룹화하고 author_lname과 해당 author_lname 그룹의 개수를 선택
  SELECT author_lname, COUNT(*) FROM books GROUP BY author_lname;
  -- books 테이블의 author_lname을 기준으로 그룹화 하고 author_lname과 해당 author_lname의 개수를 선택하고 author_lname의 개수는 books_written으로 명명하고, books_written을 오름차순 기준으로 정렬
  SELECT author_lname, COUNT(*) AS books_written FROM books GROUP BY author_lname ORDER BY books_written DESC;
  ```

- MIN & MAX

  ```SQL
  -- books 테이블의 pages가 제일 큰 것
  SELECT MAX(pages) FROM books;
  -- books 테이블의 author_lname이 제일 작은 것(type이 text라면 알파벳 순)
  SELECT MIN(author_lname) FROM books;
  -- books 테이블의 pages가 제일 큰 것을 찾고 제일 큰 pages에 해당하는 title, pages 선택
  SELECT title, pages FROM books WHERE pages = (SELECT MAX(pages) FROM books);
  -- books 테이블의 released_year가 제일 작은 것을 찾고 제일 작은 released_year에 해당하는 title, released_year를 선택
  SELECT title, released_year FROM books WHERE released_year = (SELECT MIN(released_year) FROM books);
  ```

- 다중 GROUP BY

  ```SQL
  -- books 테이블을 author_lname, author_fname을 기준으로 그룹화하고 author_fname, author_lname 그리고 그룹화한 행의 개수를 선택
  SELECT author_fname, author_lname, COUNT(*) FROM books GROUP BY author_lname, author_fname;
  -- books 테이블을 기준으로 author_fname, ' ', author_lname을 CONCAT으로 병합하고 그것을 author로 명명한 후 author를 기준으로 그룹화 후 그룹화한 행의 개수를 선택
  SELECT CONCAT(author_fname, ' ', author_lname) AS author,  COUNT(*) FROM books GROUP BY author;
  -- books 테이블의 author_lname을 기준으로 그룹화하고 author_lname과 해당 그룹의 제일 작은 released_year를 선택
  SELECT author_lname, MIN(released_year) FROM books GROUP BY author_lname;
  -- books 테이블의 author_lname을 기준으로 그룹화하고 author_lname과 해당 그룹의 가장 큰 released_year과 제일 작은 released_year를 선택
  SELECT author_lname, MAX(released_year), MIN(released_year) FROM books GROUP BY author_lname;
  -- books 테이블의 author_lname을 기준으로 그룹화하고 author_lname, 그룹화한 행의 개수, released_year의 최대값, released_year의 최소값, pages의 최대값을 선택하고, 그룹화한 행의 개수는 books_written, released_year의 최대값은 latest_release, released_year의 최소값은 earliest_release, pages의 최대값은 longest_page_count로 명명함
  SELECT author_lname, COUNT(*) as books_written, MAX(released_year) AS latest_release,MIN(released_year) AS earliest_release,MAX(pages) AS longest_page_count FROM books GROUP BY author_lname;
  -- books 테이블의 author_lname과 author_fname을 기준으로 그룹화하고 author_lname, author_fname, 그룹화한 행의 개수, released_year의 최대값, released_year의 최소값을 선택하고, 그룹화한 행의 개수는 books_written, released_year의 최대값은 latest_release, released_year의 최소값은 earliest_release로 명명함
  SELECT author_lname, author_fname, COUNT(*) as books_written, MAX(released_year) AS latest_release,MIN(released_year)  AS earliest_release FROM books GROUP BY author_lname, author_fname;
  ```

- SUM

  숫자가 아니면 SUM의 결과는 0

  ```SQL
  -- books 테이블의 pages의 합계
  SELECT SUM(pages) FROM books;
  -- books 테이블의 author_lname을 기준으로 그룹화 후 author_lname, 그룹화한 행의 개수, 그룹화한 행의 pages의 합계
  SELECT author_lname, COUNT(*), SUM(pages) FROM books GROUP BY author_lname;
  ```

- AVG

  ```SQL
  -- books 테이블의 pages의 평균
  SELECT AVG(pages) FROM books;
  -- books 테이블의 released_year의 평균
  SELECT AVG(released_year) FROM books;
  -- books 테이블의 released_year을 기준으로 그룹화 후 released_year, stock_quantity의 평균, 그룹화한 행의 개수
  SELECT released_year, AVG(stock_quantity), COUNT(*) FROM books
  GROUP BY released_year;
  ```
