---
title:  자바기반의 응용SW개발자 양성과정 9일차 - 자바
author: Kim
date: 2021-07-19 06:00:00 +0900
categories : [Increpas]
tags: [Increpas]
---

# 오전시간

- 나이를 체크하는 프로그램 : 10대 ~ 40대까지
- 그 외의 나이가 입력되면 " 나이 범위를 벗어났습니다 " 라는 문장 출력
- 예 ) 입력 : 40 출력 : 40대시군요!

코드작성<br>

```java
package pm;

import java.util.Scanner;

public class AgeCheck {
	public String check(int age) {
		String res = "";
		
		if (age >= 10 && age <= 19) {
			res = "10";			
		}else if (age >= 20 && age <= 29) {
			res = "20";
		}else if (age >= 30 && age <= 39) {
			res = "30";
		}else if(age >= 40 && age <= 49) {
			res = "40";
		}
		return res;
	}
	public static void main(String[] args) {
		
		// 1.키보드로 부터 나이를 입력 받는다.
		// 조건 : 10대 20대 30대 구별하는 프로그램을 만드세요
		Scanner scan = new Scanner(System.in);
		AgeCheck ac = new AgeCheck();
		
		int value = scan.nextInt();
		String res = ac.check(value);
		
		if(res == "") { 
			System.out.println("Exit...");
		}else{
			System.out.println(res + "대");
		}
	}
}
```

10 ~ 49 세의 범위로 나이를 체크해주었고 메서드는 따로 구현해주었다<br>

※ Scanner : 키보드로 입력받을 수 있게 입력장치를 가진 객체를 호출한 것<br>

※ int value = scan.nextInt() 는 정수를 받아 반환하는 기능을 가진<br>
메서드를 호출한걸로 다시한번 이해하였다<br>

<strong>또 다른문제</strong><br>

이번에는 위에 있는 문제와 비슷한 문제지만 약간 다르게 해 보았다<br>

- 나이 입력받기
- 40 이상 -> 어르신
- 30 대 -> 정말 좋을 때
- 20 대 -> 눈물나게 좋을 때
- 10 대 -> 미성년 

```java
package am;

import java.util.Scanner;

public class Ex1_if {
	
	public String ageCheck(int age) {
		String res = "";
		
		if (age >= 40) { // 40이상 숫자
			res = "어르신";
		}else if (age >= 30) { // 자연스럽게 30~ 39까지 범위를 저장함
			res = "정말 좋을 때";
		}else if (age >= 20) {
			res = "눈물나게 좋을 때";
		}else {
			res = "미성년";
		}
		return res;
	}
	public static void main(String[] args) {		
		
		Scanner scan = new Scanner(System.in);
		Ex1_if ex1 = new Ex1_if();
		
		int val = scan.nextInt();
		String res = ex1.ageCheck(val);
		
		if (res != "")
			System.out.println(res +" 입니다");
	}
}
```
숫자의 범위를 체크하려면 무조건 논리연산자를 사용하는게 좋겠다는 생각이 들었는데<br>
무조건 이라는건 없는 것 같다 그냥 큰 숫자부터 비교연산자로 범위를 잡아주면<br>
밑에 숫자들은 자연스레 범위를 줄어드게 할수있는 방법도 있구나 라는걸 알게되었다<br>


# 반복문

<strong>반복문은 여러 개의 문장을 반복 수행하고자 할 때 사용한다 종류는 다음과 같다</strong><br>

- for ★ 제일중요한 것
- while
- do~while

for 문 외에 while / do ~ while 은 구성 자체가 다르므로 스타일대로 진행해도 괜찮다<br>
먼저 for문의 구성을 알아보자<br>

<strong>for 문의 구성</strong>

- for(초기식 ; 조건식 ; 증감식)
- {반복할 내용}




연습문제) for문을 사용하여 1부터 10까지 값을 출력해보자<br>

```java
package am;

public class Ex2_for {
	public static void main(String[] args) {
		for (int i = 1 ; i <= 10 ; i ++ ) {
			System.out.println(i);
		}
	}
}
출력
1 2 3 4 5 6 7 8 9 10
```
<img src = "/post/Java/for.png"><br>

- 초기식 : 변수 i = 1
- 조건식 : i 가 10 보다 작거나 같을 때 까지
- 증감식 : 조건식이 true 일때만 증감한다


연습문제2 ) for문을 사용하여 1부터 10까지의 합을 출력하자<br>

```java
package am;

public class Ex3_for {	
	public static void main(String[] args) {
		
		int sum  = 0;
		
		for (int i = 1 ; i<= 10 ; i++) {
			sum = sum + i;
		}
		System.out.println(sum);
	}
}
```
※ 변수는 어디서 선언했는지 잘 확인하고 사용하자.<br>
※ for문 안에 변수랑 for 밖의 변수는 완전히 다른 변수 이므로 주의해서 사용할 것!<br>


<strong>구구단 찍기</strong><br>

```java
package am;

import java.util.Scanner;

public class Ex4_for {
	public static void main(String[] args) {
		// 1. 구구단 
		Scanner scan = new Scanner(System.in);
		int val = scan.nextInt();
		
		for (int i = 1 ; i <= 9 ; i ++ ) {
			System.out.println(val + " * " + i + " = " + (val * i));
		}
	}
}
```

# 오후시간

## while

```java
package pm;

public class Ex1_while {
	public static void main(String[] args) {
		
		int i = 1;
		while(i <= 10) {
			System.out.printf("%-2d", i);
			++ i;
		}
		System.out.println();
		i = 1;
		int sum = 0;
		while (i <= 10)
			
			sum = (sum) + (i++);
		// printf() 첫번째 들어오는 값은 포맷을 지정함
		System.out.printf("1 ~ 10 까지의 합 : %-3d" , sum);
	}
}
```
<strong>출력</strong><br>

```java
1 2 3 4 5 6 7 8 9 10
1 ~ 10 까지의 합 : 55 
```

분석 (1)<br>

```java
int i = 1;
while(i <= 10) {
    System.out.printf("%-2d", i);
    ++ i;
}
System.out.println(); // 줄바꿈
```
<strong>출력</strong><br>

```java
1 2 3 4 5 6 7 8 9 10
```

변수 i의 초기값은 1로 지정되어있고 while문은 i가 10보다 작거나 같은지 조건식을 주는데<br>
결과는 true를 반환하여 ```1 2 3 4 5 6 7 8 9 10 ``` 를 출력할 수 있게 됩니다<br>

※ true를 반환하므로 i는 점점 늘어나게 된다<br>

분석 (2)<br>

```java
i = 1;
int sum = 0;
while (i <= 10) {
    sum = (sum) + (i++);
    System.out.println("Sum = " + sum + " " + "i = " + i);
}
// printf() 첫번째 들어오는 값은 포맷을 지정함
System.out.printf("1 ~ 10 까지의 합 : %-3d" , sum);
```
첫번째 while 문이 종료되면서 i가 마지막으로 가지고 있는 값은 10을 가지고 있기 때문에<br>
변수 i를 다시 1로 초기화하여 1부터 10까지의 합을 출력할 수 있게됩니다<br>

<strong>while문이 연산하는 과정</strong><br>

```java
Sum = 1 i = 2
Sum = 3 i = 3
Sum = 6 i = 4
Sum = 10 i = 5
Sum = 15 i = 6
Sum = 21 i = 7
Sum = 28 i = 8
Sum = 36 i = 9
Sum = 45 i = 10
Sum = 55 i = 11

1 ~ 10 까지의 합 : 55 
```

## do-while

- while 문 이나 for 문은 선 비교 후 처리이기 때문에<br>
  조건에 만족하지 않으면 반복하지 않는다.<br>

- do-while 문은 선 처리 후 비교이므로 조건에 만족하지 않아도<br>
  최소 1번은 수행하게 되는 구조이다<br>

```java
do {
    반복할 구문

}while(조건식);
```

최소 1번은 다음과 같은 예를 든 것<br>
```java
package pm;

public class Ex2_dowhile {
	public static void main(String[] args) {
		int i = 11;
		do {
			
			System.out.printf("%-2d", i);
			i ++;
		} while (i <= 10);
	}
}
출력
11
```

## do - while 문을 이용하여 구구단 만들기

- Scanner로 입력받기.

```java
package pm;

import java.util.Scanner;

public class Ex3_dowhile_G {
	public static void main(String[] args) {
		
		Scanner scan = new Scanner(System.in);
		System.out.print("입력 : ");
		
		int i = 1;
		
		int dan = scan.nextInt();
		
		do {
			System.out.println(dan + " * "+ (i) + " = " + (dan * i));
			i ++;
		} while (i <= 9);
	}
}
```

## 중첩 for문

- for문안에 또 for문

중첩for문 개념은 솔직히 어렵다고 생각했는데 이번 수업으로 완벽하게 이해하게 되었다<br>
첫번째 for문은 행을 만드는 것 이라 생각하고 안에 들어가는 for문은 열을 만든다고 생각하면<br>

중첩 for문의 개념은 쉽게 잡을 수 있다<br>

```java
package pm;
public class Ex6_MultiFor {
	public static void main(String[] args) {
		
		char c = 65;
		
		for (int i = 1 ; i <= 3 ; i ++) {  // start for 2 (행의 수를 만듦)
			for (int j= 1; j <= 5 ; j++) { // start for1 (열의 수를 카운트)
				System.out.printf("%-2c",c ++);
			}
			System.out.println();
		}
	}
}
출력
A B C D E 
F G H I J 
K L M N O 
```

유명한 별찍기 문제<br>

```java
package pm;

public class Ex7_MultiFor {
	public static void main(String[] args) {

		// * * * * *
		// * * * * 
		// * * *
		// * *
		// *
		for (int i = 5 ; i > 0 ; i --) { // 5 4 3 2 1
			
			for (int j = 1 ; j <= i;  j ++) {
				System.out.print(j);
			}
			    System.out.println();
		}
	}
}
출력
* * * * * 
* * * * 
* * * 
* * 
* 
```

## break문 + break label

break문은 가장 가까운 반복문을 탈출할 때 쓴다<br>
※ 중첩반복문을 사용할 때 전체를 탈출하지 못함.<br>

오늘 수업하면서 처음 알게 된건데 break 에도 이름을 지어줄 수 있었다..<br>

```java
package pm;
public class Ex10_break_label {
	public static void main(String[] args) {
		bk:for (int i = 0 ; i < 4 ; i ++) {
			for (int j = 0 ; j < 5 ; j ++) {
				System.out.printf("%-2d" , j+1);
				// 3의 배수를 만나면 반복문 탈출
				if ( (j+1) %3 ==0 ) {
					break bk; // label을 붙이면 for(1) 문을 탈출한다
				}
			} // end of for(2)
			System.out.println();
		}// end of for(1)
	}
}
```
만약 종료시킬 반복문이 있다면 앞에 사용할 이름: 이렇게 쓰면 해당 반복문을 탈출 할 수 있다<br>