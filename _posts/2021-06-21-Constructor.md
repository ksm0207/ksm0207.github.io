---
title:  생성자 (Constructor)
author: Kim
date: 2021-06-21 18:51:00 +0900
categories : [Java]
tags: [Java]
---

## 생성자 는 무엇일까 ?

예제는 다음과 같이 준비하였습니다.<br>

* Animal 클래스

```java
public class Animal {
	
	String name;
	
	public void setName(String name) {
		this.name = name;
	}
}
```

* Dog 클래스

```java
public class Dog extends Animal{
	
	public void sleep() {
		System.out.print(this.name + " Zzz ... ");
}
```

* HouseDog 클래스

```java
public class HouseDog extends Dog{
	
	public void sleep() {
		System.out.print(this.name + " 집에서 잠을 잡니다 ..." + "\n");
	}
	
	public void sleep(int hour) {
		System.out.print(this.name + " 집에서 "
	    + hour + "시간 동안 잠을 잡니다 ..."+"\n");
	}
	
	public static void main(String [] args) {
		
		HouseDog houseD = new HouseDog();
		houseD.setName("진돗개");
		houseD.sleep();
		houseD.sleep(1);
	}
```

그다음 ``` HouseDog ``` 클래스 의 main 메소드를 다음과 같이 수정해보았습니다<br>
```java
public static void main(String [] args) {
		
		HouseDog houseD = new HouseDog();
		System.out.print(houseD.name);
}
```
실행결과는 ```null``` 이 나왔고 이유는 객체 변수에 아직 아무런 값을 설정하지 않아서인데<br>

HouseDog 클래스는 개발자가 코딩하기에 따라 ```객체 변수 name```에 값을 설정하거나 안하거나<br>
값을 정할 수 있습니다<br>

그렇다면 객체 변수 name 에 ```값을 설정해야만 객체가 생성 될 수 있도록 ```<br>
강제로 할 수 있는 방법은 어떻게 하면 될까요 ? <br>

만약 값을 넣어야만 객체가 생성 될 수 있다면 객체를 생성할 때<br>
이런 코드로 만들 수 있지 않을까요 ?<br>

```java
(1) HouseDog house = new HouseDog() // 기본으로 객체 생성하는 방법

if(만약에 값을 넣어서 객체를 만들어야 하는 상황 일땐 ?)

(2) HouseDog house = new HouseDog(객체변수 타입 1 ,객체변수 타입 2 , ...)
new 연산자로 생성한 후 객체에 타입을 강제적으로 넣는다면 만들 수 있지 않을까?
```

## 생성자 생성하기

* 값을 설정해서 객체가 생성될 수 있도록 만들기

HouseDog 클래스 상단에 다음과 같은 메소드를 추가하였습니다.

```java
public HouseDog(String name) {
		this.setName(name);
}
```
생성자는 ``` 메소드 명이 클래스 명과 동일하고 리턴 자료형이 없는 메소드 ``` 입니다<br>

즉 생성자를 만들때 규칙은 다음과 같습니다<br>

* (1) 클래스 이름 과 메소드 이름이 동일해야 한다.<br>
* (2) 리턴은 정의하지 않는다.<br>

생성자는 ``` 객체가 생성 될 때 호출 되는 특징 ``` 이 있습니다<br>
객체가 생성될 때 --> ``` new ``` 연산자를 이용해 만들어 지는데<br>

즉 생성자도 역시 ``` new ``` 를 이용해 호출 된다는 것<br>

```java
new ClassName(inputType)
```

생성자는 메소드와 마찬가지로 입력을 받을 수 있습니다 때문에 클래스 상단에 추가한<br>
메소드에는 다음과 같이 문자열을 입력값으로 생성할 수 있습니다<br>
```java
public HouseDog(String name) {
		this.setName(name);
}
```
현재 main에서는 입력받은 문자열이 없기 때문에 에러를 표시하고 있을 것 입니다<br>
```java
public static void main(String [] args) {
		
		HouseDog houseD = new HouseDog(); // Error 
		System.out.print(houseD.name);
	}
```

에러 표시가 나는 이유는 객체 생성 방법이 현재 생성자 규칙과 어긋나 있기 때문인데<br>
다시말해 생성자의 규칙과 맞지 않기 때문에 애러 표시가 나는걸로 파악해 볼 수 있습니다<br>

※ ```생성자가 선언된 경우 생성자의 규칙대로만 객체를 생성할 수 있다.```<br>


객체안에 ``` 사모예드 ``` 를 넣어 출력해 보면 객체 변수가 출력 될 것 입니다.<br>

```java
public static void main(String [] args) {
		
		HouseDog houseD = new HouseDog("사모예드");
		System.out.print(houseD.name);
	}
```

※ 전체코드<br>

```java
public class HouseDog extends Dog{
	
	public HouseDog(String name) {
		this.setName(name);
	}
	
	public void sleep() {
		System.out.print(this.name + " 집에서 잠을 잡니다 ..." + "\n");
	}
	
	public void sleep(int hour) {
		System.out.print(this.name + " 집에서 "
	    + hour + "시간 동안 잠을 잡니다 ..."+"\n");
	}
	
	public static void main(String [] args) {
		
		HouseDog houseD = new HouseDog("사모예드");
		System.out.print(houseD.name); // 사모예드 출력
	}
}
```

## default 생성자

※ default : 사용자가 별도의 명령을 내리지 않아도 ``` 기본으로 적용 되어 있는 것 ```<br>
  기본값 이라고 생각하면 될려나 ?<br>

이번에는 ```default 생성자``` 에 관한 것을 알아보겠습니다<br>

* Dog 클래스

보기 1><br>
```java
public void sleep() {
		System.out.print(this.name + " Zzz ... ");
}
```

보기 2> <br>
```java

public Dog() {
		
}
	
public void sleep() {
    System.out.print(this.name + " Zzz ... ");
}
```
보기1 과 보기2 의 차이점을 알아 볼 까요 ? 두번 째 코드에는 ``` 생성자 ``` 를 구현 하였습니다<br>

```java

public Dog(){

}
```
생성자의 입력 항목이 없고 생성자 내부에 아무 내용이 없는 생성자를 ``` default ``` 생성자 라고 합니다<br>
디폴트 생성자를 구현하면 ``` new Dog() ``` 객체가 만들어 질 때 위 생성자가 실행되는데<br>

만약 클래스에 생성자가 하나도 없다면 컴파일러는 자동으로 디폴트 생성자를 추가합니다<br>
단 사용자(개발자) 가 작성한 생성자가 하나라도 구현되어 있다면 추가하지 않습니다<br>

위 내용대로 HouseDog 클래스에 추가한 메소드가 바로 이런 이유가 되는 것 이라고 이해 할 수 있겠네요<br>

## 생성자 오버로딩

하나의 클래스에 여러개의 입력항목이 다른 생성자를 만들 수 있습니다<br>

※ ```HouseDog 클래스```<br>

* 문자열 입력으로 받는 생성자

```java
// 1. String Input
	public HouseDog(String name) {
		this.setName(name);
	}
```

* 정수형 입력으로 받는 생성자

```java
// 2. Integer Input
	public HouseDog(int type) {
		if(type == 1) {
			this.setName("진돗개" +"\n");
		}else if(type == 2) {
			this.setName("말티즈" +"\n");
		}else {
			System.out.print("null");
		}
	}
```
두 생성자의 차이는 입력 항목이고 입력 항목이 다른 생성자를 여러 개 만들 수 있는 것을<br>
생성자 오버로딩 이라고 합니다 ( 기존 메소드 오버로딩 과 같은 개념)<br>

HouseDog 객체는 다음과 같이 두 가지 방법으로 객체 생성이 가능합니다<br>
```java
HouseDog houseD = new HouseDog("사모예드 \n");
HouseDog typeD = new HouseDog(1);
		
System.out.print(houseD.name);
System.out.print(typeD.name);
```

출력결과<br>
```java
사모예드
진돗개
```


