---
title:  자바기반의 응용SW개발자 양성과정 18일차
author: Kim
date: 2021-07-30 06:00:00 +0900
categories : [Increpas]
tags: [Increpas]
---

# 오전시간

-  클래스   : 객체를 정의하는 설계도면
-  객체     : Heap 영역에 가르키는 주소값
-  참조변수 : 객체를 참조하는 변수를 의미함

has_a 관계<br>

다음주 : 상속 추상화 인터페이스<br>

다음은 학생관리 프로그램을 만든다<br>

- StudentVO - 아이템만들기

```java
package am;

public class StudentVO{
	
	String number; // 학번
	String name;   // 이름
	MajorVO mvo;
	
	public String getNumber() {
		return number;
	}
	public void setNumber(String number) {
		this.number = number;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
		
	public MajorVO getMvo() {
		return mvo;
	}
	public void setMvo(MajorVO mvo) {
		this.mvo = mvo;
	}
}
```

- MajorVO - 전공 + 학과장 ? 아이템

```java
package am;

public class MajorVO {
	
	// 전공 클래스
	
	String title;  
	String manager;
	
	public String getTitle() {
		return title;
	}
	public void setTitle(String title) {
		this.title = title;
	}
	
	public String getManager() {
		return manager;
	}
	public void setManager(String manager) {
		this.manager = manager;
	}
}
```

- Main - 프로그램 시작

```java
package am;

import java.util.Scanner;

public class Main {
	
	StudentVO [] person;
	
	// 배열을 초기화 동작 (전공 : 컴퓨터공학 , 물리학과 , 실용음악)
	public void initStudentVO() {
		person = new StudentVO[1];
	
		for (int i=0; i<person.length; i++) {
			person[i] = new StudentVO();
			// StudentVO 내부에 있는 mvo에 저장해줄
			// MajorVO객체의 주소를 준비한다
			MajorVO mvo = new MajorVO();
			person[i].setMvo(mvo);
			
			switch (i) {
			case 0:
				person[i].setNumber("21");
				person[i].setName("Kim");
				person[i].getMvo().setTitle("컴퓨터전공");
				person[i].getMvo().setTitle("컴퓨터");
				person[i].getMvo().setManager("알수없음");
				break;
			}
		}
	}// end of initStudentVO()
	
	// 이름으로 검색하여 학생정보를 화면에 출력하는동작 만들기
	
	public String getSearch(String name) {
		StringBuffer sb = new StringBuffer();
		for (int i=0; i<person.length; i++) {
			
			StudentVO search = new StudentVO();
			search = person[i];
		
			if (search.getName().contains(name)) {
				sb.append("이름 : ");
				sb.append(search.getName());
				sb.append("\n");
				sb.append("학번 : ");
				sb.append(search.getNumber());
				sb.append("\n");
				sb.append("전공 : ");
				sb.append(search.getMvo().getTitle());
				sb.append("\n");
				sb.append("학과장 : ");
				sb.append(search.getMvo().getManager());
			}
			// end of if-else
		}// end of for loop(1)
		return sb.toString();
	} 
	
	public static void main(String[] args) {
		
		Main main = new Main();
		main.initStudentVO();
		Scanner scan = new Scanner(System.in);
		String find = scan.next();
		
		String res = main.getSearch(find);
		System.out.println(res);	
	}
}
```

※ 이번에는 Main에서 간략하게 테스트를 진행해보았다<br>

# 오후시간

- 생성자

생성자는 new 연산자를 통해 객체를 생성할 때 반드시 호출이 되고<br>
생성자는 멤버 변수를 초기화하는 역할을 한다.<br>

person[i] = new StudentVO(); 이것 역시 생성자를 호출한 것이다<br>

기본생성자 구성은 다음과 같다<br>

```java
public 클래스명 () {}
```

사실 생성자는 우리가 직접 구현하지않아도 컴파일러가 알아서 기본생성자를<br>
정의하도록 되어있다고 했다 학생관리 프로그램 구현중 조금 귀찮은 부분이 있다<br>

```java
for (int i=0; i<person.length; i++) {
			person[i] = new StudentVO();
			// StudentVO 내부에 있는 mvo에 저장해줄
			// MajorVO객체의 주소를 준비한다
			MajorVO mvo = new MajorVO();
			person[i].setMvo(mvo);
}
```

바로 이 부분이다 나한테는 가독성도 별로 안좋고 헷갈리게 할 만한 코드였다<br>

위 와 같은 코드를 작성하지 않기위해선 StudentVO 클래스에서 다음과 같이 작업한다<br>

```java
public StudentVO() {
    // StudentVO() 객체가 생성될 때 MajorVO() 객체도 같이 생성된다
    mvo = new MajorVO();
}
```

기본생성자를 내가 직접 만들고 안에는 MajorVO() 생성자를 만들어주는 것이다<br>
이렇게보면 StudentVO() 클래스에 MajorVO() 주소값이 들어 가 있겠구나 라는걸<br>
쉽게 알아볼 수 있을 것 같다<br>

```java
for (int i=0; i<person.length; i++) {
			person[i] = new StudentVO();
}
```
for문으로 객체화 시키는 작업 역시 가독성면에도 좋다고 생각되고<br>
앞으로도 2개이상의 VO를 초기화 시켜야 할 일이있다면 생성자를 만들어서<br>
아까같은 방법으로 초기화를 하는 방법을 쓸 것같다<br>
