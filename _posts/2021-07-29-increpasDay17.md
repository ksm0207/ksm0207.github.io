---
title:  자바기반의 응용SW개발자 양성과정 17일차 - 클래스 연습 + 자판기 프로그램2
author: Kim
date: 2021-07-29 06:00:00 +0900
categories : [Increpas]
tags: [Increpas]
---

이번시간에도 클래스 개념과 객체지향 프로그램을 만들어보는 예제로<br>

꽃 자판기를 만들어봤는데 객체지향 프로그램이 무엇인지 흐름을 알게해주는 시간이었다<br>


# 꽃 자판기

- Flower 클래스

```java
package am;

public class Flower {
	String name;
	String create_date;
	int price;
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getCreate_date() {
		return create_date;
	}
	public void setCreate_date(String create_date) {
		this.create_date = create_date;
	}
	public int getPrice() {
		return price;
	}
	public void setPrice(int price) {
		this.price = price;
	}
}
```

Flower 클래스는 설계도면에 필요한 아이템들을 정의해준다<br>
그럼 아이템들을 가지고 동작이 필요한 클래스 역시 필요하다<br>
Flower 클래스에 정의해도 상관없지만 객체지향을 배워보는 것 이기때문에<br>

동작이 필요한 클래스 VendingMachine (자판기) 을 만들어 주었다<br>
여기서 동작이란 무엇을 의미하는걸까 ?<br>

- 자판기에 돈을 넣는다
- 구매할 수 있는 꽃을 확인한다
- 번호를 고른다
- 꽃을 구매하고 잔액이 얼마나 남아있는지 확인한다

위 처럼 실제 생활에서 해볼 수 있는 이런 것들을 의미한다고 생각한다<br>
다른 예로 라면을 끓인다고 가정해보면 필요한 것들이 무엇이 있는지 생각해보자<br>

- 냄비에 물을 끓인다
- 적절한 물의 온도가 맞춰지면 라면을 넣는다
- 푹푹 끓인다
- 스프를 넣고 추가로 넣고싶은 재료를 넣는다

동작은 우리 사람이 생활하는 모습을 프로그래밍 언어로 표현될 수 있고<br>
자바에서는 이런것을 모두 객체지향 프로그래밍 이라고 하는 것 같다<br> 


- VendingMachine 클래스 아이템을 가지고 동작을 만들어보자

```java
package am;

import java.util.Scanner;

public class VendingMachine {
	
	// 꽃을 5개만 판매하는 자판기
	Flower [] items = new Flower[5];

//	Flower [] items;
	
	// 배열 초기화
	public void initItems() {
		// 배열을 생성하고 각 요소에 초기화 하는 반복문
//			items = new Flower[5];
		for (int i=0; i<items.length; i++) {
			items[i] = new Flower();
			switch (i) {
			case 0:
				items[i].setName("해바라기");
				items[i].setPrice(1000);
				items[i].setCreate_date("2021-07-25");
				break;
			case 1:
				items[i].setName("장미");
				items[i].setPrice(1500);
				items[i].setCreate_date("2021-07-26");
				break;
			case 2:
				items[i].setName("노랑국화");
				items[i].setPrice(1800);
				items[i].setCreate_date("2021-07-27");
				break;
			case 3:
				items[i].setName("백합");
				items[i].setPrice(2000);
				items[i].setCreate_date("2021-07-28");
				break;
			case 4:
				items[i].setName("튤립");
				items[i].setPrice(2000);
				items[i].setCreate_date("2021-07-29");
				break;
			}
		}// end of for loop(1)
	}
	
	// 금액을 인자로 받고 금액의 범위안에 속하는 꽃들을 출력하기
	public boolean getPrint(int money) {
		boolean flag = false;
		
		for (int i=0; i<items.length; i++) {
			// 배열로부터 객체를 하나씩 가져오기 (변수를 빼서 가져오는방법)
			Flower flower = items[i];
			if (money >= flower.getPrice()) {
				System.out.printf("%d.%s:%d ",
						i+1,
						flower.getName(),
				        flower.getPrice());
				flag = true;
			}
		}// end of for loop(1)
		System.out.println();
		
		if (!flag)
			System.out.println("금액이 부족합니다.");
		
		return flag;
	}// end of getPrint()

	public int getItems(int u_money , int userChoise) {
		
		if (u_money - items[userChoise].getPrice() >= 0) {
			System.out.println("주문하신 " + items[userChoise].getName() + " 나왔습니다 !" + items[userChoise].getCreate_date());
			u_money = u_money - items[userChoise].getPrice();
			System.out.println("남은잔액 : " + u_money + " 원");
		}else {
			System.out.println("잘못된 입력입니다.");
		}
		
		return u_money;
	}
}
```

이제 동작을 간단하게 만들어보고 Main 클래스에서 테스트를 진행해보자<br>

- Main 클래스 - 프로그램 시작

```java
package am;

import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		
		// 자판기 객체
		VendingMachine vend = new VendingMachine();
		// 객체 호출
		vend.initItems();

		int userChoise;
		
		Scanner scan = new Scanner(System.in);
		System.out.print("금액을 입력해주세요 :");
		int u_money = scan.nextInt();
		
		boolean check = vend.getPrint(u_money);
		
		if (check) {
			System.out.print("구매 번호 : ");
			userChoise = scan.nextInt() -1;
			u_money = vend.getItems(u_money, userChoise);
		}
	}
}
```

## 프로그램 실행

실행을 해보면 다음과 같다<br>

- (1) 금액을 5000원 넣고 장미를 구매하기

<img src = "/post/Java/vend1.png">

- (2) 돈을 적게 넣고 금액이 부족하다는 문구를 출력하기

<img src = "/post/Java/vend2.png">

위 사진은 VendingMachine 클래스의 getPrint() 메소드에서 실행 된 것이다<br>

```java
// 금액을 인자로 받고 금액의 범위안에 속하는 꽃들을 출력하기
	public boolean getPrint(int money) {
		boolean flag = false;
		
		for (int i=0; i<items.length; i++) {
			// 배열로부터 객체를 하나씩 가져오기 (변수를 빼서 가져오는방법)
			Flower flower = items[i];
			if (money >= flower.getPrice()) {
				System.out.printf("%d.%s:%d ",
						i+1,
						flower.getName(),
				        flower.getPrice());
				flag = true;
			}
		}// end of for loop(1)
		System.out.println();
		
		if (!flag)
			System.out.println("금액이 부족합니다.");
		
		return flag;
	}// end of getPrint()
```

Main 클래스에서 인자값을 받고 범위내에 구매할 수 있는<br>
꽃을 출력해준다 첫번째 if문이 이 역할을 하고 꽃 리스트를 볼 수 있는 금액은<br>
최소 1000원 부터 가능하다<br>

만약 1 ~ 999까지 금액을 입력받으면<br>
두번째 if문에서 flag를 만나게 되서 금액이 부족합니다. 문구가 출력된다<br>

아무튼 이렇게 자판기 프로그램을 만들어보았다<br>

## 도서관 프로그램

이번엔 도서관에서 도서를 검색하면 도서의 정보를 확인하는 프로그램을 만들어보자<br>

조건은 다음과 같다<br>

<img src = "/post/Java/book.png"><br>

예전에 알고리즘 문제를 풀어봐서 그런지 생각보다 간단한 문제였다<br>
문자열을 입력받고 포함되어있는 문자열을 찾아주면 되는것<br>

예를들어 이런것이다<br>

```java

package personal_study;

public class Find {
	public static void main(String[] args) {
		
		String fruit = "딸기 사과 수박 바나나 메론 복숭아";
		
		if (fruit.contains("바나나")) {
			System.out.println("contains() : 포함");
		}else {
			System.out.println("contains() : 포함");
		}
	}
}
```
위 결과는 contains() : 포함을 출력한다<br>

- contains() : 이 메소드는 String 값에서 포함되어 있는 값을 확인하여<br>
               boolean 값을 반환해준다<br>


내가 직접 구현해본 코드는 다음과 같다<br>

- Books 클래스 설계도면에 필요한 아이템만들기

```java
package example0729;

public class Books {
	String name;       // 책 이름
	String publishing; // 출판사
	String location;   // 위치
	boolean check;     // 대여여부
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getPublishing() {
		return publishing;
	}
	public void setPublishing(String publishing) {
		this.publishing = publishing;
	}
	public String getLocation() {
		return location;
	}
	public void setLocation(String location) {
		this.location = location;
	}
	public boolean isCheck() {
		return check;
	}
	public void setCheck(boolean check) {
		this.check = check;
	}
}
```

- Library 클래스 - 아이템 초기화 및 검색하는 동작

```java
package example0729;

public class Library {
	
	Books []  b_items;
	
	public void initBooks() {
		// Flower [] items = new Flower[5];
		b_items = new Books [8];
		for (int i=0; i< b_items.length; i++) {
			b_items[i] = new Books();
			switch (i) {
			case 0:
				b_items[i].setName("자바바이블");
				b_items[i].setPublishing("한빛아카데미");
				b_items[i].setLocation("A-15");
				b_items[i].setCheck(false);
				break;
			case 1:
				b_items[i].setName("자바의정석");
				b_items[i].setPublishing("도우출판사");
				b_items[i].setLocation("A-10");
				b_items[i].setCheck(true);
				break;
			case 2:
				b_items[i].setName("점프 투 자바");
				b_items[i].setPublishing("이지스 퍼블리싱");
				b_items[i].setLocation("A-9");
				b_items[i].setCheck(true);
				break;
			case 3:
				b_items[i].setName("어서와 Java는 처음이지!");
				b_items[i].setPublishing("인피니티북스");
				b_items[i].setLocation("A-15");
				b_items[i].setCheck(false);
				break;
			case 4:
				b_items[i].setName("PHP & Mysql");
				b_items[i].setPublishing("인피니티북스");
				b_items[i].setLocation("B-25");
				b_items[i].setCheck(true);
				break;
			case 5:
				b_items[i].setName("점프 투 파이썬");
				b_items[i].setPublishing("한빛아카데미");
				b_items[i].setLocation("B-2");
				b_items[i].setCheck(true);
				break;
			case 6:
				b_items[i].setName("점프 투 장고");
				b_items[i].setPublishing("이지스 퍼블리싱");
				b_items[i].setLocation("B-8");
				b_items[i].setCheck(false);
				break;
			case 7:
				b_items[i].setName("C언어본색[열혈강의]");
				b_items[i].setPublishing("프리렉");
				b_items[i].setLocation("B-13");
				b_items[i].setCheck(true);
				break;	
			}
			
		}
	}

	public void getFindBooks(String books) {
		String res = "";
		
		for (int i=0; i<b_items.length; i++) {
			if (b_items[i].getName().contains(books)) {
				if (!b_items[i].isCheck()){
					res = "대여중";
				}else {
					res = "대여가능";
				}
				System.out.println(b_items[i].getName() + " | " + b_items[i].getPublishing()
						+ " | "+ b_items[i].getLocation() + " | " + res);
		}// end of for loop(1)
		
		}
	}
}
```

- Main - 프로그램 실행

```java
package example0729;

import java.util.Scanner;

public class Main {
	
	public static void main(String[] args) {
		Library library = new Library();
		Scanner scan = new Scanner(System.in);
		library.initBooks();
		
		System.out.print("도서명 검색 :");
		String find = scan.next();
			
		library.getFindBooks(find);	
	}
}
```

문제대로 출력은 잘 나왔지만 강사님의 로직을 보면 내가 놓치거나 생각하지 못한 부분을<br>
확인할 수 있었다 문자열 편집에 따른 메모리의 효율성을 위한 StringBuffer클래스 !<br>


내가 생각한 로직<br>

```java
for (int i=0; i<b_items.length; i++) {
			if (b_items[i].getName().contains(books)) {
				if (!b_items[i].isCheck()){
					res = "대여중";
				}else {
					res = "대여가능";
				}
				System.out.println(b_items[i].getName() + " | " + b_items[i].getPublishing()
						+ " | "+ b_items[i].getLocation() + " | " + res);
		}// end of for loop(1)
```

강사님 버전<br>
```java
for(int i=0; i<ar.length; i++) {
			//배열로 부터 책객체 하나를 얻어낸다.
			Book b = ar[i];
			
			if(b.getName().contains(n)) {
				sb.append(b.getName());
				sb.append("|");
				sb.append(b.getPress());
				sb.append("|");
				sb.append(b.getPos());
				sb.append("|");
				if(b.isRent())
					sb.append("대여중");
				else
					sb.append("대여가능");
				sb.append("\n");
			}
		}//for문의 끝
		return sb.toString();
```

그리고 인자로 단어를 받아 검색하는 메소드의 반환값은 개발자가 정한다고 말씀해주셨다<br>
즉 정해진 건 아니기 때문에 너무 복잡하게 생각하지 말고 반환값이 필요하다면<br>
반환값을 정해주는거고 안해도 된다고 판단되면 안하는 거고 즉 상황에 따라서 달라질 수 있다<br>

자판기 프로그램과 도서관 프로그램을 간단하게 만들어봤는데 오늘 객체지향을 배워보면서<br>
그동안 어렵게 생각했었던 것을 조금씩 걸어가고 있다는 느낌을 받아 슬슬 재미가 붙여지기 시작했다<br>