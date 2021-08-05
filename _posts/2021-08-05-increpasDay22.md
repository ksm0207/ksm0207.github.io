---
title:  자바기반의 응용SW개발자 양성과정 22일차 - Static , 상수 , 추상화
author: Kim
date: 2021-08-05 06:00:00 +0900
categories : [Increpas]
tags: [Increpas]
---


# 오전수업

Static에 대해서 알아보자 <br>

기본적으로 클래스의 변수들은 인스턴스 변수 , 인스턴스 메소드 등이 있다<br>

- 인스턴스 변수 : 클래스의 멤버변수와 같은 의미를 가지고 있다

```java
String str = "대한민국";
int a
```

- 인스턴스 메소드 : 클래스의 멤버메소드와 같은 의미를 가지고 있다

```java
public print() {
    System.out.println("String str : " + str);
    System.out.println("int a : " + a); 
}
```

변수 왼쪽 부분에 Static 이라고 붙어있는 인스턴스 변수들을 의미한다<br>
Static이 붙는 순간 이들은 더이상 인스턴스 쪽에 해당하지 않게된다<br>

```java
// 정적멤버변수 (인스턴스변수 라고 하지 않음 )
	static String msg = "힘내라";
	static int b = 200;
```

Static 으로 변수를 만들 수 있다면 메소드도 Static을 붙일 수 있지 않을까?<br>
정답은 만들 수 있지만 메소드 역시 Static을 붙여줘야 한다<br>
만약에 일반 인스턴스 멤버 변수를 출력하려고 하면 아래 코드에 보이는 것 같이<br>
에러를 발생시키는 부분을 주석처리된 부분을 확인 해 주도록하자<br>

```java
// 	정적멤버메소드 <==> 멤버변수는 들어올 수 없음
	public static void staticPrint() {
		System.out.println("Static msg : " + msg);
		System.out.println("Static b : " + b);
//		System.out.println("Static str" + str);
// 		Error : 정적 필드가 아닌 필드 str을 정적 참조할 수 없습니다.
	}
```
인스턴스 변수 str은 Static 영역에 들어올 수 없다 정도로 이해할 수 있다<br>
Error 라고 주석처리한 내용은 System.out.println("Static str" + str); 이 부분에서<br>
에러내용을 구글링으로 번역한 내용이다<br>

Static은 뭔가 특별한 영역인 것 같았다 인스턴스 변수나 메소드는 객체를 생성해야만<br>
사용할 수 있었는데 이건 객체 생성과 다르게 직접 호출이 가능하다는 점을 알았다<br>

- Class Ex1_Main

```java
package am;

public class Ex1_Main {

	public static void main(String[] args) {
		
// 		Static 선언된 멤버변수나 메소드 들이 있다
// 		해당 객체를 생성하지 않고도 직접 호출이 가능하다
		System.out.println(Ex1_Static.msg);
		System.out.println(Ex1_Static.b);
		Ex1_Static.staticPrint();
		
		System.out.println("=======================");
		
//		static으로 선언되지 않은 멤버들은 객체를 생성 후 사용한다
//		레퍼런스 변수로 Static 을 호출하는 것은 바람직하지 않음		
		Ex1_Static ex1 = new Ex1_Static();
		Ex1_Static ex2 = new Ex1_Static();
		Ex1_Static ex3 = new Ex1_Static();
		
		ex2.a = 1300;
		System.out.println("Ex1 객체 : " +ex1.a); // 100
		System.out.println("Ex2 객체 : "+ ex2.a); // 1300

//      정적 필드 Ex1_Static.b는 정적 방법으로 액세스해야 합니다.		
		ex2.b = 2500;
		System.out.println("Ex1.value2 : " + ex1.b);

		System.out.println("Ex1_Static.b : " + Ex1_Static.b);
		
		System.out.println("==============================");
		
		System.out.println(ex3.b);
	}
}
```
위 코드에서 주의깊게 본것은 바로 이 부분이다<br>

```java
// 정적 필드 Ex1_Static.b는 정적 방법으로 액세스해야 합니다.		
ex2.b = 2500;
System.out.println("Ex1.value2 : " + ex1.b);

System.out.println("Ex1_Static.b : " + Ex1_Static.b);
```

객체생성을 하고나서 레퍼런스 변수 ex2 가 Static 변수 값을 강제로 바꿔놓으면<br>
값이 바꿔지게 되고 A 객체 B 객체 둘다 2500이라는 값을 참조하게 된다는 것 이다<br>

즉 Static 으로 설정된 값은 `공유` 할 수 있다는 것을 알게되었다<br>
실제 System.out.println("Ex1.value2 : " + ex1.b); 이 부분에서 노란줄로 표시하길래<br>

궁금해서 마우스를 대보면 정적 필드 Ex1_Static.b는 정적 방법으로 액세스 하라는<br>
권장하는 메세지를 볼 수 있다 저렇게 사용은 가능하지만 올바른 방법으로 사용해라<br>
이런 뜻 인 것 같았다<br>

Ex2 객체를 B 객체라고 가정해보면 다음 레퍼런스 변수가 Static 값을 변경하면<br>
```java
ex2.b = 2500;
```

Ex3 객체를 C라고 하자 이 객체 역시 2500 이라는 값을 할당받고 있다<br>
정리하면 Static 변수는 공유되는 개념이다<br>

```java
Ex1_Static ex3 = new Ex1_Static();
System.out.println(ex3.b);
```
## 메소드 우선도 호출

Static 멤버 메소드와 일반 인스턴스 메소드의 호출 순위는 Static으로 정의된것이 더<br>
빠르다는 것을 알게되었다 다음 예제를 보도록 하자<br>

- Class Ex2_Static

아래 코드는 메소드의 우선 호출순위를 알아보기위한 코드다<br>

먼저 생성자 와 Static 메소드를 만들어 주었다<br>
```java
package am;

public class Ex2_Static {
	
	String msg = "Test";
	
	static int su1 = getValue();
	static int su2 = 10;
	
	// 생성자 , 생성하려 할때 호출
	public Ex2_Static() {
		System.out.println("Ex2_Static 생성자 호출");
	}
	// 호출 우선도가 제일 높다
	public static int getValue() {
		System.out.println("getValue()");
		return 100;
	}
}
```

- Class Ex2_Main

다음 Main을 실행하여 출력해주었다<br>

```java
package am;

public class Ex2_Main {

	public static void main(String[] args) {
		
		Ex2_Static st1 = new Ex2_Static();	
	}
}
```
결과는 다음 과 같다<br>

```java
getValue()
Ex2_Static 생성자 호출
```
이렇게 Static 으로 붙은 정적멤버메소드가 더 우선순위로 호출한다는 것을 알았다<br>

# 상수

상수는 짧게나마 개념을 익혀봤는데 상수를 만드는 방법은 다음 문법으로 작성할 수 있다<br>

- static final 자료형 lalala;

상수로 정의된 값은 프로그램이 종료될 때 까지 `절대 변하지 않는 값` 이라고만 알아두었다<br>

그럼 상수를 정의해서 사용빈도는 얼마나 될까? 아직 개발을 해보지않아서 잘 모르겠지만<br>
다음 예제를 통해 실제 웹 개발에 들어가면 이런 용도로 사용할 수 있지 않을까하는 생각이 든다<br>

- Class Ex1_Final

먼저 상수를 정의한 클래스는 다음과 같다<br>

```java
package pm.Ex1;

public class Ex1_Final {
	
	// 인스턴스 변수 선언
	int value = 100;
	
	// 인스턴스 상수 선언
//	final int VALUE1 = 1;
	
	// 상수 선언 Static 영역에 올라간다
	static final int ADD = 1;
	static final int SEARCH = 2;
	static final int DELETE = 3;
	static final int TOTAL = 4;
	
	public int getValue() {
		return value;
	}
	
    public void setValue(int value) {
		this.value = value;
	}

	public void exe() {
		if (value == Ex1_Final.ADD) {
			System.out.println("데이터를 추가하였습니다.");
			
		}else if (value == Ex1_Final.SEARCH) {
			System.out.println("검색 결과입니다.");
			
		}else if (value == Ex1_Final.DELETE) {
			System.out.println("데이터를 삭제하였습니다.");
			
		}else if (value == Ex1_Final.TOTAL) {
			System.out.println("전체 리스트 입니다.");
		}
	}
}// end of Final
```

- Class Ex1_Main

Main 클래스에서는 간단하게 1~4까지의 수를 체크하고 입력을 받으면 Final 클래스에서<br>
출력할수 있도록 만들어주었다<br>

```java
package pm.Ex1;

import java.util.Scanner;

public class Ex1_Main {
	
	public static void main(String[] args) {
		
		Scanner scan = new Scanner(System.in);
		Ex1_Final ex1 = new Ex1_Final();
		System.out.println("1 ~ 4 입력");
		int cmd = scan.nextInt();
		
		
		// 입력된 값이 1 ~ 4인지 ?
		if(cmd >= 1 && cmd <= 4) {
			ex1.setValue(cmd);
			ex1.exe();
		}else {
			System.out.println("1 ~ 4 수들 중 하나만 입력해야 합니다.");
		}// end of if-else
	}
}
```
상수를 사용하면 어떤이점이 있는지 좀 더 공부해서 포스팅 해보는 것도 나쁘지 않을 것 같다<br>

# 오후수업

오후수업은 추상화 개념을 짧게 알아보았다<br>


## 추상화

프로그래밍에서 추상화란 개념은 처음 들었을때 애매모호했다.. 이게 무슨말인가 싶었지만<br>

추상화 클래스를 만들면 자식클래스들이 직접구현하는 기술중 하나라고 생각했다<br>

예를들면 다음과 같은 일이 발생했다고 하자<br>
키보드를 만드는 회사에서 A 사장이 개발자 B 와 C 에게 각각 다른 키보드를
만들어 달라는 업무를 받았는데 만들어야 키보드는 다음과같다<br>

- 개발자 B 에게는 `무선 무소음 키보드`

- 개발자 C 에게는 `유선 기계식 키보드`

- 추상클래스 키보드


이렇게 개발자 2명은 `키보드` 를 `상속` 받아 각자 실체화된 클래스에 구현을 시작하는데<br>
정말 다행인건 추상클래스에는 미리 정의한 필드와 메소드를 가지고 있어서<br>
이렇게되면 개발자의 역량대로 키보드를 개발할수 있다는 것이다<br>

하지만 여기서 미리 정의한 필드와 메소드는 단순하게 정의됐다고만 볼수 없다<br>
그 이유는 개발자 B 와 C는 키보드를 상속받아 사용하려는 메소드는 반드시 재정의해야만<br>
사용할 수 있는 하나의 `조건부` 같은 개념이 들어가 있기때문이다<br>

추상화를 나타내는 클래스는 다음과 같다<br>

```java
package Abstract;

abstract class Keyboard {
	
	String keyBoardName;
	
	abstract String getKeyBoardName(); // 추상메소드
}
```

`abstract` 라는 키워드를 나타내고 다음은 개발자 B 와 C 클래스를 만들어보았다<br>
여기서부터 왜 재정의를 해야만 사용가능하고 추상화 클래스를 왜 쓰는지 알수있다<br>

개발자B 클래스에서 Keyboard를 상속받으면 클래스명에 빨간줄 에러가 나오게된다<br>

```java
package Abstract;

public class DeveloperB extends Keyboard {

}
```

빨간색으로 칠한 부분의 에러내용은 다음과 같다<br>

```java
The type DeveloperB must implement the inherited abstract method
Keyboard.getKeyBoardName()
```
DeveloperB 형식은 상속된 추상 메서드 Keyboard.getKeyBoardName()을 구현해야 합니다<br>

그렇다면 바로 getKeyBoardName() 메소드를 만들어주는데 이때 주의해야할 점은<br>
일반적인방법 으로 메소드를 생성하는 것 이 아닌 `오버라이드` 를 해줘야 한다는 것 이다<br>

※ 오버라이드 뜻은 부모클래스의 메소드를 재정의 한다는 의미가 있다<br>

메소드를 재 정의후 에러는 더이상 나오지 않게되고 개발자B는 앞으로 이 메소드를 사용하기만 하면된다<br>

```java
package Abstract;

public class DeveloperB extends Keyboard {

	@Override
	String getKeyBoardName() {
		// TODO Auto-generated method stub
		return null;
	}
}
```

개발자 C도 마찬가지다 부모클래스를 상속받아 메소드를 재정의하여 사용한다<br>

```java
package Abstract;

public class DeveloperC extends Keyboard{

	@Override
	String getKeyBoardName() {
		// TODO Auto-generated method stub
		return null;
	}
}
```

여기서 추상화 클래스를 사용하게되면 공통적으로 사용했던것은 무엇일까?<br>
바로 개발자 B 와 C가 `공통적인 메소드` 이름으로 작업을 임했다는 것 이다<br>
이렇게되면  공통작업으로 인해 통일성이 이루어질 수 있고<br>
유지보수성을 높일 수 있는 장점을 가질 수 있을거라고 생각한다<br>

## 추상클래스는 객체화가 될 수없다

실체 클래스는 실제 객체를 생성할 정도의 구체성을 가지는게 늘 해왔던 그것이지만<br>

추상클래스가 객체가 될 수 없는 이유는 미완성적 메소드를 포함하고 있어서 그렇다.<br>
메소드의 구현부가 없고 구체적이지 않기 때문이라고 생각하면 될 것 같다<br>

예를들면 다음과같다<br>

```java
abstract String getKeyBoardName(); // 추상메소드
```
딱 봐도 애매모호한 부분때문에 컴파일러 입장에서는 되게 난감해 할 것 같다는 생각이 든다<br>
클래스를 만들고 영역에 올려야하는데 저게뭐지.. 라고 하지않을까?<br>

