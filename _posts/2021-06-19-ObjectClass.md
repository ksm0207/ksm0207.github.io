---
title: Object 클래스
author: Kim
date: 2021-06-19 15:09:00 +0900
categories : [Java]
tags: [Java]
---

## Object

모든 클래스의 조상인 Object 클래스에 대해서 알아보겠습니다.<br>
도움받은 사이트 : <a href ="https://opentutorials.org/course/1223/6241">생활코딩 Object 클래스</a>

먼저 자바에서 상속이란 것은 필수적 이라고 합니다 우리가 상속을 하든 안하든<br>
기본적인 상속을 하게 된다고 하였는데요<br>

예를들어 이런 코드가 있다고 가정해보겠습니다<br>

```java
package org.opentutorials.javatutorials.progenitor;
 
class O {}
```

위 코드는 아래 코드와 같습니다<br>
```java
package org.opentutorials.javatutorials.progenitor;
 
class O extends Object {}
```
자바에서 모든 클래스는 ```Object``` 를 암시적으로 상속받고 있다고 하는데 그런 점에서<br>
```Object는 모든 클래스의 조상```이라고 할 수 있습니다 이렇게 된 이유는 모든 클래스는<br>
공통으로 포함하고 있어야 하는 기능을 제공하기 위해서 입니다<br>

그렇다면 공통으로 제공하는 기능은 무엇이 있을까요? 자바 API 문서를 통해 알아보았습니다<br>
<a href="https://docs.oracle.com/javase/7/docs/api/java/lang/Object.html">Java API</a>

```java
java.lang
Class Object (클래스 개체)
java.lang.Object

public class Object (공용 클래스 개체)
Class Object is the root of the class hierarchy. Every class has Object as a superclass. All objects, including arrays, implement the methods of this class.

클래스 Object는 클래스 계층 구조의 루트이고 모든 클래스에는 Object 수퍼 클래스가 있습니다
배열을 포함한 모든 객체는 이 클래스의 메소드를 구현합니다.
```

```java

[수정 및 유형]          [방법 및 설명]

(1) protected Object || clone()
                          이 개체의 복사본을 만들 수 있고 반환합니다.

(2) boolean          || equals(Object obj)
                          다른 개체가 이 개체와 같은 지 여부를 나타냅니다

(3) protected void   || finalize()
                          개체에 대한 참조가 더 이상 없다고 판단 할 때 개체의 가비지
                          수집기에 의해 호출됩니다

(4) Class<?>         || getClass()
                          런타임 클래스를 반환합니다 (Object) 

(5) int              || hashCode()
                          객체의 해시 코드 값을 반환합니다.

(6) void             || notify()
                          이 개체의 모니터에서 대기중인 단일 스레드를 깨운다.

(7) void             || notifyAll()
                          위와 비슷한 개요지만 모든 스레드를 깨워준다  

(8) String           || toString()
                         객체의 문자열 표현을 반환합니다.

(9 ~ 11 : void)      || wait()
                         다른 스레드가 이 개체에 대한 notify() 혹은 notifyAll() 메소드를
                         호출할 때 까지 현재 스레드는 대기하도록 합니다.
                         
                        wait(long timeout)
                         다른 스레드가 이 개체에 대한 notify() 또는 notifyAll()메소드를
                         호출 하거나 지정된 시간이 경과 할 때까지 현제 스레드는 대기합니다

                        wait(long timeout , int nanos)
                         다른 스레드가 현재 스레드를 중단하거나 일정량의 실시간이 경과 할
                         때 까지 현제 스레드가 대기하도록 합니다.  
```
※ (01) ~ (11) 까지의 내용들은 Object 클래스가 가지고 있는 메소드 입니다 <br>
```자바의 객체는 위 메소드들을 반드시 가지고 있다고 할 수 있음!```<br>

※ (3) finalize() 설명에서 ``` 가비지 ``` 라는 것을 찾아보았는데 메모리 관리 기법 중의 하나로<br>
프로그램이 동적으로 할당했던 메모리 영역 중에서 필요없게 된 영역을 해체하는 기능을 뜻 합니다<br>

* 쓰레기 수집은 동적 할당된 메모리 영역 가운데 더 이상 사용할 수 없게 된 영역을 탐지하여<br>
  자동으로 해제하는 기법 , 더이상 사용할 수 없게 된 영역이란 말은<br>
  어떤 변수도 가리키지 않게 된 영역을 의미함.

* 자바 C# 일부 스크립트 언어들은 처음부터 쓰레기 수집 기법을 염두에 두고 설계되어 있다고함!<br>
  ★ 포스팅 해볼 것

## toString

자바에서는 특별한 메소드를 취급하는 것이 있는데 바로 ```toString()``` 메소드 가 있습니다<br>

* ```toString()``` 객체를 문자로 표현하는 데 있어서 사용하는 메소드

```java
package ObjectExample;

public class toStringTest {
	
	int x , y;
	
	public void toReceiveValue(int x , int y) {
		this.x = x;
		this.y = y;
	}
	
	public void sum() {
		System.out.print(this.x + "  " + this.y);
	}
	
	public void avg() {
		System.out.print( (this.x + this.y) / 2 );
	}

	public static void main(String[] args) {
		toStringTest ts = new toStringTest();
		ts.toReceiveValue(50, 100);
		// 인스턴스 ts 가 이곳 클래스 의 인스턴스 라는 의미.
		// @ 뒤의 내용은 인스턴스 만의 고유식별값.
		System.out.print(ts);
	}
}
```
간단한 계산기 예제 입니다 toStringTest 클래스의 인스턴스 ```ts```는 toReceiveValue()<br>
메소드에 각각 50 , 100 입력 값을 전달하여 ```인스턴스 ts```를 출력해보았는데<br>

결과 값은 다음과 같습니다<br>
```System.out.print(ts);```

```java
ObjectExample.toStringTest@2d363fb3
```
이것은 인스턴스 ts 가 클래스 toStringTest 의 ```인스턴스 라는 의미 ``` 라고 합니다<br>
@ 뒤에 내용은 인스턴에 대한 고유한 식별 값 이라고 하지만<br>
무언가 를 나타내고 있는 주소(?) 같은 것 이라고 이해 하였습니다<br>

## 클래스 안에 toString()

그럼 클래스안에 toString()를 재 정의 (오버로딩) 한다면 어떻게 될까요?<br>

```java
public class toStringTest {
	
	int x , y;
	
	public void toReceiveValue(int x , int y) {
		this.x = x;
		this.y = y;
	}
	public void sum() {
		System.out.print(this.x + "  " + this.y);
	}
	
	public void avg() {
		System.out.print( (this.x + this.y) / 2 );
	}
	## 재 정의
	@Override
	public String toString() {
		// TODO Auto-generated method stub
		return "x 값 : " + this.x + " y 값 : " + this.y +"\n";
	}
    public static void main(String[] args) {
		toStringTest ts = new toStringTest();
		ts.toReceiveValue(50, 100);
		System.out.print(ts);
		System.out.print(ts.toString());
		
	}
}
```
결과는 다음과 같습니다<br>
```java
x 값 : 50 y 값 : 100
x 값 : 50 y 값 : 100
```
기존에 있는 클래스에 ```toString()``` 메소드를 재 정의하고 ```인스턴스를 System.out.print()``` 의<br>
```인자로 전달하면 toString을 명시적으로 호출하지 않아도 동일한 효과가 나타나게 되었습니다```<br>
toString() 을 직접 호출하지 않아도 어떤 객체를 System.out.print() 로 호출하면<br>
자동으로 toString()이 호출한다는 점 이것을 통해 인스턴스를 좀 더 파악할 수 있게 되었습니다.<br>

즉 main에서 ``` System.out.print(ts.toString()); ``` 이 부분을 호출하지 않아도 될 것 같습니다<br>

## equals

equals 는 ``` 객체와 객체가 같은 것인지를 비교할때 ``` 쓰는 메소드 입니다<br>
특히 ```String 끼리 비교```할 때 많이 사용했던 걸로 기억하는데 여기서 더 알게 된 것은<br>

* 객체 간에 동일성을 비교하고 싶을 때는 ``` == ``` 보다 equals가 유용하다.<br>
  String은 클래스 이고 객체이기 때문에 사용 했었던 것.. 다시 알게됨..

* equals 를 ``` 직접 구현 ``` 해야 한다면 hashCode() 도 함께 구현 할 줄을 알아야 하는것.
* 비교 연산자 ```==``` 은 원시 데이터형 이랑 비교할 때만 사용하는 것.<br>
  ```원시데이터 : 기본자료형 int long float double boolean char 등이 있음```

객체와 객체가 같은 것인지를 비교하기 위한 예제를 통해 알아보도록 하겠습니다<br>

```java
class Fruit {
	String name;
	
	public Fruit(String name) {
		this.name = name;
	}
	
	public boolean equals(Object obj) {
		Fruit fruit = (Fruit) obj;
		//name  : String ObjectExample.Fruit.name
		//fruit : Fruit fruit - ObjectExample.Fruit.equals(Object)
		// return name.equals(fruit.name);
		return name == fruit.name;
	}
}

public class EqualsTest {
	
	public static void main(String[] args) {
		
		Fruit f1 = new Fruit("수박");
		Fruit f2 = new Fruit("수박");		
	}
}
```

두 객체의 값을 비교를 위해 main 에서 다음 과 같이 비교 해주었습니다<br>
```java
if (f1 == f2) {
    System.out.print(true);
}else{
    System.out.print(false);
}
```
결과 : ``` false ```

그 다음 비교 <br>

```java
if (f1.equals(f2)) {
    System.out.print(true);
}else{
    System.out.print(false);
}
```

결과 : ``` true ```<br>

비교연산자 ``` == ``` 를 사용할때랑 ``` equals() ``` 메소드를 사용했을 때 결과가 각자 다르게<br>
나오는 이유는 ```f1 과 f2 서로 다른 객체``` 라는 이유로 나온 결과 입니다 <br>

만약 두 개의 객체가 ``` 수박 ``` 이라는 값을 가지고 있고 객체가 같은 객체인지 알고싶을 때<br>
```Object의 메소드 equals를 overiding``` 을 사용합니다<br>

아래코드 중에 ``` fruit = (Fruit) obj; ``` 부분은 메소드 ```equals``` 로 전달된<br>
```obj``` 의 데이터 타입이 Object이기 때문에 이것을 Fruit 타입으로 형 변환 해준 코드 입니다<br>
```java
public boolean equals(Object obj) {
		Fruit fruit = (Fruit) obj; // 형변환
		return name == fruit.name;
	}
```
그 다음 코드는 다음과 같이 분석 해 볼수 있었습니다.<br>
``` return name == fruit.name ; ```<br>

현재 ```객체의 변수 String name``` 과 ```equals 의 인자로(obj) 전달된 객체```의<br>
```name을 비교한 결과를 boolean 값으로 리턴```하고 있습니다 이 값에 따라 두 개의 객체는<br>
같거나 다른것 이 된다는 점을 알 수 있습니다.<br>


## finalize

객체가 소멸될 때 호출되기로 약속되어 있는 메소드 ``` finalize ``` 는 취지만 이해 해보았습니다<br>

먼저 ``` 가비지 컬렉션 ``` 에 대해서 알아봐야 합니다 , 인스턴스를 만드는 것은<br>
컴퓨터의 내부적인 요소에 있는 ``` 메모리 `` 를 사용하는 것 과 같습니다

* 인스턴스를 만든다 - 컴퓨터 메모리 를 사용해서 만들어짐

이때 ``` 메모리 ``` 는 ``` RAM ``` 을 뜻한다고 합니다 램은 가장 빠른 장치이며<br>
컴퓨터 프로그램은 램에 저장된 후 동작하게 되고 , 램을 적게사용 하는 프로그램이<br>
좋은 프로그램이 될 수 있다고 볼수 있겠습니다 많은 프로그래밍 언어들이 램을 효율적으로<br>

사용하기 위해선 ```더 이상 사용하지 않는 데이터를 램에서 제거할 수 있는 방법들을 제공```하지만<br>

자바에서는 이런 방법을 제한적으로 제공되고 있는데 그 이유는 자동적으로 해주고 있기 때문입니다<br>
즉 더 이상 사용하지 않는 데이터를 램 에서 부터 제거할 수 있는 방법을 자동화 된 것을<br>
``` 가비지 컬렉션 ``` 이라고 합니다<br>

* 어떤 인스턴스를 만들었고 이것을 변수에 저장 된 데이터 가 있고,
* 더 이상 사용하지 않아도 판단 된 변수 와 담겨있는 인스턴스는 메모리에 머물러 있을 필요 없으므로<br>
  자바에서 감지 후 자동으로 삭제<br>
* 개발자가 사용하지 않는 데이터를 직접 찾아 삭제하지 않아도 된다는 점 이 있다 !


## 정리

Object 클래스 , 이 클래스가 모든 클래스의 부모라는 점 과 약속된 영역 이라는 것을 이해 하고<br>
이건 자바 만든 곳 과 자바를 이용해 사용하는 개발자 측의 약속된 것임을 알게 되었다,<br>
틈틈히 API 문서를 확인하여 숙지할 수 있도록 할것 !
