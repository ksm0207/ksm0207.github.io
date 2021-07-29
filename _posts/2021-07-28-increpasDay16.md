---
title:  자바기반의 응용SW개발자 양성과정 16일차 - 
author: Kim
date: 2021-07-27 06:00:00 +0900
categories : [Increpas]
tags: [Increpas]
---

# 오전시간

오늘도 이어서 클래스 개념을 배워보도록 하자<br>

## 집을 만드는 클래스

- (1) Ex1_House 

```java
package am;

public class Ex1_House {
	
	int floor;   //  (방의) 바닥
	int room ;   //  방 개수
	int balcony; //  발코니
	int restroom; // 화장실
	
	String direction; // 방향

	public int getFloor() {
		return floor;
	}

	public void setFloor(int floor) {
		this.floor = floor;
	}

	public int getRoom() {
		return room;
	}

	public void setRoom(int room) {
		this.room = room;
	}

	public int getBalcony() {
		return balcony;
	}

	public void setBalcony(int balcony) {
		this.balcony = balcony;
	}

	public int getRestroom() {
		return restroom;
	}

	public void setRestroom(int restroom) {
		this.restroom = restroom;
	}

	public String getDirection() {
		return direction;
	}

	public void setDirection(String direction) {
		this.direction = direction;
	}
}
```

Getter & Setter 을 이용해서 메소드를 만들어 주었는데 this 키워드를 주목해야 한다<br>
this : 현재 객체를 의미한다 여기서 객체란 생성한 클래스를 의미한다<br>

※ 쉽게 정리하면 현재 객체의 주소를 의미한다<br>
※ this. 속성 / 동작 > 변수 와 메소드에 접근할 수 있다<br>
※ 객체의 속성과 동작들을 한마디로 줄여 멤버라고 칭한다<br>


다음은 Main 클래스에서 직접 집을 구현해보도록 하였다<br>
```java
package am;

public class Ex1_Main {
	
	public static void main(String[] args) {
		
		Ex1_House house = new Ex1_House();
		
		house.setFloor(2);
		house.setRoom(5);
		house.setRestroom(2);
		house.setBalcony(1);
		house.setDirection("동향");
		
		Ex1_House house2 = new Ex1_House();
		
		house.setFloor(1);
		house.setRoom(6);
		house.setRestroom(3);
		house.setBalcony(2);
		house.setDirection("남향");

		System.out.println(house.hashCode()); // 1521118594
		System.out.println(house2.hashCode()); // 1940030785
	}
}
```

house 객체 말고도 새로운 house2 객체를 만들었는데 이 둘의 차이점은 주소값이 다르고<br>
객체변수는 서로 공유하지 않는다는것을 알고있어서 hashCode() 메소드를 사용해서<br>
확인 해 봤는데 역시 내 예상대로 맞았다.<br>

그림으로 표현하면 다음과 같다<br>
※ 밥먹구와서 하기<br>

## 컵 객체를 만들어보자

- 속성 정의

```java
package am;

public class Cup {
	
	String cupTypes;      // 컵 타입
	String color; //         컵 색상
	String cupMaterial;   // 컵 재질
	int cupCapacity;      // 컵 용량
	
	
	public String getCupMaterial() {
		return cupMaterial;
	}
	public void setCupMaterial(String cupMaterial) {
		this.cupMaterial = cupMaterial;
	}
	public String getCupTypes() {
		return cupTypes;
	}
	public void setCupTypes(String cupTypes) {
		this.cupTypes = cupTypes;
	}
	public int getCupCapacity() {
		return cupCapacity;
	}
	public void setCupCapacity(int cupCapacity) {
		this.cupCapacity = cupCapacity;
	}
	public String getColor() {
		return color;
	}
	public void setColor(String color) {
		this.color = color;
	}
}
```

- 객체 생성

```java
package am;

public class CupMain {
	
	public static void main(String[] args) {
		
		Cup cup1 = new Cup();
		
		cup1.setCupTypes("머그컵");
		cup1.setColor("그린");
		cup1.setCupCapacity(250);
		cup1.setCupMaterial("유리");
		
		
		System.out.println("========================");
		System.out.println("타입 : "+cup1.getCupTypes());
		System.out.println("색상 : "+cup1.getColor());
		System.out.println("용량 : "+cup1.getCupCapacity() +"ml");
		System.out.println("재질 : "+cup1.getCupMaterial());
		System.out.println("========================");
		Cup cup2 = new Cup();
		
		cup2.setCupTypes("맥주잔");
		cup2.setColor("투명색");
		cup2.setCupCapacity(500);
		cup2.setCupMaterial("유리");
		
		System.out.println("타입 : "+cup2.getCupTypes());
		System.out.println("색상 : "+cup2.getColor());
		System.out.println("용량 : "+cup2.getCupCapacity() + "cc");
		System.out.println("재질 : "+cup2.getCupMaterial());
		System.out.println("========================");
		
		Cup cup3 = new Cup();
		
		cup3.setCupTypes("텀블러");
		cup3.setColor("블랙");
		cup3.setCupCapacity(345);
		cup3.setCupMaterial("스테인리스 스틸");
		
		System.out.println("타입 : "+cup3.getCupTypes());
		System.out.println("색상 : "+cup3.getColor());
		System.out.println("용량 : "+cup3.getCupCapacity() + "ml");
		System.out.println("재질 : "+cup3.getCupMaterial());
		System.out.println("========================");
	}
}
```
cup1 ~ cup3은 서로 주소값이 다르다는걸 잊지말자<br>
출력결과는 다음과같다<br>
```java
========================
타입 : 머그컵
색상 : 그린
용량 : 250ml
재질 : 유리
========================
타입 : 맥주잔
색상 : 투명색
용량 : 500cc
재질 : 유리
========================
타입 : 텀블러
색상 : 블랙
용량 : 345ml
재질 : 스테인리스 스틸
========================
```

# 오후시간

## 자판기 만들기

오후에는 문제를 제시한 자판기를 만들어보는 시간을 가져봤다<br>

여기서 내가 궁금했던것이 있었는데 바로 아래 사진부분을 의미한다<br>
<img src ="/post/Java/img.png"><br>

나는 총 MoneyCheck 와 ReturnMoney ... 네이밍 센스가 좀 없는 것 같긴하다..<br>
본 목적은 클래스를 2개를 만들어서 나눠서 분리해보는 연습을 아직 가져보지않아서 작성을해봤는데<br>

저렇게 객체를 전역으로 세워두면 괜찮을까 궁금했던 찰나에 강사님께서는 객체가 존재하는동안<br>
정확한 값들을 저장하고 사용되어야 한다는 것이 주의점이 된다고하셔다<br>

Menu 객체 같은경우 자판기의 아이템들이 존재하고 객체가 없어지기 전까지 항상 정확하고<br>
예상해볼 수 있는 값들을 저장하도록 설계된 것 이라고 말씀해주셨다 즉 확실한 정보들만<br>
정의해두는 것이 좋다는 것이다<br>

직접 한번 만들어본 자판기 소스는 다음과같다<br>

- Menu 클래스 - 자판기 아이템

```java
package example;

public class Menu {
	
	String  menu;
	String returnMoney;
	int price;
	
	public String getMenu() {
		return menu;
	}
	public void setMenu(String menu) {
		this.menu = menu;
	}
	
	public int getPrice() {
		return price;
	}
	public void setPrice(int price) {
		this.price = price;
	}
	
	public String getReturnMoney() {
		return returnMoney;
	}
	public void setReturnMoney(String returnMoney) {
		this.returnMoney = returnMoney;
	}
}
```

- VendingMachine 클래스 - 메인실행

```java
package example;

import java.util.Scanner;

public class VendingMachine{
	public static void main(String[] args) {
		
		// 자판기 객체
		VendingMachine vm = new VendingMachine();
		// 입력 객체
		Scanner scan = new Scanner(System.in);
		// 금액 확인 체크 후 아이템 반환 하는 메소드
		MoneyCheck money_check = new MoneyCheck();
		// 전액 반환 해주는 메소드
		ReturnMoney rt_money = new ReturnMoney();
		
		// 메뉴 호출
		Menu [] menu = vm.start();
		
		int userMoney = 0;
		System.out.println("무엇을 주문하시겠습니까 ?");
		System.out.print("주문 번호 : ");
		while(true){
			try {
				int userChoies = scan.nextInt() -1;
				if (userMoney == 0) {
					System.out.println("선택한 메뉴 : " + menu[userChoies].getMenu());
					System.out.println("필요한 금액 : " + menu[userChoies].getPrice());
					
					System.out.println("금액을 충전해주세요.");
					userMoney = scan.nextInt();
					userMoney = money_check.checkItems(userMoney, userChoies, menu);
				}
				System.out.println("현재 가지고 있는 금액은 " + userMoney + " 원 입니다");
				
				if(userMoney > 0)
					System.out.println("전액 반환 을 하시려면 5번을 눌러주세요");
					userChoies = scan.nextInt();		
					rt_money.returnChangeMoney(userMoney);
					
			}catch (Exception e) {
					System.out.println("다시 입력해주세요.");
					scan = new Scanner(System.in);
			}
		}
	}
	public Menu[] start() {
		
		Menu[] menu = new Menu[4];
		System.out.println("자판기 테스트 !! ");
		for (int i = 0 ; i < menu.length ; i ++) {
			menu[i] = new Menu();
			
			switch (i) {
			case 0:
				menu[i].setMenu("레쓰비");
				menu[i].setPrice(600);
				break;
			case 1:
				menu[i].setMenu("사이다");
				menu[i].setPrice(700);
				break;
			case 2:
				menu[i].setMenu("콜라");
				menu[i].setPrice(700);
				break;
			case 3:
				menu[i].setMenu("게토레이");
				menu[i].setPrice(900);
				break;
			}
			System.out.println( (i+1) +"." +menu[i].getMenu() + "  " +  menu[i].getPrice());
		} // end of for(1)
		return menu;
	}
}	
```

- MoneyCheck 클래스 - 아이템 구매 및 금액 체크

```java
package example;

import java.util.Scanner;

public class MoneyCheck {
	
	// 금액 확인 후 아이템 반환 메소드
	public int checkItems(int money , int userChoies , Menu[] menu) {
		
		Scanner scan = new Scanner(System.in);
		
		if ((money - menu[userChoies].getPrice()) >= 0) {
			money = money - menu[userChoies].getPrice();
			System.out.println("주문하신 " + menu[userChoies].getMenu() + " 나왔습니다 감사합니다 !");
		}else {
			System.out.println("잔액이 부족합니다");
			System.out.println("부족한 금액을 채워주세요 :");
			money += scan.nextInt();
			money = money - menu[userChoies].getPrice();
			System.out.println("주문하신 " + menu[userChoies].getMenu() + " 나왔습니다 감사합니다.");
		} 
		return money;
	}
}
```

- ReturnMoney 클래스 - 금액 반환하기

```java
package example;

public class ReturnMoney {
	
	
	// 전액 반환 메소드
	public int returnChangeMoney(int u_money) {
		
		int [] money = {10000,5000,1000,500,100,50,10};
		int remainMoney = 0;
		
		if (u_money == 0) {
			System.out.println("반환하실 금액이 없습니다.");
		}else {
			for (int i=0 ; i <money.length; i ++) {
				
				if (u_money / money[i] > 0) {
					System.out.println(money[i] + "원 " + u_money/money[i] + "개 반환하였습니다.");
					u_money %=money[i];
				}
			}// end of for
			System.out.println("자판기에 남은 돈 : " + remainMoney);
		}
		return u_money;
	}
}
```
