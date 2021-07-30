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


