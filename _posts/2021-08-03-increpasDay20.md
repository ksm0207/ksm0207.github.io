---
title:  자바기반의 응용SW개발자 양성과정 20일차 - 상속 + 메모리구조
author: Kim
date: 2021-08-03 06:00:00 +0900
categories : [Increpas]
tags: [Increpas]
---

# 상속 개념 배우기

<strong>준비한 클래스</strong><br>

- Child - 자식 클래스

```java
package am;

public class Child extends Parent {
	
	public Child() {
		System.out.println("Child Class ");
	}	
}
```

- Parent - 부모 클래스

```java
package am;

public class Parent {
	
	String value;
	
	public Parent() {
		System.out.println("Parent Class ");
	}
	
	public String getValue() {
		return value;
	}
	
	public void setValue(String value) {
		this.value = value;
	}
	
	public void getPrint(int n) {
		for(int i=0; i<n; i++) {
			System.out.printf("%s",value);
		}
		System.out.println();
	}
}
```

- Main 클래스 - 프로그램 실행

```java
package am;

public class Main {
	
	public static void main(String[] args) {
		
		Child child = new Child();	
	}
}
```

위 세가지 클래스를 메모리 구조를 그려보면 다음과 같다<br>

<img src ="/post/Java/extend.png"><br>

그림을 보면 오타가 난 부분이 있는데 Child child = new Child(); 가 맞다.<br>

Child 클래스에서 Parent 클래스를 상속받으면 Heap 영역에서 가장 먼저 Object 클래스가<br>
생성된다고 하셨다 생각해보면 그 말이 맞는 것 같다. 자바에서만 그런건지 몰라도<br>
Object 클래스는 모든 클래스의 조상이라고 배워왔기때문이다<br>

그런다음 Parent 부모 클래스 영역이 생기고 마지막으로 Child 자식 클래스 영역이 생긴다<br>
child 레퍼런스 변수가 사용할 수 있는 범위 역시 그림표와 같다<br>

※ 인스턴스 안에 객체수는 프로그램이 종료될 때 까지 내용 변경이 가능하다<br>

그럼 만약에 반대로 `Parent p1 = new Child();` 로 선언하면 구조는 어떻게 될까?<br>

<img src ="/post/Java/extend2.png"><br>

2차 레퍼런스 변수는 Parent를 가르키고 사용할 수 있는 범위가 줄어들게 되버린다<br>

다음 그림은 부모 클래스와 자식 클래스 간의 포함 관계를 나타낸 그림이다.<br>
<img src ="/post/Java/extend3.png"><br>

이미지 출처 : <a href = "http://tcpschool.com/java/java_inheritance_concept">TCPSchool</a><br>




