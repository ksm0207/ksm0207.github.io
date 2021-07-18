---
title: 클래스(Class) 파악하기
author: Kim
date: 2021-06-16 18:35:00 +0900
categories : [Java]
tags: [Java]
---

## 클래스

동물 이라는 클래스는 다음과 같이 만들어 보았습니다.
```java
public class Animal {

}
```
위 동물 클래스는 클래스의 선언만 있고 내용이 없는 껍데기뿐인 클래스 이지만<br>
이 껍데기만 있는 클래스도 중요한 기능을 가지고 있는데<br>
그것은 바로 객체를 만드는 기능이있습니다.<br>

## 객체는 어떻게 만드나요 ?

```java
new 연산자 를 이용하여 클래스를 로드하는 방식.
Animal dog = new Animal ();
```
new 연산자는 객체를 생성할 때 사용하는 키워드 이고 이 연산자를 통해서<br>
동물 클래스의 인스턴스인 ```dog```로 통해 ```Animal 객체```를 만들 수 있습니다.<br>

## 객체와 인스턴스 ? 말이너무 어려워요!!

```클래스에 의해서 만들어진 객체를 인스턴스``` 라고 부릅니다<br>
현재 경우에는 dog가 바로 그것이 되는데 그렇다면 객체와 인스턴스 의 차이는<br>
무엇인지 알아가는 것이 매우 중요합니다.<br>

먼저 이렇게 생각해보겠습니다. ```Animal dog = new Animal () 이렇게 만들어진 dog```는<br>
객체가 되고 dog 객체는 Animal의 인스턴스가 됩니다 즉 인스턴스는<br>
특정 객체(dog)가 어떤 클래스의 객체인지를 관계위주로 따질때 사용됩니다.<br>

즉 dog는 인스턴스 보다 dog 객체 라는 표현이 자연스럽고 dog는 Animal 의 객체보다는<br>
Animal 의 인스턴스 라는 표현을 쓸 수 있습니다.<br>

※ Animal 의 인스턴스는 dog , dog는 Animal 객체<br>
과자를 만드는 과자틀과  틀 안에서 만들어진 과자로 설명해보자면..<br>

과자틀 -- > 클래스 (Snack) || 과자틀에 만들어진 과자 → ObjectName 객체가 되는데<br>
클래스는 다음과 같이 많은 과자 객체들을 Snack 클래스로 만들 수 있습니다<br>

```java
Snack potato = new Snack
Snack gobukchip = new Snack
Snack bananachip = new Snack …
```

# 객체 변수 ( Instance Variable )

Animal 클래스에 조금 더 발전시켜 Animal 클래스로부터 만들어지는<br>
동물 이름을 지어주도록 해보겠습니다<br>

```java
public class Animal {
	String name;
}
```

Animal 클래스에 name 이라는 ```String 변수```를 추가했습니다<br>
이렇게 ```클래스안에 선언된 변수를 객체변수``` 라고 부르며<br>
```인스턴스 변수 || 멤버 변수 || 속성``` 이라고도 말합니다<br>

클래스에 의해 생성되는 것은 객체라고 말하고 선언된 변수는<br>
객체변수 라고 하였고 이제 이것을 사용해보도록 하겠습니다<br>

먼저 객체변수는 말 그대로 변수이므로 값을 대입할 수 있을 것 입니다<br>
그럼 어떻게 객체 변수에 ``` 접근``` 해야 하는지를 알아야합니다<br>

객체 변수는 다음과 같이 . 연산자를 이용하여 접근할 수 있습니다<br>

```java
Animal dog = new Animal 객체생성
dog.name ( . 연산자를 이용하여 접근 )
```

```위와 같이 dog 객체를 생성하여``` dog 객체의 객체변수 name에 접근할 수 있습니다<br>
이제 객체 변수에 어떤 값이 대입되어 있는지 다음과 같이 출력해보면.<br>

```java
Console : null 
```

null 이라는 값을 얻었습니다 ```null 이라는 것은 아무런 값이 할당되어 있지 않은```<br>
상태를 말합니다 객체 변수로 name을 선언했지만 아무런 값을 대입하지 않았기 때문에 <br>
null 이 출력된 것 입니다<br>

지금까지 알아본 것은 객체를 new 연산자를 통해서 생성하는법과<br>
객체변수에 접근하는법 을 알았지만 값은 현재 null 이라는 것 을 확인했습니다<br>
이제 객체 변수에 값을 대입하는 것에 대해서 알아볼 것 입니다<br>

객체 변수에 값을 대입하는 것은 여러가지 방법이 있지만 가장 보편적인 방법은<br>
메소드를 이용하는 것 인데<br>

클래스에는 객체 변수와 더불어 메소드 라는 것이 있습니다 메소드는 클래스 내에<br>
구현되어 있는 함수를 의미하는데 보통 함수라고 말하지 않고 메소드 라고 말합니다<br>

이제 메소드를 이용하여 Animal 클래스의 객체 변수인 name에 값을 대입해보겠습니다<br>
아래와 같이 setName 이라는 메소드를 추가 해 봅시다.<br>

## 클래스 실습하기 
```java
public class Animal {
	
	String name;
	
	public void  setName(String name) {
		this.name = name;
	}
   
   public static void main(String[] args) {
	   
	   Animal dog = new Animal();
	   
	   System.out.println(dog.name);
	
   }
```

Animal 클래스에 추가된 setName 메소드는 다음과 같은 형태의 메소드입니다<br>

* 입력 : String name<br>
* 출력 : void (리턴값은 x)<br>

입력으로 name 이라는 문자열을 받고 출력은 없는 형태의 메소드이며 메소드의<br>
입출력에 대한 자세한 내용은 다음 장에 다뤄집니다<br>

이번에는 setName 메소드의 내부를 살펴보면 다음과 같은 문장을 가지고 있습니다<br>

```java
this.name = name;
```

여기서 ```this``` 에 대해서 이해 하는 것은 꽤 중요한 부분입니다 이 문장에 대한 설명은<br>
잠시 보류하고 일단은 이 메소드를 호출하려면 다음과 같이 호출해야합니다.<br>

```java
dog.setName(“puppy”);
```

여기서 setName 메소드의 입력으로 문자열을 전달해야하는데 그 이유는 setName<br>
메소드는 입력항목으로 문자열을 필요로 하기 때문입니다<br>
setName 메소드를 호출할 수 있도록 main 에서 다음과 같이 처리합니다<br>

```java
public static void main(String[] args) {
	   
	   Animal dog = new Animal();
	   dog.setName("Puppy");
	   System.out.println(dog.name);
   }
```
이렇게 다시 실행하면 setName 메소드가 호출 될 것 입니다.<br>

이제 setName 메소드 내부를 살펴 보도록 하겠습니다<br>

```java
public void  setName(String name) {
		this.name = name;
	}
```
```this.name = name;```

main 메소드에서 dog.setName(“Puppy”); 와 같이 Puppy 라는 입력값으로<br>
setName 메소드를 호출했기 때문에 setName 메소드의 입력항목인<br>
name 에는 Puppy 문자열이 전달 되었습니다<br>

따라서 setName 메소드의 this.name = name; 문장은 다음과 같이 해석할 수 있습니다<br>
```java
this.nama = “Puppy”;
```

setName 메소드 내부에 사용된 ```this 키워드```는 Animal 클래스에 의해서 생성된<br>
객체를 지칭하는데 만약 Animal dog = new Animal() 와 같이 dog 객체를 만들고<br>
dog.setName(“Puppy”) 와 같이 메소드를 호출하면<br>

setName 메소드 내부안에 있는 ```this 키워드는 dog 객체를 지칭하는 것``` 과 같습니다<br>

그럼 만약에 ```Animal cat = new Animal()``` 으로 ```cat``` 객체를 만든 후 ```cat.setName(“Cat”)```<br>
을 호출한다면 setName 메소드 내부에 this는 cat 객체를 가리키게 되는 것 이죠<br>

따라서 this.name = “Puppy” 는 다음과 같이 해석 할 수 있습니다<br>
```dog.name = “Puppy”```<br>

이렇게 dog.name 과 같이 this 키워드를 사용하면 객체 변수에 접근할 수 있다는 것을 알아보았습니다<br>


## 객체 변수는 공유되지 않는다.

이번에는 main 메소드를 다음과 같이 변경 해 보았습니다

```java
Animal dog = new Animal();
       dog.setName("Puppy");
	   
Animal cat = new Animal();
       cat.setName("Cat");
```
dog 객체에는 Puppy 이름을 대입하고 cat 객체에는 Cat 이름을 대입했습니다<br>
이럴 경우 setName 메소드에 의해서 다음과 같은 문장이 두번 실행 될 것입니다<br>

```java
dog.name = “Puppy”
cat.name = “Cat”
```
이럴 경우 cat.name = “Cat” 문장이 나중에 수행되므로 dog.name의 값도 Cat 으로<br>
변경되지 않을까 라는 생각이 날 수 있습니다<br>
만약 Animal 클래스의 ```객체변수 name이 dog 객체와 cat 객체간 서로 공유되는```<br>
```변수라면``` 그럴 가능성은 있지만 결과는 다르게 나옵니다<br>

```java
public static void main(String[] args) {
	   
	   Animal dog = new Animal(); // dog객체
	   dog.setName("Puppy");
	   
	   Animal cat = new Animal(); // cat 객체
	   cat.setName("Cat");
	   
	   System.out.println(dog.name);
	   System.out.println(cat.name);
   }
```

결과는 다음과 같이 출력됩니다<br>
```java
Puppy
Cat
```

name 객체 변수는 공유되지 않는다는 것을 확인할 수 있습니다<br>
이 부분은 너무 중요한 부분이며 필히 숙지해야하는 부분이라고 합니다<br>
클래스에서 가장 중요한 부분은 ```객체 변수의 값이 독립적으로 유지된다는점```<br>

클래스의 존재이유는 바로 이 점 때문이라고 볼 수 있습니다<br>
객체지향적 이라는 말의 의미도 결국은 객체 변수의 값이 독립적으로 유지되기때문에<br>
가능한 것이죠<br>

※ 객체 변수의 값은 공유되지 않지만 static을 이용하게 되면 객체 변수를 공유하도록<br>
할 수는 있습니다<br>