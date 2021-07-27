---
title:  getter & setter 정리
author: Kim
date: 2021-07-27 06:05:00 +0900
categories : [Java]
tags: [Java]
pin: true
---

# getter & setter

클래스의 특성중 정보 은닉을 가장 잘 보여줄 수 있는 메소드를 의미합니다<br>

보통 클래스의 멤버변수는 private로 접근제한자를 설정합니다<br>
private 제한자 특성상 자신 클래스 안에서만 사용하고 외부클래스에서는 허용되지 않지만<br>
getter / setter 를 통해 멤버변수 의 값을 변경 후 호출 하게 할 수 있습니다<br>

- PersonInfo 클래스

```java
package personal_study;

public class PersonInfo {
	
    // 멤버변수 선언 private 제한자로 
    // 현재 클래스에서만 접근 할 수 있다
	private String name;
	private String email;
	private int age;

    // 멤버변수에 값을 넣는 메소드 
	public void setName(String name) {
		this.name = name;
	}
    // "" 값을 읽어오는 메소드
	public String getName() {
		return name;
	}
	
	public void setEmail(String email) {
		this.email = email;
	}
	public String getEmail() {
		return email;
	}
	
	public void setAge(int age) {
		this.age = age;
	}
	public int getAge() {
		return age;
	}
}
```

- PersonMain 클래스

```java
package personal_study;

public class PersonMain {
	
	public static void main(String[] args) {
		
		PersonInfo info = new PersonInfo();
		
		info.setName("Kim");
		info.setEmail("kkkkkk@gmail.com");
		info.setAge(27);
		
		String name = info.getName();
		System.out.println("name : " + name);
		
		String email = info.getEmail();
		System.out.println("email : " + email);
		
		int age = info.getAge();
		System.out.println("age : " + age);
		
	}
}
출력

name : Kim
email : kkkkkk@gmail.com
age : 27
```

## getter 와 setter 왜 필요할까?

객체의 데이터는 객체 외부에서 직접적으로 접근하는 것을 막는것을 막을 수 있습니다<br>
데이터를 외부에서 읽고 변경 시 객체의 무결성이 꺠질 수 있기 때문에<br>

객체 지향 프로그래밍 에서는 메소드를 통해 데이터를 변경하는 방법을 좀 더 <br>
선호하다는 걸 볼 수 있습니다<br>

- Setter

Setter는 데이터가 외부에서 접근하지 않도록 막고 메소드만 공개하며<br>
외부에서 메소드만을 통해 데이터에 접근하도록 유도할 수 있는 기술방식 입니다<br>

- Getter

Getter는 메소드로 필드값을 가공 후 외부로 전달하는 기술방식 입니다<br>

※ 클래스를 선언할 때 필드를 private로 선언하여 은닉 후 외부로부터 보호한 후<br>
  필드에 대한 getter / setter 메소드를 작성하여 필드값을 안전하게 변경하는 것이 좋습니다<br>

※ Getter / Setter 메소드를 사용하는 이유는 필드 값에 부적절한 값이 대입되는 것을 막기위한 것<br>

※ 정보 은닉의 특성을 고려한 방식이며 클래스의 멤버 변수를 private 제한자로 구현 후<br>
  Getter / Setter 메소드를 통해 처리하도록 구현하는 것이 좋다<br>