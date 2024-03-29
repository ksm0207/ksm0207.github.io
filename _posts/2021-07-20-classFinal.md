---
title:  클래스 정리
author: Kim
date: 2021-07-19 23:25:00 +0900
categories : [Java]
tags: [Java]
pin: true
---

# 클래스와 객체

클래스의 기초적인 개념을 다시 한번 더 공부해보았는데 클래스를 설명할때 가장 적절한건 바로<br>
건물을 지을때 필요한 설계도면이 가장 베스트 이지 않을까 싶었다<br>

개발자를 목수 라고 비유해보면 설계도면의 바탕이 되는 디자인을 보고 건물을 짓는데
이때 완성된 건물을 보고 객체 라고 하는게 맞는 것 같다

<!-- <a href="/posts/classFinal2/">클래스 정리 2부</a> -->
<!-- <a href="/posts/java03-example/">변수와 리터럴</a> -->

## 스타크래프트 - 배럭

<img src = "/post/Java/obj.png"><br>

위 사진은 미네랄 150이면 기초건물을 지을 수 있는 배럭이다 <br>
내가 만약 현실 SCV가 되어서 배럭을 짓는다고 생각해보면 어떨까?<br>

배럭의 설계도면을 건네준 어떤 사람이 나한테 배럭을 지어달라고 요청하면 나는 이거대로<br>
건물을 지어주면 끝나는 일 이라고 생각한다<br>

이렇게 건물이 모두 지어지면 건물의 위치를 나타내는 주소(Reference) 가 있는게 당연하고<br>
주소를 통해 일정한 미네랄을 지불하여 마린 , 메딕 등을 뽑을수 있게된다<br>

똑같은 설계도면을 가지고 다른곳에 배럭을 여러개를 짓는다고 해볼까?<br>

<img src = "/post/Java/obj2.png"><br>

위 사진을 보면 위치가 다르지만 똑같은 건물을 세웠다 하지만 모양만 같을 뿐<br>
다른 객체이면서 각각 주소(Reference)가 있다는 것을 잘 알고있어야 한다<br>

※ 하나의 설계도면을 재사용하여 똑같은 건물이 서로 다른 위치에 각각 만들어져있다<br>
※ 객체도 재사용이 가능하다<br>

## 클래스 - 재사용성을 고려해야 하는 이유

클래스를 작성할 때 재사용성을 고려해야 한다고 한다 그 이유는 한번만 사용하고 버려지는 클래스는<br>
시간낭비 자원낭비가 되기때문이다 따라서 클래스를 객체화 할땐<br>

적어도 다른 곳에서 또는 다른 응용프로그램에서도 필요에 따라 생성하고 사용할 수 있도록<br>
재사용성과 이식성등을 고려하는게 맞다고 본다<br>

객체가 수행하는 능력이 뛰어나면 다른 곳에서도 뛰어난 객체를 사용하려는 횟수가 많아지는데<br>
이렇게 재사용성을 목적으로  속성 - (자료) 과 동작 - (수행력) 을 하나의 객체로<br>

정의하는것 그리고 객체를 중심으로 이루어지는 설계가 객체지향 프로그래밍의 개념이 된다<br>

# 클래스의 구조와 정의

<img src = "/post/Java/class.png"><br>

클래스 구조의 정의를 그림으로 그려봤다 여기서 멤버 필드와 멤버 메소드는 클래스 정의에 매우<br>
중요한 부분이고 다음은 클래스 헤더부터 알아보자<br>


## 클래스 헤더

클래스 헤더는 클래스를 선언하는 부분을 의미한다 여기에는 class 라는 예약어를 중심으로 오른쪽에는<br>
클래스명을 나타내고 왼쪽에는 ```접근제한자``` + ``` 클래스의 형태 즉 종류``` 를 나타내기도 한다<br>

- 접근제한자 : 현재 클래스를 접근하여 생성하고 사용하는 데 있어 제한을 두겠다는 의미<br>

- 클래스종류 : final 클래스 혹은 추상 클래스와 같은 종류를 의미한다 어떤 클래스 인지<br>
               수식어의 일종이며 보통 우리가 생성하는 클래스는 일반클래스이다<br>               

- 클래스명 : 말 그대로 클래스 이름을 의미하며 추가로 상속에 대한 정의 구현에 대한 정의 방법이 있다<br>
             상속은 부모클래스 자식클래스 개념이 있고 구현은 인터페이스 개념이 들어간다고 생각한다<br>

클래스 헤더에 Example 이라는 클래스를 정의하면 다음과 같다<br>

```java
class Example {

}
```
위 클래스는 접근제한 부분과 클래스 종류가 생략된 일반적인 방법이며 중괄호로 둘러싸인 부분은<br>
클래스의 시작과 끝을 의미한다 이 안에서 멤버필드 와 생성자 그리고 멤버 메소드를 정의할 수 있다<br>

그럼 일반적인 클래스 안에 멤버 필드 생성자 멤버함수 세가지를 정의한다고 했는데 각각 무슨 의미를 가진걸까?<br>

## 멤버필드

변수와 상수 즉 자료형을 나타낸다 이건 객체가 만들어질 때 객체의 특징적인 속성을 담아둘 수있다<br>
단 필드의 형태가 static 인지 인스턴스 인지 필드의 개념이 달라지게 된다<br>

- 상수 : 프로그램이 종료될 때 까지 절대로 변하지 않는 값이며 생성할 때 대문자로 만든다
- 변수 : 상수와의 개념이 정 반대이다 프로그램이 종료될 동안 언제든지 값이 변경되는 값이다<br>

멤버필드를 정의한다고 할땐 이렇게 사용하는것이 맞다<br>

```java
class Example {
    int a;
}
```

일반클래스 안에 멤버필드를 정의한 형태이고 하나의 클래스로 똑같은 객체가<br>
여러 개 생성되었을 때 각각객체를 구별하는데 쓰인다<br>

## 멤버메소드

메소드는 특정한 일을 동작하는 행위 라고 생각하면 쉽게 느껴진다<br>

- 멤버필드들의 값을 가지고 작업을 수행한다
- 메소드도 static 메소드 인스턴스 메소드 두가지 종류로 나뉠 수 있다

Static 메소드는 메소드를 가지는 객체를 생성하지 않아도 사용할 수 있는점이 있지만<br>
인스턴스 메소드는 객체를 생성해야만 사용할 수 있는 조건이 있다<br>

멤버 메소드를 정의해보면 다음과 같다<br>

```java
class Example {
    int a;

    public void setData(int value){
        a = value;

        void : 반환하지않음
    }
}
```
a 라는 멤버필드의 값을 매개변수 value 값으로 변경하는 형태의 동작을 정의한 메소드이다<br>
이런 속성들과 동작들을 멤버라고 총칭 할 수 있다<br>

## 클래스 정의

다음 조건을 보고 일상 생활에 있는 사물 중 자유롭게 클래스를 정의해보도록 하자<br>

- 조건 1 : 클래스 명은 자유롭게 정한다
- 조건 2 : 속성 부분은 색상과 볼륨 동작을 기억하는 멤버 필드를 정의한다
- 조건 3 : 동작 부분은 볼륨 업 & 다운 과 색상을 설정하는 메소드를 정의하자

```java
public class Phone {
	
	// 멤버 필드 정의
	String color;
	int volume;
	
    // 멤버 메소드 정의
	public void setColor(String col) {
		// 컬러를 지정한다
        color = col;
	}
	public void volumeUp(int up) {
		// 볼륨을 올린다
        volume += up;
	}
	public void volumeDown(int down) {
        // 볼륨을 내린다
		volume -= down;
	}
}
```

많이 생소한 부분이지만 클래스의 구조는 멤버라는것을 정의할 수 있다 라는것이 핵심이다<br>

# 객체 생성 은 어떻게 ?  멤버들은 어떻게 접근할까 ?

## 객체 생성법

- 클래스 타입의 레퍼런스 변수를 Stack 영역에 올라간다

```java
Phone phone;
```
이 방법은 아직 객체가 생성된 것은 아니다 단지 Phone 클래스 타입의 phone 이라는 참조 변수를<br>
Stack 영역에 등록되는 단계이다<br>

그 다음이 객체를 생성할때 사용하는 new 연산자를 통해 객체를 생성할 수 있다<br>

```java
Phone phone = new Phone();
```
new 연산자를 통해 메모리 내에 공간을 할당받고 Phone 클래스의 생성자를 통해 객체를 생성한 후<br>
생성된 객체를 참조할 수 있는 참조변수를 phone 에 할당한 것이다<br>

※ 객체는 Heap 영역에 등록된다<br>
※ 참조변수는 특정 주소값을 가지고 있으며 객체를 구분할 때 사용할 수 있는 주소번지와 같은 개념이다<br>
※ phone 이 바로 참조변수를 의미하며 16진수인 값을 가지고 있다<br>

## 멤버 접근법

- 멤버 접근에 대해서는 객체의 참조변수를 통해 '.' 을 사용해서 접근할 수 있다<br>

```java
phone.volume = 10;        // 멤버변수 참조
phone.setColor("Yellow"); // 멤버메소드 참조
```
이것을 통해 인자 값을 변수 와 메소드에 할당할 수 있다<br>
※ phone 참조변수 : 멤버변수 와 멤버 메소드 에게 인자 값을 할당해주고 있다<br> 


## 메모리 공간 ? Heap 영역과 Stack 영역

클래스를 통해 객체는 메모리 내에서 생성된다는 개념이있다 우선 메모리 공간은 크게 Stack 과 Heap 영역이 있다<br>

- Stack : 참조할 수 있는 변수와 같은 가벼운 것을 저장하는 영역이다<br>
- Heap  : 참조영역을 따로 가지고있고 객체와 같은 무거운것을 저장하는 공간이다<br>


객체 생성을 하면 메모리 공간의 추상적(?) 구조는 다음과 같이 그려보았다<br>

<img src = "/post/Java/memory4.png"><br>

위 그림과 같이 Heap 영역에는 필요에 따라 생성된 객체들이 존재한다<br>
Stack 영역의 가벼운 것들은 프로세서가 시작하고 끝날 때 자동적으로 JVM에 의해 생성 후<br>
소멸되는 곳 이다 이들을 사용하려면 접근하는법을 알아야한다<br>

# 접근제한자

Phone 클래스에 접근하려면 필요한것이 무엇일까 ? 그럴려면 접근제한자 개념을 파악해볼 필요가 있다<br>

객체의 멤버들에게 접근을 제한할 수 있고 제한 속성에 따라 어떤 멤버에게는 접근을 허용하고<br>
어떤 멤버에게는 접근을 제한한다면 정보에 대한 은닉성을 높여 정보의 유지를 고려하는 효과를 가질 수 있다<br>

멤버들은 객체 자신들만의 속성이자 특징을 가지고 있으므로 대외적으로 공개되는 것은 결코 좋은 방법이<br>
아니라고 한다 . 이런 이유로 프로그래머가 객체의 멤버들에게 접근 제한을 걸어주는데<br>
이를 접근제한자 라고 부른다<br>

객체지향에서 정보은닉 이라는 말이 있다 사용자가 굳이 알 필요가 없는 정보는 사용자로부터 숨겨주는 개념인데<br>
사용자는 언제나 최소한 정보만으로 프로그램을 손쉽게 사용할 수 있게 해야 한다<br>

자바에서는 이러한 정보은닉을 위해서 접근제한자를 제공하고 핵심은 클래스 외부에서의 직접적인 접근을<br>
허용하지 않는 멤버를 설정하여 정보 은닉을 구체화 하는데 유용하다<br>

접근제한자는 총 4가지 종류가 있다<br>

- Public : 모든 접근을 허용
- Protected : 같은 패키지에 있는 객체와 상속관계의 객체들만 허용한다
- default : 같은 패키지 내에 있는 객체들만 허용된다
- private : 현재 클래스 내에서만 허용한다


<img src = "/post/Java/public.png"><br>
<a href = "https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=0neslife&logNo=221542964491">이미지 출처 : 규공간</a><br>

## Private 접근제어자

- private 접근제어자를 사용하여 선언된 클래스 멤버는 외부에 공개되지 않고 직접 접근할 수 없다<br>

- 자바 프로그램은 private 멤버에 직접 접근할 수 없으며 해당 객체의 Public 메소드를 통해서만 접근한다<br>

- private 멤버는 public 인터페이스를 직접 구성하지 않으며 클래스 내부의 세부적인 동작을 구현하는데 사용한다<br>


※ 다른패키지 안에 있는 일반 클래스 와 자식 클래스에서 접근할 수 없다<br>
※ 같은 패키지 안에 있는 일반클래스 와 자식클래스 역시 접근할 수 없다<br>
※ 오직 선언한 클래스 공간에서만 사용한다<br>

```java

public class Sample {
    private String res = "나는 같은 클래스에서만 사용가능해";
    
    private String getPrint(){

        return this.res;
    }
}

```



## Public 접근제어자

- 선언된 클래스 멤버는 외부로 공개되며 해당 객체는 어디에서나 직접 접근이 가능하다

- public 메소드를 통해서만 해당 객체의 private 멤버에 접근할 수 있다

```java

public class Sample {

    public String res = "난 어디에서든 사용할 수 있어";

    public String getPrint(){

        return this.res;
    }
}
```

## Default 접근제어자

- 자바에서는 클래스 와 멤버의 접근 제어의 기본값으로 디폴트 접근제어를 별도로 명시한다

- 접근제어자가 지정되지 않으면 자동적으로 디폴트 접근제어를 가진다

- 접근제어를 가지는 멤버는 같은 클래스의 멤버와 같은 패키지에 속하는 멤버만 접근할 수 있다

※ 같은 패키지에 있는 일반 클래스 와 자식클래스는 접근이 가능하다는 것 다른 패키지에서는 접근 X<br>


```java
package test;

public class Sample {

    // 접근제어자를 명시해준 멤버필드
    public  String a = "public 접근제어자";
    private String b = "private 접근제어자";

    // 접근제어자를 명시를 안해주면
    // 자동으로 디폴트 제어를 가진다
    String c = "default 접근제어자";

    public static void main(String [] args) {
        String res = "다른 패키지에는 접근할 수 없음";
    }
}
```

## Protected 접근제어자

- protected 멤버에 접근할 수 있는 영역은 멤버를 선언한 클래스의 멤버이다

- 멤버를 선언한 클래스가 속한 패키지의 멤버까지 허용한다

- 상속받은 자식 클래스 와 다른 패키지 자식 클래스 포함이다

```java

package test;

public class Sample {
	
	protected String a = "다른 패키지에 존재하는 자식 클래스까지만 허용";
}
```

※ 같은 패키지는 접근 가능<br>

```java
package other;
import test.Sample; // test 패키지의 Sample 클래스를 import 한다

public class Child extends Sample {
	
	public static void main(String[] args) {
		Child c = new Child();
		System.out.println(c.a);
	}
}
```

※ 다른 패키지에 속하는 자식 클래스도 접근허용<br>