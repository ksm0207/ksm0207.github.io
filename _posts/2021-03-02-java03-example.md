---
title: Java 01 - 자바 프로그래밍 기초(3) 변수와 자료형 내용추가
author: Kim
date: 2021-03-02 09:30 +0900   # 2019-08-20 19:34:00 0900
categories : ["Algorithms", ""]
tags: [Java,Algorithms]
comments : true
---

# 변수

변수는 프로그램에서 특정 타입의 데이터를 변수에 담아서 사용합니다<br>
새로장만한 텀블러가 있다고 하면 이 안에 ``커피`` 혹은 ``차`` 가 있을수도 있고 그외 다른 ``음료``가 있을수도 있습니다<br>
언제든지 음료종류 가 변경될 수 있는것이 ``변수`` 입니다

변수의 이름은 다음과 같이 정의할 수 있습니다

```
int coffee;
int coffee, water;
선언시 콤마 ``,``로 분리하여 여러개를 선언하는 것도 가능합니다
```

위에는 변수 선언이 되었지만 아무 값도 넣지 않은 상태인데 이것을 우리는 초기화 되지 않은 변수라고 말하고<br>
반대로 변수에 최초로 값을 할당하게 되면 초기화 된 변수라고 부릅니다<br>

만약 초기화 되지 않은 변수 와 초기화 된 변수끼리 연산을 시도하면 어떻게 될까요?<br>

```
int coffee;
int water=1;
System.out.println(coffee+water);

Error : java: variable coffee might not have been initialized
        coffee 변수가 초기화 되지 않았을 수 있습니다.
```

Java 에서 에러 를 알려주는걸 확인해볼 수 있었습니다<br>

# 리터럴

현재 변수에 값을 넣을때 사용되는 값은 ``` int water=1 ``` 이고 이런것을 즉시 사용되는값 이라고하여<br>
``` 리터럴 ``` 이라고 합니다 ( 프로그램에서 직접 표현되는 값 )

리터럴 종류는 `` 정수형 실수형 문자형 논리형 문자열 `` 이 존재하고 기본적인 타입은 다음과 같습니다<br>
<img src="/post/images/variabletype.PNG">