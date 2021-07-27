---
title:  자바기반의 응용SW개발자 양성과정 15일차 - 클래스 연습하기
author: Kim
date: 2021-07-27 06:00:00 +0900
categories : [Increpas]
tags: [Increpas]
---

# 오전시간

## 클래스 안에는 어떤 내용을 지을 수 있을까?

- 멤버변수
- 멤버메소드

```java
public String test(int n){
    String str = null ;

    return str;
}
```

- 인자 n 과 str 변수는 현재 메소드안에서 정의된 변수이다(지역변수를 뜻함)
※ 지역변수는 메소드 안에서만 사용되는 변수이며 사용즉시 소멸된다<br>

- return : 메소드 안에서 만들어진 지역변수는 실행 시 소멸되는 특징이 있다<br>
           하지만 지역변수를 다른쪽에서 사용하도록 하고싶을 때 반환한다<br>


## 메소드를 활용해서 값 비교하기

```java
package am;

import java.util.Scanner;

package am;

import java.util.Scanner;

public class Ex1_Class {
	
//	멤버변수 선언
	int value;
	
//	          멤버메소드 선언
	
	// 1. 호출될 때마다 1씩 증가하는 메소드
	public void setValue() {
		value ++;
	}
	
	// 2. 호출하면 value를 반환하는 메소드
	public int getReturnValue() {
		return value;
	}
	// 3. 호출하면 정수를 하나 받아서 value 와 비교하여
	// value 보다 크면 크다를 반환하고
	// 작으면 작다를 반환하고
	// 같으면 같다를 반환해라.

	private String test(int x) {
		
		String res = "";
		
		if (x > value) {
			res = "X 는 Value 보다 크다";
		}else if (x < value) {
			res = "X 는 Value 보다 작다";
		}else {
			res = "X 는 Value 보다 같다";
		}
		return res;
	}
}
```

## Ex1_Class 필요한 메소드 사용하기

- 실행 클래스 : Ex1_Main

```java
package am;

public class Ex1_Main {
	
	public static void main(String[] args) {
		
		// 필요한 메소드를 가진 객체를 생성한다
		Ex1_Class ex1 = new Ex1_Class();
		
		int value = ex1.getReturnValue();
		
		System.out.println(value);
	}
}
출력
0
```

위 그림을 표현하면 다음과 같다<br>

<img src = "/post/Java/class2.png">

## Private 접근제한자

private 접근제한자는 외부클래스에서 사용 할 수 없다<br>
예를들면 다음 과 같은 메소드는 private 접근제한자로 설정되어 있다<br>

```java
private String test(int x) {
		
		String res = "";
		
		if (x > value) {
			res = "X 는 Value 보다 크다";
		}else if (x < value) {
			res = "X 는 Value 보다 작다";
		}else {
			res = "X 는 Value 보다 같다";
		}
		return res;
	}
```

이걸 Main에서 사용하려면 접근 조차가 안된다<br>

```java
System.out.println(ex1.check(value));
에러내용 : The method check(int) from the type Ex1_Class is not visible
           Ex1_Class 유형의 메서드 검사(int)가 표시되지 않습니다.
```

만약 test() 메소드를 사용하려면 private 접근제한자 대신 public으로 바꿔준다<br>

```java
public String test(int x) {
		
		String res = "";
		
		if (x > value) {
			res = "X 는 Value 보다 크다";
		}else if (x < value) {
			res = "X 는 Value 보다 작다";
		}else {
			res = "X 는 Value 보다 같다";
		}
		return res;
	}
```

접근제한자를 생략한다면 default 접근제한자를 의미한다<br>
※ 같은 클래스의 멤버와 같은 패키지에 속하는 멤버만 접근할 수 있다<br>

## Call by reference

- Ex1_Class

```java
package am;

import java.util.Scanner;

public class Ex1_Class {
	
//	멤버변수 선언
	int value;
	
//	          멤버메소드 선언
	public void inc() {
		value ++;
	}

	public int getReturnValue() {
		return value;
	}

	 public String check(int x) {
		
		String res = "";
		
		if (x > value) {
			res = "X 는 Value 보다 크다";
		}else if (x < value) {
			res = "X 는 Value 보다 작다";
		}else {
			res = "X 는 Value 보다 같다";
		}
		return res;
	}
}
```

- Ex1_Main

```java
package am;

public class Ex1_Main {
	
	public void t1(Ex1_Class ex1) {
		ex1.inc();
	}
	
	public static void main(String[] args) {
		// ----------------------------------------
		
		// 필요한 메소드를 가진 객체를 생성한다
		Ex1_Class ex1 = new Ex1_Class();
		
		int value = ex1.getReturnValue();
		System.out.println(value);
		
		ex1.inc(); // 1 증가
		value = ex1.getReturnValue();
		System.out.println(value);
		
//		System.out.println(ex1.check(value));
		
		// ----------------------------------------
		
		// t1 이라는 메서드를 호출하기 
		Ex1_Main m1 = new Ex1_Main();
		m1.t1(ex1); // 주소값 넣기

		System.out.println(ex1.getReturnValue());
		
		
	}
}
```

여기서 Call by reference 개념을 배워봤다 Ex1_Main 클래스에 멤버 메소드에는<br>
다음과 같은 구성이 있는데 여기서 inc() 메소드를 호출하면 어떻게 될까?<br>

```java
public void t1(Ex1_Class ex1) {
		ex1.inc();
	}
```
주목해야 할 점은 자료형이 Ex1_Class 라는 점이있다 Ex1_Main 메소드에서<br>
Ex1_Class 객체자료형을 받고 ex1.inc() 메소드를 호출하면<br>

값이 어떻게 변하는지 알아보기 위한 개념이다<br>

```java
Ex1_Main m1 = new Ex1_Main();
m1.t1(ex1); // 주소값 넣기

System.out.println(ex1.getReturnValue()); 

출력
2
```

이것도 역시 그림으로 표현 해 보았다<br>

<img src = "/post/Java/cbr.png"><br>





