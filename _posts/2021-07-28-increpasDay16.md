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