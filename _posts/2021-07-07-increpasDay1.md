---
title:  자바기반의 응용SW개발자 양성과정 1일차 - 인크레파스
author: Kim
date: 2021-07-07 21:15:00 +0900
categories : [Oracle,SQL]
tags: [Oracle,SQL]
---

## Day 1 오라클 XE 교육용

* 관계형 데이터베이스 (RDBMS)

※ RDBMS : Relational DataBase Management System 의 약자로<br>
 관계형 모델기반 , DBMS 유형을 뜻한다.<br>

관계형 DB 종류는 오라클 , Mysql , MS-SQL , DB2 등이 있고 이런 관계형 DB는<br>
1970년 6월 대량 공용 데이터베이스의 관계형 모델 논문이 발표 된 적이있으며<br>
크게 관심받아 지금까지 발전 해 왔다고 합니다.<br>

## 관계형 모델의 구성요소<br>

* (1) : ```데이터를 저장하는 객체``` 혹은 관계들의 집합.<br>
* (2) : 다른 관계를 생성하기 위해 관계에 가해지는 연산자의 집합.<br>
* (3) : 데이터의 대한 무결성이 보장 되어야 합니다.<br>

## SQL 문장

SQL 문장은 대소문자를 구별하지 않지만 ``` 비교값 은 구별하는 특징을 알게되었습니다 ```<br>
예를들어 테이블에 ``` USER_NAME ``` 이라는 컬럼이 있고 안에는 ```KIM``` 이 있다고 할때<br>

쿼리문을 사용하여 찾고자 하는 값이 ``` kim ``` 이랑 ``` KIM ``` 은 전혀 다른 값 이기 때문입니다<br>
왜냐하면 컬럼에는 대문자로 저장되서 대소문자를 구별한다는 특징을 붙여보면 이 때문 아닐까..<br> 

기본적인 SQL 문의 종류는 다음과 같습니다<br>

* ```DML - 데이터 조작어```<br>

* (1) 기존의 저장된 데이터를 ```수정```하고 새로운 것으로 ```업그레이드``` 시킨다 - ```UPDATE```<br>
* (2) 새로운 데이터가 추가되거나 , ```추가시킨다``` - ``` INSERT ```<br>
* (3) 데이터를 ```삭제``` 시키고 싶다 - ```DELETE```<br>
* (4) 데이터를 조회하고싶다 , 찾고싶다 - ``` SELECT ```<br>

* ```DDL - 데이터 정의어```<br>

* (1) 새로운 테이블을 생성한다 - ```CREATE```
* (2) 기존 테이블을 삭제 한다  - ```DROP```
* (3) 테이블 컬럼명을 수정한다   - ```ALTER``` 


* ```DCL - 데이터 조작어```<br>

* (1) 권한을 부여 한다 - GRANT (좀더 필요한 내용으로 이해 필요)<br>
* (2) 수거 한다 - REVOKE (위와 동일)<br>

※ 면접 질문시 , DML , DDL , DCL 중 써본게 있냐는 질문이 있을때 당당하게 얘기할 수 있도록 정리하자<br>

위 SQL 문장 종류 중 ``` SELECT ``` 문을 통해 어떻게 사용하는지 알아보도록 하겠습니다<br>
구성은 다음과 같습니다<br>

```java
[구성]
(1) SELECT   [* 또는 컬럼명1, 컬럼명2, ...., 컬럼명n]
	FROM     [테이블명]
    WHERE    [조건식] 
    ORDER BY [정렬의 기준이 되는 컬렴명]  [ASC 또는 DESC]  생략시는 오름차순이다.  
```

예시 1 : ```emploees``` 테이블의 ``` 모든 데이터를 검색 하고 싶다 ``` 라고 할땐 쿼리문은 다음과 같습니다<br>
``` SELECT * FROM emploees ``` 즉 해당 테이블의 모든 데이터를 모두 출력해서 보여줘 ! 라고 해석합니다<br>

그럼 다음 문장은 어떻게 해석할 수 있을까요?<br>

```java
SELECT employee_id , first_name , email from employees;
```

해석 : employees 테이블의 각 순번 과 첫번째 이름 그리고 이메일을 조회해줘 라고 볼 수 있습니다<br>

그 다음 문장도 이어가보겠습니다<br>
```java
employees테이블에서
      사번,이름,급여 직종 들을 순서대로 보여주는
	  SELECT문을 완성하시오!
```

위 내용대로 쿼리문을 짜보면 다음과 같습니다<br>

```java
SELECT employee_id , first_name , salary , job_id from employees
```

테이블 안에 존재하는 여러 개의 컬럼들이 존재합니다 , 그런데 특정 상황에 따라 다수의 컬럼들을<br>
``` 하나로 묶어서 ``` 표현해야 할 때는 연산자를 이용하여 존재하지 않는 컬럼을<br>
만들어 볼 수 있는데 존재하지 않는 컬럼은 어떻게 만들 수 있는 걸 까요?<br>

만약에 이런 쿼리문이 있다고 가정 해 보겠습니다<br>

```java
SELECT employee_id, first_name, last_name FROM employees;
```

사번 , 첫번째 이름 , 두번째 이름 , 이건 성 + 이름 을 뜻하는 것 같습니다 하지만 직접 조회해보면<br>
각각 컬럼마다 자리에 맞게 데이터들이 차지하고 있는데 , 여기서 성 + 이름을 합쳐보겠습니다<br>

```java
여러 개의 컬럼들을 묶어서 표현하고 싶을 때
SELECT employee_id, first_name || last_name FROM employees;
```

하지만 이름이 너무 붙어 어색하게 보입니다 , 약간의 공백을 주기위해서 다음과 같은 방법을 써봅니다<br>
```java
SELECT employee_id , first_name ||'  '|| last_name from employees;
```

아니면 컬럼명에 별칭을 붙여 볼 수도 있을 것 입니다 , 상황에 맞게 조회해서 출력 해 볼까요?<br>
```java
SELECT employee_id, first_name || last_name as fullName FROM employees;
```
``` || ``` 으로 구분짓게 하고 마지막 컬럼명에 ``` as ``` 키워드를 사용해 이름을 지어 줄 수도 있습니다<br>

## SQL - 조건부여 WHERE

기존 프로그래밍 에도 제어식이 있듯이 SQL 에서도 제어를 할 수 있습니다<br>
예를들어 에어비앤비 에서 사용자가 숙박 예약을 해야하는데 , 가장 필요한 정보는 방 시설 입니다<br>

-----이미지 첨부(예정) -----<br>

클릭한 곳에 방 시설은 깨끗한지 , 침대는 몇개 , 화장실은 몇개 , 리뷰는 어떤지 등등<br>
사용자 입장에서 원하는 데이터를 보여줄 수 있는 기술 방식 ``` WHERE ``` 키워드로<br>

요청에 따라 필요한 데이터를 처리 할 수 있습니다<br>

※ WHERE 키워드를 사용할 때 필요한 구성은 컬럼명 , 연산자 , 조건값 <br>

다음은 간단한 예제로 WHERE 키워드는 어떻게 사용하는지 알아보았습니다<br>

(1) 문제<br>

* 테이블 : employees<br>
* 조건 : 급여가 10000 이상인 사원들의 정보를 출력<br>
* 출력내용 : 사번 , 이름 , 직종 , 급여 순으로 출력하기<br>

쿼리<br>
```java
SELECT employee_id , first_name , job_id , salary
FROM employees
WHERE salary >= 10000;
```

(2) 문제<br>

* 테이블 : employees<br>
* 조건 : 직종이 IT_PROG 로 지정된 사원의 정보를 출력하기 <br>
* 출력내용 : 사번 , 이름 , 직종 , 입사일 순으로 출력하기<br>

쿼리<br>
```java
SELECT employee_id , first_name , job_id , hire_date
FROM employees
WHERE job_id = 'IT_PROG';
```

문제 2번에서 주의해야 할점은 job_id 로 데이터를 조회할 때 =="IT_PROG" 로 한다면<br>
오류가 발생합니다 , 프로그램을 구현할 때 비교연산자로 ``` 같다 ``` 의미로 사용 할 수 있지만<br>
SQL 문에서는 존재하지 않는 연산자로 ``` = ``` 를 쓰는게 좋습니다<br>

※ 오라클 에서는 "" 사용이 불가능하므로  '' 을 사용하기 <br>  
※ 데이터를 조회할 때 대소문자 꼭꼭 구분하기<br>

(3) 문제<br>

* 테이블 : employees<br>
* 조건 : 2000년도 이후에 입사한 사원들의 정보를 출력하기 <br>
* 출력내용 : 사번 , 이름 , 직종 , 입사일 부서코드 순으로 출력하기<br>

쿼리<br>

```java
SELECT employee_id , first_name , job_id , hire_date , department_id
FROM employees
WHERE hire_date >= '2000-01-01';
```

(4) 문제<br>

* 테이블 : employees<br>
* 조건 : 2000년도 이후가 아닌 2000년도 에만 입사한 사원들의 정보를 출력하기 <br>
* 출력내용 : 사번 , 이름 , 직종 , 입사일 부서코드 순으로 출력하기<br>

쿼리<br>

```java
SELECT employee_id , first_name , job_id , hire_date , department_id
FROM employees
WHERE hire_date >= '2000-01-01' AND hire_date <= '2000-12-31';
```
※ 2개 이상의 조건을 부여할 때 AND 조건과 OR 조건이 있습니다 중간에<br>
AND 연산자 혹은 OR 연산자를 넣어 구현 할 수 있습니다<br>

(5) 문제<br>

* 테이블 : employees<br>
* 조건 : 직종이 IT_PROG ```이거나``` SA_MAN 인 사원들의 정보를 출력하기 <br>
* 출력내용 : 사번 , 이름 , 직종 , 급여 순으로 출력하기<br>

쿼리<br>

```java
SELECT employee_id , first_name , job_id , salary
FROM employees
WHERE job_id = 'IT_PROG' OR job_id = 'SA_MAN';
```

(6) 문제<br>

* 테이블 : employees<br>
* 조건 : 직종이 IT_PROG ```이면서``` 급여가 5000 이상인 사원 정보를 출력하기 <br>
* 출력내용 : 사번 , 이름 , 직종 , 급여 순으로 출력하기<br>

쿼리<br>

```java
SELECT employee_id , first_name , job_id , salary
FROM employees
WHERE job_id = 'IT_PROG' AND salary >=5000;
```

## SQL - BETWEEN ,  IN ,   LIKE 연산자

BETWEEN : A 에서 B 값의 사이 , 범위의 정보를 얻을때 사용합니다<br>
구성은 다음과 같습니다<br>

```java
[구성]
WHERE colName BETWEEN A AND B
A 와 B는 값을 의미합니다
```
BETWEEN 을 사용한 예제는 다음과 같습니다<br>

(1) 문제<br>

* 테이블 : employees<br>
* 조건 : 2000년도 이후가 아닌 2000년도에만 입사한 사원들의 정보를 출력하기 <br>
* 출력내용 : 사번 , 이름 , 직종 , 입사일 부서코드 순으로 출력하기<br>

위 문제는 WHERE 키워드를 소개할 때 사용했 던 예제에서 BETWEEN 을 사용 해 봤습니다<br>

기존쿼리<br>

```java
SELECT employee_id , first_name , job_id , hire_date , department_id
FROM employees
WHERE hire_date >= '2000-01-01' AND hire_date <= '2000-12-31';
```

WHERE 구절만 보면 다음과 같이 연산자를 사용하여 데이터를 조회할 수 있었지만<br>
```java
WHERE hire_date >= '2000-01-01' AND hire_date <= '2000-12-31';
```

쿼리<br>

BETWEEN 을 사용한다면 코드가 줄어들고 가독성이 편하다는걸 느낄 수 있었습니다<br>
```java
SELECT employee_id , first_name , job_id , hire_date , department_id
FROM employees
WHERE hire_date BETWEEN '2000-01-01' AND '2000-12-31';
```

차이<br>
```java
WHERE hire_date >= '2000-01-01' AND hire_date <= '2000-12-31';
WHERE hire_date BETWEEN '2000-01-01' AND '2000-12-31';
```

(2) 문제<br>

* 테이블 : employees<br>
* 조건 : 급여가 ```8000 에서 10000 사이인 사원들의 정보를 출력하기 ``` <br>
* 출력내용 : 사번 , 이름 , 직종 , 급여 순으로 출력하되 BETWEEN 사용하기<br>

쿼리<br>

```java
SELECT employee_id , first_name , job_id , salary
FROM employees
WHERE salary BETWEEN 8000 AND 10000;
```

IN 연산자<br>

※ 특정 컬럼안에 해당 값이 속해있는지 찾아내는 연산자.<br>
※ 자바의 String 비교를 할때 사용하는 ```equals ``` 메소드와 비슷하게 사용 할 수 있습니다<br>
```java
[구성]
WHERE colName IN (value1 , value2 ...);
```

(1) 문제 <br>

* 테이블 : employees<br>
* 조건 : 급여가 2200 , 3200, 5000 , 6800 을 받는 사원들의 정보를 사용하기 <br>
* 출력내용 : 사번 , 이름 , 직종 , 급여 순으로 출력하되 IN 연산자 사용하기<br>

쿼리<br>

```java
SELECT employee_id , first_name , job_id , salary
FROM employees
WHERE salary IN (2200,3200,5000,6800);
```

만약 위 문제에서 IN 연산자를 사용하지 않는다면 다음과 같습니다<br>
```java
WHERE salary = 2200 OR salary = 3200 OR salary = 5000 OR salary = 6800;
```

LIKE 연산자<br>

컬럼에서 지정한 문자형태와 일치한 데이터를 검색합니다.<br>

형식 : % --> 모든 값 을 의미 , _(언더바) --> 하나의 값<br>
* (1) 'M%' : M 을 시작하는 모든 값 (Michael , Mike , Mother)
* (2) '%n' : n으로 끝나는 모든 값
* (3) '%a%': 중간에 a가 있는 모든 값 ( 1apart100, apple, ...)
* (4) 'M_____' : M 으로 시작하는 값들 중 전체 문자의 수가 N자인 값

※ (4) 번 경우 언더바가 5개 이므로 M으로 시작하는 값들 중 6자인 값 이다<br>

(1) 문제 <br>

* 테이블 : employees<br>
* 조건 : 입사일이 2000년도에 입사한 사원들의 정보를 출력하기 <br>
* 출력내용 : 사번 , 이름 , 직종 , 입사일 순으로 출력하되 LIKE 연산자 사용하기<br>

쿼리<br>
```java
SELECT employee_id , first_name , job_id , hire_date
FROM employees
WHERE hire_date LIKE '00%';
```

## 값을 정렬하자 - ORDER BY

질의 결과에 반환되는 행안에 존재하는 데이터를 정렬할 때 사용합니다<br>

```java
[구성]
ORDER BY 정렬기준 컬럼명 1 ASC 혹은 DESC , 정렬기준 컬러명2 ASC 혹은 DESC

먼저 기술된 정렬기준에 의해 결과가 같은것이 있으면 , 뒤에 있는
다음의 정렬기준으로 순서를 정할 수 있다
```

* ASC  : 오름차순 정렬 위에서 부터 아래로 증가하는 방식<br>
  ※ 10 11 12 13 14 15 ... 
* DESC : 내림차순 정렬 아래에서 위에서 부터 아래로 감소하는 방식<br>
  ※ 10 9 8 7 6 5 4 3 ...<br>



(1) 문제 <br>

* 테이블 : employees<br>
* 조건 : 급여가 많은 사원들 부터 출력하고 , 급여가 같다면 입사일이 빠른 사원 출력하기<br>
* 출력내용 : 사번 , 이름 , 급여 입사일 순으로 정렬하여 출력하기<br>

쿼리<br>

```java
SELECT employee_id , first_name , salary , hire_date
FROM employees
ORDER BY salary DESC , hire_date ASC;
```

(2) 문제<br>

* 테이블 : employees<br>
* 조건 : 첫번째 정렬기준 부서번호 가 빠른 것 부터 , 같다면 직종이 알파벳 순 이어야 하며<br>
         직종까지 같다면 급여를 많이 받는 사원이 출력되도록 하기<br>
* 출력내용 : 사번 , 이름 , 입사일 , 부서코드 , 직종 , 급여 순으로 정렬하여 출력하기<br>

쿼리<br>
```java
SELECT employee_id , first_name , hire_date , department_id, job_id , salary
FROM employees
ORDER BY department_id, job_id, salary DESC;
```
※ ORDER BY 구절 사용시 : ASC 는 Default 값으로, 생략하여 사용 할 수 있습니다<br>