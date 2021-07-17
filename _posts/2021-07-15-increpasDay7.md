---
title:  자바기반의 응용SW개발자 양성과정 7일차 - 자바
author: Kim
date: 2021-07-15 09:19:00 +0900
categories : [Increpas]
tags: [Increpas]
---


# ERD 유저들의 아이템 구매현황 파악하기.

※ 연습필요<br>

문제) 특정 게임 유저들의 아이템 구매현황을 파악하고자 한다.<br>
아이템 종류는 티셔츠 모자 바지 안경 등<br>
유저가 언제 어떤 어이템을 구매했는지를 알 수 있어야 한다<br>

- 유저정보 : ID  , name , email , phone<br>
- 아이템정보 { name , price , 상태 0 이면 판매중 , 1이면 중지 history_fk}<br>
- 카테고리 정보 ,history pk , history_name(설명)<br>

- 구매(판매)현황 : pk , 아이템 고유번호(fk) ,  ID(fk) , 구매날짜

다른 현황판도 만들어보기. , 다른 스키마 접근법 알아보기 , Mysql 컨넥션 오류 해결한거 포스팅 정리하기<br>

톰캣 알아본 것<br>
<a href = "https://all-record.tistory.com/49">톰캣연동하기</a><br>
<a href = "https://itworldyo.tistory.com/88">톰캣 버전 고르기<br>


# 자바 두번째 시간

- Package : 의미를 부여하고 파일을 저장하는 주머니 같은 것<br>
ex) [필통] , 필기도구<br>

- ' . '  연산자 (피리어드 연산자) , ~안에 참조

- 데이터 선언 : 8가지 자료형은 예약어로 명시되어있음

데이터 종류<br>

- char 문자형 , '1' 자를 저장하는 자료형
``` char a = 'H'  O  ||  X  char a = 'Hi' X ```<br>
- boolean : true / false 참 거짓 을 나타내는 자료형<br>
- byte , short , int , long : 정수형<br>
- float , double : 실수형

헷갈렸던 것 (용어) <br>

- 홑따옴표 = ''
- 겹따옴표 = ""


객체 자료형 , 기본자료형 데이터 저장 차이 알아보기<br>
- 자바 메모리 구조 정리하기<br>

```java
// 연산자 중심 : 왼쪽
		
		// >  : 크다
		// <  : 작다
		// >= : 크거나 같다
		// <= : 작거나 같다
		// == : 같다
		// != : 같지 않다
```

문제)a 의 값 , b 의 값이 서로 같은지 비교하고 변수 c에 넣으세요<br>

```java
int a = 10;
int b = 7;
boolean c = a > b;

c = a == b;
System.out.println("a == b " + c);
결과

false
```

# int long 을 보편적으로 쓰는 이유

```java
byte res = a1 + b1; X
int res = a1 + b1 ; O
```

위 코드는 왜 오류일 까 ? <br>
 자바에서는 ```32bit 체제 int 형 밑의 자료형들``` --> ```(byte 와 shrot)``` 들은<br>
연산을 수행하면 결과 값에 상관없이 무조건 int 형으로 형변환 된다<br>

※ byte short 끼리 연산할 경우 표현할 수 있는 범위를 벗어나게 때문에 <br>

- byte : 8bit
- shrot : 16bit
- int : 32bit
- long : 64bit

메모 > OOP 개념 잘 잡기<br>

# char

## 유니코드 : 세계 문자 표준 문자

- 세게 각국의 언어를 처리하고 표현하기 위한 것
- 24개 언어를 지원하며 34.168개의 개별 코드문자를 담고있습니다.

<img src = "/post/JavaDownload/as.png"><br>



아스키코드 , 유니코드를 간단하게 출력해보기<br>

```java
package example0715;
public class CharEx {
	
	public static void main(String[] args) {
		
		char c = 'A';
		System.out.println("c의 값 = " +c);
		
		c = 65;
		
		System.out.println("유니코드 65 = " +c);
	}
}
출력
c의 값 = A
유니코드 65 = A
```

아스키코드 , 유니코드를 입력 받고 출력하기<br>
- 문자형 에서 숫자로 바꾸기

```java
package example0715;

import java.util.Scanner;

public class AscTest {
	
	public static void main(String[] args) {
		
		Scanner scan = new Scanner(System.in);
		
		System.out.println("문자 -> 숫자 바꾸기");
		System.out.println("Input : ");
		
		char value = scan.next().charAt(0);
		int change = value;
		
		System.out.println(change);
	}
}
```

아스키코드 , 유니코드를 입력 받고 출력하기
- 숫자에서 문자로 ! 무한으로 입력받기.

```java
package example0715;
import java.util.Scanner;

public class AscTest2 {
	public static void main(String[] args) {
		
		Scanner scan = new Scanner(System.in);
		
		System.out.println("숫자 -> 문자");
		System.out.print("숫자 입력 : ");
		int value;
		while(true) {
		   try {
				value = scan.nextInt();
				char c = (char)value;
				System.out.println(c);
	
			} catch (Exception e) {
				System.out.println(e.getMessage());
				scan = new Scanner(System.in);
			}	
		}
	}
}
```
Char 형은 내부적으로 모두 아스키코드 정수값으로 저장된다 즉 이 말은 키보드에 있는<br>
모든 글자들은 각각 입력값이 있다고 보면 될 것 같다<br>

- Char의 표현범위 : 0 ~ 65,535