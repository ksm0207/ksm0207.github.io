---
title:  자바기반의 응용SW개발자 양성과정 2일차 - 인크레파스
author: Kim
date: 2021-07-08 08:42:00 +0900
categories : [Increpas]
tags: [Increpas]
---

## Day 2 SQL 다양한 함수 , GROUP by , decode() .. 

SQL 함수는 쿼리문을 통해 얻어온 값을 조작할 수 있습니다<br>

* SQL 함수의 특징

* (1) 데이터에 대한 연산을 수행 할 수 있습니다.
* (2) 개별적인 데이터 항목을 수행 할 수 있습니다
* (3) ``` 그룹화 ``` 작업에도 용이합니다<br>

* SQL 함수의 종류

- 문자 함수
- 숫자 함수
- 날짜 함수

## SQL 문자함수

자바에서 사용하는 String 클래스에 다양하게 조작하거나 변경할 수 있는<br>
다양한 메소드들도 SQL 에서 접근할 수 있다는 것을 알게 되었습니다<br>

자바로 예를들면 대문자를 소문자로 변환할때 사용하는 메소드는 다음과 같습니다<br>
※ ```toLowerCase()```<br>

```java
String str = "HELLO JAVA";
System.out.println(str.toLowerCase());

결과 
hello java
```
반대로 대문자로 변환할 때 사용하는 메소드는 toUpperCase() 이 있습니다<br>

그럼 SQL 에서는 어떻게 컬럼명에 저장된 알파벳을 대소문자로 바꿀 수 있을까요?<br>

- LOWER(컬럼명) : 소문자로 바꿔주는 기능 - 자바의 toLowerCase() <br>
- UPPER(컬럼명) : 대문자로 바꿔주는 기능 - 자바의 toUppercase() <br>
- INITCAP(컬럼명) : 알파벳의 첫 문장을 대문자로 변환하기<br>

(1) 문제 

* 테이블 : employees
* 조건 : 직종이 프로그래머(IT_PROG) 를 가진 사원 찾기 , LOWER() 사용하기
* 출력 : 사번 , 이름 , 직종 , 입사일 순으로 출력하기

쿼리<br>

```java
SELECT employee_id, first_name, job_id, hire_date
	FROM employees
	WHERE LOWER(job_id) = LOWER('IT_PROG');
```
lower() 함수안에 인수값 인 job_id 를 넣고 = lower(IT_PROG) 역시 소문자로 변경되었습니다<br>

## 문자열 조작함수

* SUBSTR  : 특정 문자나 문자열을 추출 (위치값 , 길이)
* LENGTH  : 문자열의 길이를 반환
* REPLACE : 특정 문자 값으로 대체

<a href=#>Oracle 문자열 조작함수 알아보기 (수정예정)</a>

(1) 문제 

* 테이블 : employees
* 조건 : 부서번호가 50번인 사원들의 이름 중 'le' 를 '**'fh ``` 대체해서 ``` 표현하기<br>
* 출력 : 사번 , 이름 , 직종 , 입사일 순으로 출력하기

쿼리<br>
```java
SELECT department_id , first_name , replace(first_name , 'le','**')
FROM employees
where department_id = 50;
```

문자열 조작함수를 ```where ``` 구절에 사용해야 하는 줄 알았는데 select 문장에 사용하여<br>
값을 추출 하는 방법입니다.<br>
