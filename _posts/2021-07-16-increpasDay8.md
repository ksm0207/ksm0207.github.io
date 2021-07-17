---
title:  자바기반의 응용SW개발자 양성과정 8일차 - 연산자 마무리 , 제어문
author: Kim
date: 2021-07-16 09:19:00 +0900
categories : [Increpas]
tags: [Increpas]
---


# 0716 

자바 클래스명이 한글로 되어있을때 , 리눅스에 올릴려면 문제가 생김.<br>
※ 문제점 : 알아보기.<br>

콘솔창 단축키 : alt + shift + Q 눌러서 (Console) 찾기<br>
창이 사라질땐 되도록 Window 메뉴를 선택하거나 구글링을 잘하자.<br>

## 오전시간 

대입연산자<br>


- ※ a = b : 변수 b의 값을 변수 a에 저장하면 a의 값은 소멸된다

```java
int a = 12;
int b = 5;
		
a = b;
System.out.println(a); // 5
```

- ※ a +=b : b가 가지고 있는 값을 a에 연산 후 저장 됩니다<br>

```java
int a = 12;
int b = 5;

a+=b;
System.out.println(a); // 17
```
※ a-=b  a%=b a*=b 등 동일하게 동작함<br>

다음은 ```12를 5로 나눴을 때``` 나오는 ```나머지 값```<br>

```java
a%=b;
System.out.println(a); // 2
System.out.println(b); // 5

a*=b;
System.out.println(a); // 60
System.out.println(b); // 5
```

※ ```&&``` 연산자는 ```왼쪽 조건이 false``` 일 경우 ```오른쪽 조건은 실행하지 않는다```<br>
※ ```||``` 연산자는 둘중 한가지 값만이 true 인경우를 나타낼 수 있다<br>
※ !(Not) 연산자는 true / false 변경이 가능하다<br>

- ! true --> false // ```선``` 조건이 ture 일 경우
- ! false --> ture // ```선``` 조건이 false 경우

```java
// 선 조건이  true 이므로 false를 반환
c =  !(a!=b && a>b);
System.out.println("!(a!=b && a>b = "+ c);
```

## 증감연산자

변수의 값을 직접 변하게 만들 수 있다<br>

- ++ (1씩증가)
- -- (1씩감소)
- ++a ``` 변수 a의 값을 1 증가``` 시킨 후에 해당 연산을 진행함.
- a++ ```먼저 해당 연산을 수행하고``` 나서, 피연산자의 값을 1 증가시킴.

```java
int a = 12;
System.out.println(++a); // 13
System.out.println(a++); // 13 ( Stack 14)
System.out.println(++a); // 15
```

```java
int N = 1;
		
System.out.println(++N); //  2

System.out.println(N ++); //  2 출력 , Stack = 3)

System.out.println(N ++); //  3 출력 , Stack = 4  

System.out.println(++ N); //  5
```
※ 증감연산자는 ```+ 또는 -``` 가 ```변수 앞에 있으면 우선순위가 높아져서``` 수행합니다<br>
※ 반대로 ```변수 뒤에 있으면 우선순위가 낮아져``` 나중에 수행합니다<br>

※ ```.println(a++)``` --> . 연산자로 먼저 프린트를 한 다음 13을 출력하고 <br>
  ```후 증가``` 되는 것 입니다 (좀 많이 헷갈리는 부분이었음) <br>

※ : ```.``` 연산자는 이항 연산자 이며 ```피리어드``` 라고 읽는다.<br>

※ 사용자 암호화 : 라이브러리를 활용할 것<br>


## 비트연산자

- [&] : and 두 비트가 모두 1일 경우에만 연산결과가 1로 표현됩니다.
- [or] : or
- [^] : 배타적OR : 서로 다른 값일 때만 값이 1이 된다.

```문제1)``` 출력 결과는 4 인데 왜 4가 나온걸까?<br>

```java
int a = 12;
int b = 6;

int c = a & b;

System.out.println(c);
출력
4
```

## 컴퓨터 비트<br>

최소 1의자리 부터 최대 64까지 있는 bit 단위가 있다고 가정하자 (2의1승 ★)<br>
``` int a = 12``` 를 비트 단위로 쪼개면 ```1 1 0 0``` 컴퓨터는 이렇게 표현한다<br>

```java
|[64] [32] [16] [8] [4] [2] [1]|
   생략         [1] [1] [0] [0]
```

```1 1 0 0``` 이 될수 있었던 이유는 비트 자리에 [8] [4] 가 불이 켜졌기 때문이다<br>
※ 컴퓨터는 저장할 수 있는 범위에 1을 나타내고 아닌 경우 0을 나타냅니다<br>

가장 끝자리 1부터 왼쪽으로 한칸씩 움직일 때 마다 2의1승 단위로 움직이는데<br>
그중에 ``` 1 ``` 로 나타내고 있는 비트자리를 연산하면 12가 나온다<br>

```java
[8] [4] [2] [1]
[1] [1] [0] [0] //  
// 0 +  0 + 2의2승 2의3승 = 0 + 0 + 4 + 8 
// 8 + 4 = 12
```

만약 int a = 14 였다면 어떻게 표현될까?<br>
```java
int a = 14
[8] [4] [2] [1]
[1] [1] [1] [0] 
// 0 + 2의1승 2의2승 2의3승 = 0 + 8 + 4 + 2
14가 나온다
```

int a = 15<br>

```java
int a = 15
[8] [4] [2] [1]
[1] [1] [1] [1]
// 1 + 2 + 4 + 8 = 15
```

그렇다면 12 & 6 이 왜 4가 나왔는지 이제야 이해할 수 있게된다<br>

<img src = "/post/Java/and.png"><br>
※ 이미지 출처 : <a href = "https://coding-factory.tistory.com/521">코딩팩토리</a>
- [&] : and 두 비트가 모두 1일 경우에만 연산결과가 1로 표현됩니다.

위 조건 때문이고 내가 생각한대로 풀이해보면 다음과 같다<br>

```java
12 의 컴퓨터 식 표현
[1][1][0][0]

6  의 컴퓨터 식 표현
[0][1][1][0]
```

이렇게만 보면 ``` 두 비트가 모두 1 일 경우에만 ``` 연산 결과가 1로 표현된다<br>
라는 조건이 있다 이걸 응용해보면 오른쪽에서 세번째 자리가 조건식에 맞으므로<br>

```java
[1]  [1][0][0]
      t
      r
      u
      e  
[0]  [1][1][0]
2 제곱으로 계산하면 저 자리는 4가 나온다
```

그외 비트연산자 알아보기 <a href = "https://coding-factory.tistory.com/521">코딩팩토리</a><br>

※ : 데이터의 표현 단위는 Bit 단위 와 Byte 단위가 있다<br>

- Bit : 컴퓨터가 표현하는 데이터의 ```최소단위``` 2진수 값 하나를 저장할 수 있는<br>
  메모리의 크기<br>

- Byte : 8개의 비트를 묶은 단위<br>

<a href = "https://blog.kimtae.xyz/5">데이터 표현 방식의 이해</a><br>



## 오후시간

삼항연산자<br>

- 삼항연산자 ( 조건연산자 )
- 사용법 : (조건식) ? 참 거짓
- 연산자가 해석이 더 빠름<br>

※ ``` 값을 비교할땐 자료형 타입``` 이 같아야한다<br>

연습1)<br>

```java
int a = (5 > 4) ? (5) : (4);
결과
4
```

연습2)<br>

```java
int a1 = 12;
int b1 = 20;

boolean check = (a1 > b1) ? true : false;
System.out.println(check);
출력
false
```

연습3)<br>

```java
int val1 = 20;
int val2 = 30;
		
int test = (val1 > val2 ? (true) : val2); // Error

에러내용 : 유형이 일치하지 않음: 개체 & 직렬화 가능 & 비교 가능
object에서 변환할 수 없습니다.> int로 ...
```

연습4)<br>
```java
int val1 = 20;
int val2 = 30;

int test = ((val1 > val2) ? (val1 + val2) : (val1 - val2));
System.out.println(test);
결과
-10
```

※ 삼항연산자를 사용하면 코드가 줄어들지만 컴파일 속도가 빠른건 아니다<br>



## if - else  swithch 제어문 반복문

- if문<br>

if문의 기본적인 형태는 다음과 같다<br>

```java
if (조건식) {실행}
else {실행}
else if : if 문과 동일
```

(1)``` if else , else if문의 형태```<br>

```java
if (조건식)
{
  조건식에 맞는 실행코드 true 값을 반환한다
}
else if (조건식)
{
  첫번째 if에서 false 를 만났으면 그다음
  실행되는 곳이다
}
else
{
   if + else if 모두 false를 반환하면 이곳을 실행한다
}
```
※ if 조건식 결과가 false 이면 실행되지 않고 else로 넘어온다<br>
※ 한쪽이 실행되면 한쪽은 실행될 수 없다


Switch문의 작동순서<br>

```java
switch(value)
{
  case 변수값: 실행코드
               break;
  case 변수값: 실행코드
               break;
  case 변수값: 실행코드
               break;
               .
               .
               .
}
```
if문과 달리 ```실행조건``` 이 두개로 나뉜다<br>

※ break 는 실행문이 끝날때마다 적어줘야 한다 안하게 되면 case를 이어 실행하게된다<br>
※ 해당 로직을 실행하지 않고 밖으로 나온다는 것으로 받아들이자.<br>

※ Switch 와 if else 중 어떤 것을 써야할까? (정리)<br>

- Switch 는 지정된 변수를 입력받고 미리 정해놓은 ``` 값 ``` 을 찾아 Case를 실행하는 반면
- ```if else``` 구문은 boolean 의 결과 값을 내놓는 조건문에 따라<br>
  코드의 흐름이 달라질 수 있다<br>

if else 문을 쓸 수 있는 모든 상황에 Switch 문을 사용할 수 있는건 아니지만<br>
그와 반대로 모든 Switch 구문은 if else문으로 대체될 수 있다<br>

★ : if - else + Switch 교재 보고 예제풀이 하기

<a href = "https://github.com/ksm0207/increpas/tree/main/Example/src/increpas_example02">0716 교재 문제풀이</a><br>




