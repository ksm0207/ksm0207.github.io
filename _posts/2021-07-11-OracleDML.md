---
title:  Oracle DML 연습하기
author: Kim
date: 2021-07-09 22:00:00 +0900
categories : [Java,Oracle]
tags: [Java,Oracle]
---

# DML 종류 와 뜻

```DML - 데이터 조작어```<br>

* Insert - 값을 넣을 때 사용
* Select - 테이블 조회 
* Update - 테이블 의 값을 수정 할 때
* Delete - 말 그대로 지우기.



# Insert 방법 & 데이터입력

Oracle에서 테이블에 데이터를 입력할 때는 Insert 문을 사용하면 됩니다<br>
Insert 문은 SQL의 가장 기본적인 방법이며 , 상황에 따라 다양한 방법으로 사용 할 수 있습니다<br>



- Insert 구문 예시 - 기본 사용법

```java

INSERT INTO 테이블명 ( 컬럼명 1 , 컬럼명 2, 컬럼명 3, 컬럼명4)
VALUES (value1 , value2 , value3 , value4) 
```

- DB : Oracle , 새로운 테이블 생성 + 값 넣어보기

(1) HR계정에 새로운 테이블을 생성합니다<br>
```java

CREATE TABLE MyFirstTable

( num_id number PRIMARY
,   name  varchar2(30)
,   email varchar2(30)
,   gender varchar2(30)
, fav_food varchar2(30)
, birth_day date);
```

(2) INSERT 구문을 사용하여 데이터에 추가<br>

```java
INSERT INTO MyFirstTable

(num_id , name , email,gender,fav_food , birth_day)
VALUES (1,'Kim','Gmail','Man','삼겹살',to_date('1995-02-07','yyyy-mm-dd'));
```

(3) 값 조회하기<br>

```java
SELECT * FROM MYFirstTable;
```
결과<br>

<img src = "/post/Oracle/insert_result.png">

작성시 ```INTO 절의 컬럼 개수 , 데이터 타입```이 ```VALUES 절의 컬럼 개수와 데이터 타입은 동일해야 합니다```<br>

※ VALUES 절에 테이블의 모든 컬럼이 나열되어 있다면 INTO 절의 컬럼을 생략할 수 있지만<br>
  INTO 절에 입력할 컬럼을 모두 나열하는 방식을 권장합니다.<br>


만약 VALUES 절에 입력할 테이블의 모든 컬럼이 나열되어 있다면 INTO 절의 테이블 명만 존재하고<br>
컬럼은 생략할 수 있습니다<br>

```java
INSERT INTO 테이블명
VALUES (value1 , value2 , value3, value4 )
```

※ 실무에서는 쿼리를 작성할 때 INTO 절에 컬럼을 모두 작성할 것을 권장합니다.<br>
  테이블에 컬럼이 추가되거나 삭제되었을 경우 기존 쿼리문에 오류가 발생할 수 있는 가능성이 생김<br>


# Insert - 서브쿼리 (SELCT INSERT)

서브쿼리는 INSERT 구문에도 사용 할 수 있습니다<br>
기존 INSERT 구문 작성 시 ``` VALUES ``` 를 사용하였지만 이 대신 SELECT 를 사용할 수 있습니다<br>

즉 서브쿼리 작성이 가능하다는 얘기가 됩니다<br>

※ 여러 개의 데이터를 INSERT 하거나 , 기본 값을 조회 후 파라미터로 전달된 값과 합쳐 사용가능.<br>
※ FROM절 뒤에 WHERE 절 사용 가능.<br>

```java

INSERT INTO 테이블명 (컬럼명1 , 컬럼명2, 컬럼명3, 컬럼명4)
SELECT value1 , 참조변수.컬럼명2 , 참조변수.컬럼명3, ....

FROM 테이블명 . 참조변수(파라미터)
WHERE 참조변수.컬럼명2 = 'IT'

```


# HR 테스트 계정 , 무결성 제약조건이 위배

employees 테이블에 INSERT를 시도하였다가 갑자기 무결성 제약조건이 위배되었다<br>
``` 부모 키가 없습니다 ``` 라는 에러가 발생하였습니다<br>

에러의 원인은 찾아본 결과 다음 과 같습니다<br>

- 테스트 코드의 데이터 생성시
- 부모 테이블에서 참조하는 컬럼의 값인 Foreign Key 값은
- 부모 테이블에 ``` 먼저 존재해야만 참조 가능 ```

즉 참조하려는 부모 테이블의 컬럼 값이 존재하지 않아 ```무결성 제약조건이 위배```되었다 라고 볼 수 있습니다<br>

Solution<br>

Foreign Key로 사용되는 컬럼 값을 부모 테이블의 컬럼에 먼저 생성한 후<br>
생성된 해당 키 값을 자식 테이블에서 참조할 수 있도록 데이터를 넣어줍니다.


# employees 테이블에 새로운 데이터를 Insert 하기.




# 외래키 제약 조건
