---
title:  자바 객체 주소값 확인
author: Kim
date: 2021-07-18 22:30:00 +0900
categories : [Java]
tags: [Java]
---

# 객체 주소

객체 출력값을 레퍼런스변수만 사용하여 확인했던 적이 많았는데 눈으로 확인하면<br>
항상 알수없는 문자로 나타나 이게 뭔가 싶었는데 특히 ```@``` 뒤에 나오는 문자가<br>
무엇을 의미하는지 궁금하여 구현을 해 보았습니다<br>

- 사용한 클래스 : Address
- 목표 : 레퍼런스변수을 출력하여 @ 뒤에 나오는 문자 의미 찾기

```java
package personal_study;

public class Address {
	
	String res = "";
	
	public Address(String res) {
		this.res = res;
	}
	public static void main(String[] args) {
		// 1. 개인 공부 - 객체 주소값 확인해보기
		Address ad1 = new Address("Kim");
		Address ad2 = new Address("Nam");

		System.out.println(ad1);
		System.out.println(System.identityHashCode(ad1));
		
		System.out.println("============================");
		
		System.out.println(ad2);
		System.out.println(System.identityHashCode(ad2));
	}
}
```

출력<br>

```java
personal_study.Address@7d6f77cc
2104457164
============================
personal_study.Address@5aaa6d82
1521118594

```
이제 의문의 @뒤에 나오는 문자와 숫자의 의미를 파악해 볼 차례입니다<br>


## System.identityHashCode

```java
System.identityHashCode()
```
위 메서드는 객체의 고유한 HashCode를 리턴하는 메서드 이면서 인자로 전달된 객체의<br>
HashCode가 정수형으로 리턴되는 메서드입니다<br>

※ 간략설명 : 인자로 전달된 객체는 10진수로 출력된다<br>

객체 키워드를 사용한 ad1 와 ad2 는 객체의 메모리 주소번지 라고<br>
조심스럽게 예상하고 @ 뒤에 나오는 문자들이 전부 16진수를 나타내는 것 같습니다<br>
```System.identityHashCode()``` 설명대로라면 전달된 객체는 10진수를 반환한다고 하였으니<br>
확인을 위해서 진수변환기를 사용 해 보았습니다<br>

<a href = "http://www.hipenpal.com/tool/binary-octal-decimal-hexadecimal-number-converter-in-korean.php">진수변환기</a><br>


## Address = Kim

먼저 ``` Kim ``` 을 가지고 있는 ad1이 나타내는 값은 16진수이고<br>
identityHashCode() 메서드가 전달된 객체의 값을 10진수로 반환한 값이면서<br>
둘다 같은 의미로 봐도 되는걸까요?<br>

```java
Address ad1 = new Address("Kim");
System.out.println(ad1); // personal_study.Address@7d6f77cc
System.out.println(System.identityHashCode(ad1)); 2104457164
```

확인결과<br>

- ad1 이 나타내고 있는 16진수 값<br>

<img src = "/post/Java/t1.png"><br>

- 16진수 에서 10진수로 변환한 결과<br>

<img src = "/post/Java/t1_res.png"><br>

결과값이 일치합니다 둘다 같은 의미이고 ```메모리 주소번지```를 나타내는게 맞는 것 같습니다<br>

정리<br>

- @ 뒤에 나오는 값은 16진수를 나타낸다
- 객체 레퍼런스 변수는 객체의 메모리 주소번지를 나타낸다고 생각하면 될 듯 하다
- 참조변수 자체는 해당되는 객체이다.
- 레퍼런스변수에 null 값을 주면 가비지컬렉션 에서 객체를 없애주고 값은 0으로 변경된다.

```java
ad1 = null;
		
System.out.println(ad1);

출력결과
0
```