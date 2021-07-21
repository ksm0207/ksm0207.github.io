---
title:  지역변수 전역변수 차이 + Static 변수
author: Kim
date: 2021-07-19 23:20:00 +0900
categories : [Java]
tags: [Java]
pin: true
---

# 지역변수 로컬변수

자바에서 변수는 선언 위치에 따라 지역변수 와 전역변수로 나눠집니다<br> 

- 지역변수 : 중괄호 안에 생성되고 이 안에서만 사용할 수 있는 변수는 지역변수 입니다<br>
             메소드를 구현할 때 생성합니다<br>

- 전역변수 : 말 그대로 전체 어디에서든 호출하면 사용가능한 변수 입니다<br>


<strong>예시</strong><br>

```java
package personal_study;

public class Variables {   
	// 전역변수 
	int globalInteger;
	String globalString;
	double globalDouble;
	
	public void getInfo() {
		// 메소드안에 생성되는 지역변수
		String localString ="";
	}
    public static void main(String[] args) {
		Variables var = new Variables();
		
		var.globalInteger = 10;
		var.globalString  = "Global";
		var.globalDouble  = 20.5;
		
		System.out.println(var.globalInteger);
		System.out.println(var.globalString);
		System.out.println(var.globalDouble);
	}
}

출력

10
Global
20.5
```

위 코드는 전역변수를 호출하여 값을 대입 해 보았습니다<br>
만약에 지역변수를 호출하면 어떻게 될까요 ? <br>

```java
var.localString = "Hello";
System.out.println(var.localString);

에러 : localString cannot be resolved or is not a field
```

바로 빨간줄이 나오면서 에러가 발생하였고<br>
내용은 localString 을 확인할 수 없거나 필드가 아니라고 나왔습니다<br>

※ 전역변수는 같은 클래스에서만 호출 할 수 있다<br>
※ 지역변수는 특정 메소드 안에 생성하고 사용하도록 하자<br>


<strong>예시2</strong><br>

```java
package personal_study;

public class Variables {
    
	// 전역변수 
	int globalInteger;
	String globalString;
	double globalDouble;

	public void getInfo() {
		// 메소드안에 생성되는 지역변수
		String localString ="";
	}
	public void sum(int x , int y) {
		globalInteger = x + y;
		System.out.println("x = " + x); // 10
		System.out.println("y = " + y); // 20
		System.out.println("sum = "+ globalInteger); // 30
	}
	
	public static void main(String[] args) {
		Variables var = new Variables();
		var.sum(10, 20);
		
        // 30
		System.out.println("result = " +var.globalInteger);
	}
}
```

위 코드는 메인에서 sum 메소드에 인자 값을 10 과 20을 전달하였습니다<br>
전역변수 globalInteger 에는 전달 된 값을 대입하였고<br>
그 결과 30 이 나왔습니다 여기서 매개변수 ```int x int y``` 는 메소드 실행 후 종료되면<br>
값이 소멸되지만 globalIntger 는 전역변수이기 때문에 메인에서 30이라는 값이나옵니다<br>

## 전역변수 종류

- 객체변수<==>인스턴스 변수 : 객체변수는 클래스 영역에서 선언되고 클래스의 객체를 생성할 때<br>
                              만들 수 있습니다 이말은 즉 객체를 호출하여 사용해야 한다는 것<br>

- 클래스 변수는 static 변수와 같은말 입니다 객체화를 시키지 않고도 정적으로 사용이 가능합니다<br>
  객체변수가 객체화를 시킬떄마다 저장공간을 가진다면 static 변수는 공통적인 공간을 가집니다<br>


※ 저장공간      : 객체가 만들어지면서 새로운 해쉬값을 뜻함<br>
※ Static 변수   : 같은 해쉬값에서 사용할 수 있다<br>
※ 인스턴스 변수 : 항상 새로운 해쉬값이 생성된다<br>


## 인스턴스 변수 와 Static 변수 문법 활용

- 객체변수 : 기본자료형 변수이름을 가진 것을 의미하고 defalut 접근을 가지고 있습니다<br>

```java
String a;
int i;
```

- Static 변수 : static 을 붙여 기본자료형을 가질 수 있습니다

```java
static int i = 500;
```