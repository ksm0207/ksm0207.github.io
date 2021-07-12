---
title:  자바기반의 응용SW개발자 양성과정 4일차 - 테이블 생성 , DML , 계정생성 권한부여
author: Kim
date: 2021-07-12 10:30:00 +0900
categories : [Java,Oracle]
tags: [Java,Oracle]
---

# 테이블 생성 

- 정리 : 그룹함수 , having 절 자세히 공부하기 

* 테이블 생성법

```java

CREATE TABLE 테이블명

(
    컬럼명 1 자료형, 고유 키 값 PRIMARY KEY
    컬럼명 2 자료형,
    컬럼명 3 자료형
    .
    .
    .
    키워드 : CONSTRAINT (제약조건명) 제약조건
    제약 조건을 명시하는 행위
);
```
※ 여기서 제약조건 이란 .. 어떤 ```특정 컬럼에 값을 정의 할 수도 있고 안 할 수도있다```<br>
※ EX ) null 지정 , 혹은 무조건 값이 지정되어야만 할 때 등등..<br>


다음은 책 을 저장하는 테이블을 만들어 보았습니다<br>
책에 대한 정보들을 테이블에 저장하기 위해 먼저 사용자 입장에서 필요한 정보가 어떤 것 들이 있을지<br>
선별하고 판단 할 줄 알아야합니다.<br>

* TABLE : 책
* 컬럼  : 책 아이디 , 책 제목 , 저자 , 출판사 , 가격

```java
CREATE TABLE book_t(

    b_idx number(3),
    title  Varchar2(200),
    author Varchar2(50),
    brand Varchar2(50),
    price number(6),

    CONSTRAINT book_t_pk PRIMARY KEY(b_idx)
);



```
※ CONSTRAINT : 제약조건 이라는 사전용어<br>
※ CONSTRAINT ```book_t_pk PRIMARY KEY(b_idx)``` = PRIMARY KEY 고유 값 지정<br>

※ Varchar2() 값을 지정하거나 , ```()``` 생략 가능하지만 , 자리수 가 없으면 연산속도가 늦는다고 함!<br>
※ Varchar2() 에 입력하는 숫자 1당 n 글자를 뜻하고 ,  각각 1~2KB 차지함 , 즉 자리 수 라고 이해 하기.<br>


※ number () = > 데이터 안에 넣을 수 있는 것은 숫자의 자리수를 의미합니다<br>
숫자의 5자리만 입력제한을 주고싶다면 number(5) = ```9 9 9 9 9``` 까지 입력 가능하고 <br>

``` ※ 6.2를 넣으면  총 자리수 는 6 이고``` , 2 소수점 자리수 를 의미함. 예시 : 1000.00<br> 

고유키 : ```PRIMARY KEY ```  , 테이블에 저장되는 레코드<br>
레코드 : 테이블로 예를들면 , 책 한권의 정보를 뜻하고 PK는 중복이 되어선 안되며 null이 허용되면 안된다<br>
<img src ="/post/Oracle/pri.png"><br>

사진에 보이는 것 처럼 ``` m_idx ``` 는 ``` 고유키를 뜻하며 순차적으로 가지고 있는 레코드``` 예시 입니다<br>


# ALTER

만약 ``` 테이블 생성 후 추가로 컬럼을 추가하려면```  다음 과 같이 작업을 진행 할 수 있습니다<br>

- ALTER - add 새로운 컬럼 추가

```java
    ALTER TABLE 테이블 명
    ADD (추가할 컬럼명 자료형);

    ALTER TABLE book_t add( col_name , date_type() );
```

이번엔 테이블에 있는 ``` 기존 컬럼 값 을 수정``` 해야 할 때는 다음 과 같이 진행합니다<br>

- ALTER - modify 컬럼 값 수정

```java
    ALTER TABLE 테이블 명
    MODIFY 컬럼명 자료형;

    ALTER TABLE book_t MODIFY price number(8);
```

- ALTER - Rename 컬럼 이름 수정

```java
    ALTER TABLE TABLE 테이블 명
    RENAME col_name 대상컬럼명 TO 대상컬럼명

    ALTER TABLE book_t RENAME COLUMN reg_date TO write_date;
```

- ALTER - DROP 컬럼 삭제

※ 컬럼이 삭제되면 안에 데이터 가 모두 삭제됨<br>

```java
    ALTER TABLE 테이블 명
    DROP COLUMN 삭제할 컬럼명

    ALTER TABLE book_t DROP COLUMN write_date;
```


# Memo 테이블

* Memo 테이블 생성 하기

```java
CREATE TABLE  MEMO 
   (	M_IDX NUMBER(5,0), 
	TITLE VARCHAR2(20), 
	CONTENT VARCHAR2(4000), 
	PW VARCHAR2(16) NOT NULL ENABLE, 
	WRITER VARCHAR2(20), 
	WRITE_DATE DATE, 
	IP VARCHAR2(30), 
	 CONSTRAINT "MEMO_PK" PRIMARY KEY (M_IDX) ENABLE
   );
```

※ Content 데이터 유형은 Varchar 로 총 2000자 까지 작성 할 수 있습니다<br>

만약 게시판에 내용을 담기에는 ```4000``` 을 데이터 유형으로 넣기가 다소 부족한 경우가<br>
있습니다 , 때문에 게시판의 글 내용으로는 ```CLOB``` 이라는 자료형이 적합하며<br>

```CLOB 은 최대 문자 값들을 총 4GB 까지 저장할 수 있습니다```<br>

※ 한번 지정한 Varchar2() 에서 CLOB 으로 바꾸려면 , 기존 컬럼을 삭제 후 다시 생성해야 한다<br>
※ ```파일저장은 BLOB```을 사용하고 ```CLOB이 문자열 을 저장한다면``` BLOB은 , 파일 , 이미지 저장 하는데 쓰인다.<br>


# 문자열을 저장하는 데이터 타입 유형

* Varchar - 가변형
* Char - 고정형
* CLOB - 최대 문자값 4GB 저장

## Varchar2 와 Char 차이

* Varchar 데이터 저장  - 최대 4000Byte
* Char 데이터 저장- 최대 2000Byte

## VarChar2 - 가변형 이고 Char - 고정형 이다 이게 무슨말이야?

자료형 유형이 ```Char(8) ``` 이나 ```VarChar2(8)``` 로 저장했을 때 차이는 어떻게 날까요?<br>
예를들어 비밀번호를 저장하는 ``` pw ``` 컬럼이 있다고 가정 해 보겠습니다<br>

Kim 이라는 유저가 비밀번호를 ``` 1234 ``` 로 저장했는데 이때 컬럼 타입이 Char(8) 이면 <br>
컬럼에는 ``` 1234 ``` 가 아닌 ``` '1234  공백포함8자리 ' ``` 으로 저장합니다<br>

이유는 ```Char() 는 고정형 길이를 가지고 있기 떄문에 공백 포함 총 8자리를 채웁니다```<br>

※ : VARCHAR2 가변형 내용 추가하기.


# 데이터 추가 INSERT INTO

- Insert 구문 예시 1

```java
INSERT INTO 테이블명 ( 컬럼명 1 , 컬럼명 2, 컬럼명 3, 컬럼명4)
VALUES (value1 , value2 , value3 , value4) 
```

- Insert 구문 예시 2

```
INSERT INTO [테이블명] VALUES(value1, value2,..., value n)
```


- Insert 구문 예시 3 - 서브쿼리

```java

INSERT INTO 테이블명 (컬럼명1 , 컬럼명2, 컬럼명3, 컬럼명4)
SELECT value1 , t.컬럼명2 , t.컬럼명3, ....

FROM   test t(파라미터)
WHERE t.컬럼명2 = 'find_value'
```

※ Insert 할때 ```컬럼에 Null 값을 허용하지 않은 컬럼은``` 무조건 값이 있어야 하므로 확인하고 쓰기<br>

## 첫번째 데이터 넣기

```java
insert into memo (m_idx,title,writer)
values(1,'테스트','writer테스트');
```
<img src = "/post/Oracle/insert.png"><br>

만약 Null 유형이 NotNull 일 경우에는 생략하여 값을 넣어 줄 수도 있다<br>


# 데이터 수정 Update

구성<br>

```java
UPDATE table_name
SET col_name1 = value1 , col_name2 = value2 ..

WHERE 조건식;
```

문제<br>

m_idx 가 2번인 데이터에 writer 의 값을 '어두일미' 로 변경하기<br>

```java
UPDATE Memo SET writer = '어두일미'
WHERE M_idx = 2;
```
<img src = "/post/Oracle/update.png"><br>

UPDATE TIP : 바꾸고자 하는 데이터를 먼저 SELECT 로 확인 후<br>
      UPDATE 절을 수행하는 것이 바람직 하다고 하심<br>


# 데이터 삭제 - DELETE

※ 게시판 삭제 글 -  데이터 유형은 boolean 형태로 0 , 1 로 확인하기.<br>
``` Status ``` - 현황<br>

DELETE 는 말 그대로 삭제 할 때 사용하지만 , 실무에서는 사용빈도가 낮은 편<br>

구성<br>

```java
DELETE FROM table_name
WHERE 조건식 부여
```

# 계정 생성 및 권한 부여

롤(Role)<br>

사용자에게 허가 할 수 있는 권한들의 집합<br>

* Role을 이용하면 권한부여 및 회수를 쉽게 가능하다
* CREATE Role 권한을 가진 유저에 의해서 생성된다
* 사용자가 여러개의 Roll를 승인할 수 있고 여러 사용자에게도 부여 가능
* 오라클 DB는 기본적으로 사용자에게 CONNECT , RESOURCE , DBA Role이 제공된다

※ RESOURCE = 객체(테이블 , 생성 수정 삭제)  기능 권한 부여<br>

DBA는 유저들에게 권한을 부여할 때 하나씩 권한을 주면 번거로운 일이 발생하기 때문에<br>
유저의 역할에 맞도록 Role 을 생성하여 유저들한테 지정한다면 효율적인 관리가 될 것 같다.<br>

Role을 사용하지 않을경우<br>
```java
DBA 권한1 권한2 권한3

유저 1 : 권한 1 2 3 부여
유저 2 : 권한 1 2 3 부여
.
.
.
```

Role을 사용 할 경우<br>

```java
DBA 권한1 권한2 권한3
Role : DBA 로 부터 권한을 받음

유저 1 : Role 부여
.
.
.
```

위 내용대로 사용자 및 권한(Role) 설정 하는법을 알아보도록 하겠습니다<br>
사용자 계정을 생성하려면 먼저 ```System(DBA)``` 으로 로그인을 해 줍니다<br>

* sql 명령줄 실행 프로그램 (CMD) 실행
<img src ="/post/Oracle/conn1.png"><br>

사용자 계정 생성<br>

* CREATE USER   user_id
* IDENTIFIED BY user_pw

<img src ="/post/Oracle/create_user.png"><br>

생성된 계정으로 접속을 시도하면 다음 과 같이 오류가 발생합니다<br>
<img src ="/post/Oracle/user_login_no.png">

※ 아직 데이터베이스에 접속권한을 받지않은 상태로 DBA로 부터 기능을 부여받아야 합니다<br> 

DBA - 권한부여<br>

<img src ="/post/Oracle/grant.png"><br>

사용자 계정 test는 앞으로 데이터베이스에 접속권한 , RESOURCE 를 받았다면<br>
임의 테이블을 생성하고 편집 및 삭제는 가능하지만 다른 계정이 만든 테이블을 접근하거나<br>
RESOURCE 기능을 할 수가 없습니다<br>

예를들어 Memo 테이블은 HR계정소유 이므로 새로 생성한 test 계정이 접근할 수 없다는 것 입니다<br>
<img src ="/post/Oracle/memo.png"><br>

하지만 언젠가 협업을 해야 할 때 , test 계정에 최소한의 기능과 권한을 부여 할 수는 있습니다<br>
이를 수행하기 위해 먼저 HR계정으로 연결 해 줍니다<br>

HR --> test 권한부여<br>
<img src ="/post/Oracle/grant2.png"><br>

※ GRANT : 승인(허락)하다 사전적의미<br>
권한이 제대로 부여받았는지 test 계정으로 연결하여 확인 해 줍니다<br>

<img src ="/post/Oracle/privs.png"><br>

``` SELECT * FROM USER_TAB_PRIVS_RECD  ( 내가 받은 권한 확인 ) ```<br>

이 명령어로 통해 ```OWNER ```  와  ``` TABLE_NAME ``` 쉽게 확인 할 수 있습니다<br>
<a href="http://totoriver.egloos.com/v/2439843">참고 : 오라클 USER 생성 및 권한관리</a>

※ HR 계정이 만든 테이블에 접근할 때는 테이블명 + . 연산자로 접근 할 수 있습니다<br>
※ hr.memo<br>


## 권한 수거

권한을 부여한 사용자에게 다시 권한을 해지하려면 Revoke 가 있습니다<br>

```java
SQL> conn hr/1111;
연결되었습니다.

SQL> Revoke select , insert ON Memo FROM test;
권한이 취소되었습니다.
```

Revoke : 사용자에게 주었던 ``` SELECT , INSERT 권한 등을``` 수거해주는 키워드<br>
Revoke 사전적 의미 : 해지하다<br>