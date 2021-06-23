---
title:  인터페이스 (Interface) 개념 이해하기
author: Kim
date: 2021-06-23 22:02:00 +0900
categories : [Java]
tags: [Java]
---


## 인터페이스 , 알아보기전 !

다음의 경우를 생각 해 보겠습니다.<br>

* 나는 동물을 키우는 ```유튜버``` 입니다 그리고 채널에 동물 동영상을 등록합니다<br>
* ```육식동물``` 에게는 다음과 같이 먹이를 줍니다.<br>
* ```치타``` 에게는 사과를 줍니다<br>
* ```사자``` 에게는 수박을 줍니다<br>

위와 같은 내용으로 코드로 담아 학습하려고 만든 클래스는 다음과 같습니다<br>

* Animal 클래스   - 동물(부모) 
* Cheetah 클래스  - 자식
* Lion 클래스     - 자식
* Youtuber 클래스 - main 실행



(1) Animal 클래스

```java
public class Animal {
	
	String name = "";
	
	public void setName(String name) {
		this.name = name;
	}

}
```

(2) Cheetah 클래스

```java
public class Cheetah extends Animal{

}
```

(3) Lion 클래스
```java
public class Lion extends Animal{

}
```

(4) Youtuber 클래스
```java
public class YouTuber {
	
	public void feed(Cheetah ct) {
		System.out.print("사과를 주었습니다.\n");
	}
	public void feed(Lion lion) {
		System.out.print("수박을 주었습니다.\n");
	}
	
	public static void main(String[] args) {
		
		YouTuber ytber = new YouTuber();
		Cheetah ct = new Cheetah();
		Lion lion = new Lion();
		
		ytber.feed(ct);
		ytber.feed(lion);	
	}

}
```

Animal 을 상속한 ``` Cheetah 와 Lion ```<br>
그리고 유튜버 클래스인 Youtuber 는 (4)번과 같이 정의되어있습니다<br>

Youtuber 클래스는 치타 , 사자가 왔을때 각각 다른 feed() 메소드가 호출하게 됩니다<br>
feed() 메소드에는 ```입력값의 자료형 타입이 다른 경우``` ```메소드 명을 동일하게 사용하는데```<br>
이 방식을 ```메소드 오버로딩``` 이라고 합니다<br>

```java
서로 다른 자료형 타입,
public void feed( <Cheetah> ct) {
		System.out.print("사과를 주었습니다.\n");
	}
	public void feed( <Lion> lion) {
		System.out.print("수박을 주었습니다.\n");
	}
```
```※ 입력값의 자료형 타입이 달라도 메소드 명을 동일하게 사용할 수 있는 방법 - 메소드 오버로딩```<br>

Youtuber 클래스를 실행 한 결과는 다음과 같습니다<br>

```java
사과를 주었습니다.
수박을 주었습니다.
```

이제 다음 경우를 생각해 볼 필요가 있습니다<br>

유튜버 채널에 ```치타 와 사자뿐 이라면``` Youtuber 클래스는 사용하는데 크게 상관없겠지만<br>
만약 ```초식동물 토끼 , 소 가 추가 된다면```  ```feed 메소드를 계속해서 추가해야 할 것 입니다```<br>
혹은 ```육식동물 호랑이 , 늑대``` 가 추가될 때마다 마찬가지로 똑같이 추가해야 할 것 입니다<br>

예를들어 동물들이 추가 될 때마다<br>

```java

==육식동물
public void feed(Tiger tg){
    System.out.print(" 돼지고기 를 주었습니다.");
}
public void feed(Wolf wf){
    System.out.print(" 닭고기 를 주었습니다.")
}
==

== 초식동물
public void feed(Rabit rb){
    System.out.print("청경채를 주었습니다.");
}

public void feed(Cow cow){
    System.out.print("풀을 뜯어 주었습니다.");
}
==
```

이런식으로 ```동물``` 이 추가 될 때마다 feed 메소드를 계속해서 추가해야 한다면 번거로움이 생기게 됩니다<br>
하지만 이런 번거로움을 없앨 수 있는 ``` 인터페이스 ``` 를 알아보도록 하겠습니다<br>

## 인터페이스

먼저 ``` 육식동물 인터페이스``` 를 작성 해 보았습니다<br>

* 인터페이스 작성시 class 가 아닌 ```interface``` 키워드를 이용해 작성하기<br>

```java
public interface Predator {

}
```

다음으로 ```Cheetah , Lion``` 클래스에 ``` 인터페이스 를 구현하도록 변경 해 줍니다 ```<br>

* 클래스에 인터페이스 구현은 ``` implements ``` 키워드를 사용합니다<br>

Cheetah 클래스 

```java
public class Cheetah extends Animal implements Predator{

}
```

Lion 클래스

```java
public class Lion extends Animal implements Predator{

}
```

Cheetah , Lion 클래스 에서 ```Predator (인터페이스)``` 를 구현하면 Youtuber 클래스에는 어떤 일이 벌어질까요?<br>

예시 1 ```(인터페이스 사용하기 전 feed() 메소드 )```<br>

```java
public void feed(Cheetah ct) {
		System.out.print("사과를 주었습니다.\n");
	}
public void feed(Lion lion) {
    System.out.print("수박을 주었습니다.\n");
}
```
객체를 넘겨받아 호출하는 방식 , 동물들이 생겨날 때 마다 추가해줘야 하는 번거로움 발생<br>

예시 2 ```(인터페이스 구현 후 feed() 메소드 ) ```<br>

```java
public void feed(Predator predator) {
    System.out.print("먹이를 주었습니다.");
}
```

기존에 feed() ```메소드의 입력으로 Cheetah Lion``` 이 필요로 했었지만<br>
```Predator 인터페이스``` 가 모든 걸 대체할 수 있게 되었습니다<br>

* 예시 1번에서 보이는 ct , lion 은 각 클래스 주인 의 객체<br>
  하지만 ```Predator 객체이기도 합니다``` , 때문에 ```Predator 를 자료형의 타입으로 사용 할 수 있습니다```<br>
* ct -->   Cheetah 클래스    객체 == Predator 객체
* lion --> Lion    클래스    객체 == Predator 객체

※ 객체가 한 개 이상의 ``` 자료형 타입을 갖게되는 특성 ``` 을 다형성 이라고 부릅니다<br>

이제 어떤 육식동물이 추가되더라도 Youtuber 클래스는 feed() 메소드를 추가할 필요가 없습니다<br>
단 동물이 추가 될 때마다 인터페이스를 구현한 클래스를 작성하기만 하면 됩니다<br>

좀더 깊게 가기 위해서 Tiger 클래스 Wolf 클래스를 작성하여 동물들을 추가 해 보았습니다<br>

Tigar 클래스<br>
```java
public class Tiger extends Animal implements Predator{

}
```
Wolf 클래스<br>
```java
public class Wolf extends Animal implements Predator{
    
}
```
인터페이스 가 필요한 이유는 클래스의 구현체와 상관없이 ``` 인터페이스 기준 ``` 으로<br>
중요한 클래스를 작성해야할 때 사용해야 겠다는 생각이 들었습니다<br>
※ 이 시점에서 중요클래스 는 Youtuber 클래스<br>

구현체는 육식동물 치타 , 사자 , 호랑이 , 늑대 등 있고 점점 늘어가지만
인터페이스 는 하나로 기준 잡아 다양한 작업을 할수 있을 것 같습니다<br>

자 이제 육식동물 클래스는 총 4가지 이고 ```Youtuber 클래스``` 와 ```Predator``` 를 수정 해줘야 합니다 <br>

현재 각 육식동물을 호출하면 ```먹이를 주었습니다.``` 라는 내용만 출력되고 있습니다<br>
먹이를 주기만 했지  ``` 어떤 먹이 인지를 줬는지 ``` 는  아직 아무런 정보가 없습니다<br>
떄문에 가장 먼저  Predator 를 수정 할 것 입니다<br>



## 기본적인 인터페이스를 사용해보자

* 각 육식동물 에게 주는 먹이 정보를 출력하기

Predator (인터페이스 수정) <br>
```java
public interface Predator {
	public String getFood();
}
```
인터페이스에 getFood() 메소드를 추가 하였습니다 하지만 메소드에 몸통이 없습니다 왜 그런것 일까요?<br>

※ 인터페이스 특징<br>

* 인터페이스의 메소드는 ``` 메소드 이름과 입출력에 대한 정의만 있고 내용은 없다 ```
* 인터페이스는 ``` implements 키워드``` 가 붙어있는 클래스들이 ``` 구현해야만 한다 ```<br>
  현재 기준에서 육식동물 클래스 들이 기능구현을 해줘야만 사용할 수 있다

getFood() 메소드를 추가한 시점에서 각 육식동물 클래스에는 에러가 났다고 난리를 피우게 될 것 입니다<br>
오류를 해결하기 위해 각 클래스에 getFood() 메소드를 구현 해주어 해결 하였습니다<br>

```java
public class Cheetah extends Animal implements Predator{
    public String getFood(){
        return "닭고기";
    }
}
```
Cheetah 클래스에 이어 Lion , Tiger , Wolf 클래스에 getFood() 메소드를 추가하여<br>
먹이 정보를 리턴 할 수 있도록 해주었습니다<br>

이제 Youtuber 클래스에는 다음과 같이 변경 할 수 있습니다.<br>

Youtuber 클래스<br>

```java
public class YouTuber {

	public void feed(Predator predator) {
		System.out.print(predator.getFood() +"\n");
	}

	public static void main(String[] args) {
		
		YouTuber ytber = new YouTuber();
		Cheetah ct = new Cheetah();
		Lion lion = new Lion();
		Tiger tg = new Tiger();
		Wolf wf = new Wolf();
		
		ytber.feed(ct);
		ytber.feed(lion);
		ytber.feed(tg);
		ytber.feed(wf);
	}
}
```

이전 feed() 메소드에는 "먹이를 주었습니다." 를 출력하였는데<br>
```predator.getFood()``` 를 출력하도록 변경되었습니다 이렇게 호출하게 되면<br>

Predator 인터페이스를 구현한 구현체들 의 getFood() 메소드를 호출 할 수 있습니다<br>
마지막으로 main 메소드를 실행시켜 보면 다음과 같습니다<br>

```java
닭고기
양고기
사슴고기
돼지고기
```
이렇게 인터페이스 의 개념을 알아보았습니다 인터페이스를 사용하기 전 과 후를 정리해보면<br>

* 육식 동물들의 종류만큼 feed() 메소드를 계속해서 추가해야 하는 번거로움이 있었습니다<br>
* 번거로움을 없애고자 인터페이스 Predator 를 사용 한 결과 한개의 feed() 메소드만 호출하여<br>
  코드를 줄일 수 있게 되었습니다<br>

* 중요한 것은 Youtuber 클래스가 동물들의 종류에 더이상 의존적인 클래스 가 아닌<br>
  종류에 상관없는 독립적인 클래스가 되었다는 점이 있었고 이 것이 인터페이스 의 핵심이라 생각됩니다<br>