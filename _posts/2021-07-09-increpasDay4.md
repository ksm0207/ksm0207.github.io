---
title:  자바기반의 응용SW개발자 양성과정 4일차 - 테이블 생성 , 데이터타입
author: Kim
date: 2021-07-12 10:30:00 +0900
categories : [Java,Oracle]
tags: [Java,Oracle]
---

# Day 4 - 테이블 생성 , 데이터 저장

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
※ CONSTRAINT book_t_pk PRIMARY KEY(b_idx) = PRIMARY KEY 지정 한 것<br>

※ Varchar2() 값을 지정하거나 , ```()``` 생략 가능하지만 , 자리수 가 없으면 연산속도가 늦는다고 함!<br>
※ Varchar2() 에 입력하는 숫자 1당 n 글자를 뜻하고 ,  각각 1~2KB 차지함 , 즉 자리 수 라고 이해 하기.<br>


※ number () = > 데이터 안에 넣을 수 있는 것은 숫자의 자리수를 의미합니다<br>
5자리는 number(5) 이며 , 9 9 9 9 9 까지 입력 가능하고 <br>
``` ※ 6.2를 넣으면  총 자리수 는 6 ```, 2 소수점 자리수 를 의미함. 예시 : 1000.00<br> 

기본키 : ```PRIMARY KEY```  , 테이블에 저장되는 레코드<br>
레코드 : 테이블로 예를들면 , 책 한권의 정보를 뜻하고 PK는 중복이 되어선 안되며 null이 허용되면 안된다<br>

현실 세계 -> 개인이 각자가 가지고 있는 주민번호가 여기에 속함<br>



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





