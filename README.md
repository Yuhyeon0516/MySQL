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
