---
title:  자바기반의 응용SW개발자 양성과정 3일차 - 서브쿼리 / Join
author: Kim
date: 2021-07-09 22:00:00 +0900
categories : [Java,Oracle]
tags: [Java,Oracle]
---

# 서브쿼리 
<a href = "https://jerryjerryjerry.tistory.com/m/54">[SQL] 서브쿼리(참고사이트)</a>

서브쿼리는 SQL 문장 안에 ```또 다른 SQL 문장이 포함된 것  ``` 입니다<br>
최종 결과를 출력하는 쿼리를 ``` 메인 쿼리 ``` 라고 한다면 보조 역할을 하는<br>
SELECT문을 ``` 서브 쿼리 ``` 라고 정의할 수 있을 것 같습니다<br>

* 하나의 SQL문을 기준으로 메인 쿼리를 제외한 모든 SELECT문은 서브쿼리
* 서브쿼리는 메인쿼리가 실행되기 ``` 이전에 ``` 한번만 실행됩니다.
* 여러 개 사용할 수 있습니다.

서브쿼리 의 장점은 한번 읽어온 데이터를 메모리 안에서 가공하여 사용할 수 있도록<br>
하는 것 이고 즉 , 동일한 데이터를 다시 한번 이용하여 복잡한 가공에도 물리적인<br>
``` I/O ``` 를 줄여 줄 수 있습니다.<br>

※ I/O : 입 출력 의 약자이며 데이터를 전송하는 프로그램 , 장치를 일컫는말<br>
※ (Input / Output)<br>


정리하면 DB에 여러 번 접속해야 하는 상황을 한번에 처리가 가능하고<br>
DB에 접속시도를 줄여 속도를 증가 시킬 수 있다.<br>


서브쿼리를 사용 할 수 있는 ```사용 절``` 은 다음과 같습니다<br>

* SELECT , FROM , WHERE 절 모두 사용가능 하다.
* INSERT UPDATE DELETE 문에서도 사용 할 수 있다.
* INSERT 구문에 경우 INTO , UPDATE 구문 중 SET 에 적용 할 수 있다. 

# 서브쿼리 종류

* 1. 단일 행 서브쿼리 : 가장 기본적인 서브쿼리 이며 ```=``` 연산자를 사용합니다

* 2. 다중 행 서브쿼리 : 서브쿼리에서 반환되는 결과 행이 ``` 하나 ``` 이상일 때<br>
     사용하고 다중 행 비교 연산자 사용이 가능합니다<br>

* 3. 다중 컬럼 서브쿼리 : 하나 이상의 컬럼을 ``` 메인쿼리 로 반환 합니다.```<br>

* 4. 상호관련 서브쿼리 : 서브쿼리 와 메인쿼리 간에 결과값을 서로 주고받는 식


## 사용 시 주의사항

* 반드시 WHERE 절에 시작하고 , ``` 비교연산자의 오른쪽에 위치해야 합니다.```<br>
* 서브쿼리 문법 시작은 소괄호로 묶어서 사용합니다 ```()```
* 서브쿼리 절 안에는 ``` Order by ``` 절이 들어가면 안됩니다.



# 서브쿼리 간단히 실습해보기 

* DB : Oracle , HR계정
* 테이블 : employees
* 조건 : 사원 이름이 Michael 이고 직종이 MK_MAN 인 사원의 급여보다<br>
  ``` 더 많이 받는 ``` 사원들을 알아내기<br>
* 출력 : 사번 , 이름 , 직종 , 급여 순으로 출력<br>


(1) 먼저 사원의 이름을 찾고 직종도 찾아 급여를 알아냅니다.<br>
```java
SELECT e.first_name , e.salary , e.job_id
FROM employees e
WHERE first_name = 'Michael' AND job_id = 'MK_MAN';

결과
FIRST_NAME	SALARY	JOB_ID
Michael	    13000	MK_MAN
```


(2) 결과를 알아냈으니 급여가 13000 보다 큰 직원들은 누가 있을까요?<br>

```java
SELECT e.employee_id ,  e.first_name , e.salary , e.job_id
FROM employees e
WHERE e.salary > 13000;

결과

EMPLOYEE_ID	 FIRST_NAME	SALARY	JOB_ID
100	          Steven	24000	AD_PRES
101	          Neena	    17000	AD_VP
102	          Lex	    17000	AD_VP
145	          John	    14000	SA_MAN
146	          Karen	    13500	SA_MAN
```

(1) , (2) 는 각각 한번씩 두번을 DB에 접속한 경우이므로 이것을 서브쿼리로<br>

데이터를 처리해준 코드입니다.<br>

* SELECT , FROM , WHERE 절 모두 사용가능 하다.

```java
SELECT e.employee_id , e.first_name , e.salary , e.job_id
FROM employees e  ★ ▲ 메인쿼리 실행 (1)
                  ★ ▼ 서브쿼리 실행 (2) 
WHERE e.salary >  (SELECT e.salary FROM employees e
WHERE e.first_name = 'Michael' AND e.salary = 13000);

결과

EMPLOYEE_ID	 FIRST_NAME	SALARY	JOB_ID
100	          Steven	24000	AD_PRES
101	          Neena	    17000	AD_VP
102	          Lex	    17000	AD_VP
145	          John	    14000	SA_MAN
146	          Karen	    13500	SA_MAN
```
메인쿼리 , 서브쿼리 모두 독립적인 실행이라고 봐도 무방 할 것 같습니다.<br>


다음문제<br>

* DB : Oracle , HR계정
* 테이블 : employees
* 조건 : 사번이 111번인 사원의 직종과 같고 , 159번 사원의 급여보다<br>
    ``` 더 많이 받는 ``` 사원을 찾아내기

* 출력 : 사번 , 이름 , 직종 , 입사일 , 급여 순으로 출력하기 <br>


(1) 먼저 111번의 사원의 직종이 무엇인지 알아냅니다.
```java

SELECT e.employee_id , e.job_id
FROM employees e
WHERE e.employee_id = 111;

결과

EMPLOYEE_ID	  JOB_ID
     111	FI_ACCOUNT
```

(2) 159번 사원의 급여를 알아볼까요 ?<br>

```java
SELECT e.employee_id , e.job_id , e.salary
FROM employees e
WHERE e.employee_id = 159;

결과

EMPLOYEE_ID	  JOB_ID	SALARY
     159	  SA_REP	 8000
```

(3) 각각 결과를 알아냈으니 , 이번에도 서브쿼리로 처리한 코드 입니다.<br>

```java
SELECT e.employee_id , e.first_name , e.job_id , e.hire_date , e.salary
FROM employees e
WHERE job_id = (SELECT e.job_id FROM employees e
WHERE e.employee_id = 111) AND e.salary > (SELECT e.salary FROM employees e
WHERE e.employee_id = 159);

결과

EMPLOYEE_ID	 FIRST_NAME	  JOB_ID	HIRE_DATE  SALARY
109	          Daniel	FI_ACCOUNT	94/08/16	9000
110	          John	    FI_ACCOUNT	97/09/28	8200
```

(1) 첫번째 서브쿼리

```java
(SELECT e.job_id FROM employees e
WHERE e.employee_id = 111)

Employees 테이블에서 사원 번호가 111 번인 직종을 찾아주기
```

(2) 두번째 서브쿼리

```java
AND e.salary > 159번의 급여보다 더 받는 사람을 찾기위한 조건식

(SELECT e.salary FROM employees e
WHERE e.employee_id = 159)

사원 번호 159번의 급여를 찾아주기
```

서브쿼리를 사용할 땐 개인코딩법 마다 달라지겠지만 , 중요한건 문제를 단계별로<br>
분석하여 하나씩 접근 해줘야 마지막에 서브쿼리를 만드는데 큰 어려움이 없을 것 같습니다.<br>

# 다양한 예제로 서브쿼리 활용하기

* 새로 생성한 테이블 명 : Test
<img src = "/post/Oracle/new_table.png"><br>


* DB : Oracle , HR계정
* 테이블 : Test
* 조건 : 키가 200보다 작은 사람들 찾기
* 출력 : 번호 , 이름 , 키  순으로 출력<br>

(1) 먼저 키가 200보다 작은 사람들을 출력하기

```java
// 키가 200보다 작은 사람 찾고 , 번호 , 이름 , 키 순으로 출력

SELECT t.num_id , t.name , t.height
FROM Test t
WHERE t.height < 200;
```
<img src = "/post/Oracle/new_table_example2.png"><br>


(2) 이름이 'Kim' 인 사람의 키보다 작은 사람들 출력하기 서브쿼리 활용

```java
SELECT t.num_id , t.name , t.height
FROM Test t
WHERE t.height < (SELECT t.height FROM Test t WHERE t.name = 'Kim')
```
<img src = "/post/Oracle/new_table_example.png"><br>

# 서브쿼리 - ANY , ALL

* ANY

ANY 는 ``` 서브쿼리의 여러 개의 결과 중 한 가지만 만족합니다 ```<br>
※ SQL 연산자 종류 중 OR 와 같이 하나의 조건이 맞다면 출력 할 수 있습니다<br>

ANY 의 기본 형태는 다음 과 같습니다<br>

```java
SELECT col_name1 , col_name2 FROM 테이블이름
WHERE col_name 1 >= ANY (SELECT col_name2
FROM 테이블이름 WHERE 조건식)
```
서브쿼리 시작 시 ANY () 소괄호로 묶고 시작 할 수 있습니다<br>

* ANY 예제

* DB : Oracle , HR계정
* 테이블 : Test
* 조건 : ```주소가 인천인 사람들의 키보다 크거나 같은 경우```
* 출력 : 번호 , 이름 , 키 , 주소  순으로 출력<br>


(1) 근무지가 '인천' 인 사람들 찾는다.<br>

```java
SELECT t.num_id , t.name , t.height , t.addr
FROM Test t
WHERE t.addr = '인천';
```

(2) '인천' 인 사람들의 키보다 크거나 같은 인원을 출력한다 - 서브쿼리 & ANY

```java
SELECT t.num_id , t.name , t.height , t.addr
FROM Test t
WHERE t.height >= ANY (SELECT t.height FROM Test t WHERE t.addr='인천');
```
<img src = "/post/Oracle/any.png"><br>

※ '인천' 인 사람은 Seo 이고 ANY 조건은 Seo 보다 키가 크거나 Kim 보다 키가 크면 출력 됩니다<br>


* ALL

ALL은 서브쿼리의 여러 개의 결과를 모두 만족할 때 사용 할 수 있습니다<br>
※ AND 연산자와 같이 모든 조건이 만족해야만 합니다<br>

ALL 의 기본 형태는 다음 과 같습니다<br>

```java
SELECT col_name1 , col_name2 FROM 테이블이름
WHERE col_name 1 >= ANY (SELECT col_name2
FROM 테이블이름 WHERE 조건식)
```

* ALL 예제

* DB : Oracle , HR계정
* 테이블 : Test
* 조건 : ``` 주소가 IT 인 사람들의 키보다 작은 경우를 찾는다.```
* 출력 : 번호 , 이름 , 키 , 주소  순으로 출력<br>

```java

SELECT t.num_id , t.name , t.height , t.addr
FROM Test t
WHERE t.height < ALL (SELECT t.height FROM Test t WHERE t.addr = 'IT');
```
<img src = "/post/Oracle/all.png"><br>

주소가 IT 인 사람은 Admin 이며 ALL 조건은 Admin 보다 키가 작은 사람들이 출력 됩니다<br>


## 문제<br>

* DB : Oracle , HR계정
* 테이블 : Test
* 조건  : 주소가 여의도 인 사람들 중 키가 가장 작은 값 보다 큰 키를 가진 사람은?
* 조건2 : 내림차순으로 정렬하고 ANY 와 MIN을 사용하여 출력 해 주세요. 
* 출력 : 번호 , 이름 , 키 , 주소  순으로 출력<br>

```java
SELECT t.num_id , t.name , t.height , t.addr
FROM Test t
WHERE t.height > ANY (SELECT min(t.height) FROM Test t WHERE t.addr='여의도')
ORDER BY t.height desc;
```
<img src = "/post/Oracle/any2.png"><br>


# Join


조인은 ``` 관계형 데이터베이스 ``` 에서 ``` A 테이블 ``` 과 ``` B 테이블 ``` 간의<br>
``` 연결성을 의미합니다 ``` 또한 ``` 기본키 / 외래키 ``` 활용도 유무를 따르며<br>

※ Key : ```기본키 Primary Key``` 와 참조키(외래키) ```Foreign Key``` 가 있습니다<br>

하나의 테이블에서 여러 테이블을 한꺼번에 볼 수 있는 방법 이라 생각됩니다.<br>

※ ```두개 이상의 테이블을 서러묶어서 하나의 결과 집합으로 만들 수 있는 기술```<br>
※ 두 테이블을 묶어서 추출된 결과를 새로운 테이블을 만들어 집어 넣어 보여주는 형식<br>
  이때 새로운 테이블은 데이터베이스에 저장<br>

# Join 은 왜 필요하고 왜 쓰는 것 일까?

만약에 헬스 회원 관리 프로그램이 있다고 가정 해 보겠습니다<br>

``` A 테이블 에는 회원 테이블 ``` 이 있고 ```B 테이블에는 예약 테이블``` 이 있는데<br>
서로 Relationship (관계) 를 맺고 있을때 반드시 두개의 테이블을 조합해서만<br>
원하는 정보를 얻어야 하는  ``` 상황 ``` 이 왔을 때 사용합니다<br>

※ 경우에 따라 C 테이블 , D 테이블 등 필요한 조건에 따라 늘어 날 수 있습니다<br>

이때 , 두 테이블 모두 각각 검색해서 정보를 도출해야하는데 결국은 조회를 2번이나<br>
해야한다는 뜻이 되는데요 , 하지만 Join을 사용하면 2번 조회를 거칠 필요 없이<br>
단 한번만 검색해서 정보를 알 수 있게 됩니다<br>

즉 두 테이블을 한번에 묶어 보여주기 위해 Join을 사용하고 두개 이상의 테이블을<br>
결합하여 원하는 결과를 얻기 위한 기술이라고 정리하면 될 것 같습니다<br>

Join 종류는 다음 과 같습니다<br>

* (1) InnerJoin : 조인 조건이 정확히 일치하는 경우 사용합니다<br>


* (2) OuterJoin : 조인 조건이 정확히 일치하는 ``` 행 ``` 과<br>
    ``` 일치하지 않은 모든 행들을 알고 싶을 때 ``` 활용하는 방법<br>

* (3) SelfJoin : 하나의 테이블에서 ``` 특정 컬럼과 연결성을 가지는 경우 ```

* 더 많은 종류가 있으면 추가할것 .


# Inner Join

* Inner Join 은 내부조인 이라 부르며 , 조인 기술 중에서 가장 많이 사용되는 조인 입니다<br>
※ 일반적으로 Join ! 이라고 하면 내부조인 입니다.<br>

* 각 테이블의 기본키와 참조키를 구분하여 사용해야 합니다.


## Inner Join 실습코드

* DB : Oracle , HR계정
* 테이블 : employees , departments
* 조건 : 각 ``` 사원들 ``` 의 ``` 부서코드 ``` 로 부서명을 알아내기
* 출력 : 사원번호 , 이름 순으로 출력하기<br>

(1) 시작하기전 , 오류코드 부터 알고 들어가기<br>

```java
SELECT employee_id , first_name , department_id , department_name
FROM employees , departments
WHERE employees.department_id = departments.department_id;

결과

ORA-00918: 열의 정의가 애매합니다
```

오류가 일어나는 부분은 department_id 에서 일어났습니다 그 이유는 <br>
Employees , Departments 테이블 모두 가지고 있는 컬럼이기 때문에 Oracle 입장에서는<br>

어느 테이블에서 department_id 값을 가져올지를 판단하지 못해 발생한 오류입니다<br>
그렇다면 수정할 곳은 컬럼명 앞에 사용자가 원하는 테이블명을 기술할 수도 있습니다<br>

(2) 수정 한 코드 (InnerJoin 적용)<br>

```java
SELECT e.employee_id, e.first_name, d.department_id, d.department_name
FROM employees e, departments d
WHERE e.department_id = d.department_id;

※ 프로그래밍에서 사용하는 . 연산자로 구분지어 값을 추출 할 수 있다는 것을 알게됨..
```


(3) 위 문제를 서브쿼리로 풀어본다면?

```java

SELECT e.* , d.department_name

FROM (SELECT employee_id , first_name , job_id , department_id FROM employees)e,

(SELECT department_id , department_name FROM departments d )d

WHERE e.department_id = d.department_id;
========================================

(1 ) employees 의 모든 컬럼명 , departments 의 name 을 조회
SELECT e.* , d.department_name

(2) 첫번째 서브쿼리 , employees 테이블에 각 컬럼명을 조회
FROM (SELECT employee_id , first_name , job_id , department_id FROM employees)e,

(3) 두번째 서브쿼리 , departments 테이블에 각 컬럼명 조회
(SELECT department_id , department_name FROM departments d )d

(4) 조건 : employees 테이블의 department_id 가 department 테이블 id가 같은지 확인
```

위 문제대로 내가 알던 서브쿼리 작성문<br>

```java
SELECT e.employee_id , e.first_name , e.job_id , d.department_id , d.department_name

FROM employees e , departments d

WHERE e.department_id = d.department_id;
```

InnerJoin 을 사용 후 서브쿼리 작성문<br>

```java
SELECT e.* , d.department_name

FROM (SELECT employee_id , first_name , job_id , department_id FROM employees)e,

(SELECT department_id , department_name FROM departments d )d

WHERE e.department_id = d.department_id;
```



