---
title:  자바기반의 응용SW개발자 양성과정 10일차 - 제어문 마무리 + 클래스
author: Kim
date: 2021-07-20 06:00:00 +0900
categories : [Increpas]
tags: [Increpas]
---

# 오전시간

## 별찍기

```java
package increpas_example0719;
public class Ex8_MultiFor {
	public static void main(String[] args) {
		// 별찍기 (숙제)
		
		// *
		// * *
		// * * *
		// * * * *
		// * * * * *
		for (int i = 0 ; i < 5 ; i ++) {
			for (int j = 0 ; j <= i; j ++) {
			
				System.out.print("* ");
			}// end of for loop(2)
			System.out.println();
		}// end of for loop(1)
	}
}
```
위에 별찍기는 중첩for문의 이해를 한다면 쉽게 풀수 있는 문제다<br>
바깥쪽 for문은 행 을 담당하는 부분인데 왜 행이되는지 이해하려면 i를 먼저 찍어주자<br>
```java
for (int i = 0 ; i < 5 ; i ++) {
    System.out.println(i);
}

출력
0
1
2
3
4
```
그 다음 별을 찍어줘야 하는데 각 행에 값을 넣어.. 일단 정지 !!

## 별찍기 2

```java
package am;

public class Ex1_MultiFor {
	public static void main(String[] args) {
		// [결과]
		//   * * * * *
		//     * * * *
		//       * * *
		//         * *
		//           *
		String res = "";
		for (int i = 0 ; i <= 5 ; i ++) {
			
			for (int j = 1 ; j <= 5; j ++ ) {
				res = (i < j) ?  ("* ") : ("  ");
				//System.out.print("i 값 = "+i);
				//System.out.println(" j 값 = "+j);
				System.out.print(res);
			}// end of for loop(2)
			System.out.println();
		}// end of for loop(1)
	}
}

출력

* * * * * 
  * * * * 
    * * * 
      * * 
        * 
          

```

※ 삼항연산자로 i 가 j보다 작다면 true 에는 별을 찍고 false 에는 공백을 넣어준다<br>

i값과 j값 연산은 다음과 같다<br>
```java
* i 값 = 0 j 값 = 1
* i 값 = 0 j 값 = 2
* i 값 = 0 j 값 = 3
* i 값 = 0 j 값 = 4
* i 값 = 0 j 값 = 5
 
  i 값 = 1 j 값 = 1
* i 값 = 1 j 값 = 2
* i 값 = 1 j 값 = 3
* i 값 = 1 j 값 = 4
* i 값 = 1 j 값 = 5
 
  i 값 = 2 j 값 = 1
  i 값 = 2 j 값 = 2
* i 값 = 2 j 값 = 3
* i 값 = 2 j 값 = 4
* i 값 = 2 j 값 = 5
 
  i 값 = 3 j 값 = 1
  i 값 = 3 j 값 = 2
  i 값 = 3 j 값 = 3
* i 값 = 3 j 값 = 4
* i 값 = 3 j 값 = 5
 
  i 값 = 4 j 값 = 1
  i 값 = 4 j 값 = 2
  i 값 = 4 j 값 = 3
  i 값 = 4 j 값 = 4
* i 값 = 4 j 값 = 5
 
  i 값 = 5 j 값 = 1
  i 값 = 5 j 값 = 2
  i 값 = 5 j 값 = 3
  i 값 = 5 j 값 = 4
  i 값 = 5 j 값 = 5
```

## 홀수 짝수 게임


# 오후시간

## String - next() 와 nextLine() 차이

- next()     : 문자열을 공백을 기준으로 한 단어 또는 한 문자씩 입력받고<br>
               엔터값을 제외한다<br>

- nextLine() : 문장 한라인 전체를 입력받는다.<br>

## String 클래스 알아보기

- 자바에서는 문자열을 객체로 인식한다<br>

```java
String str = ""; // 초기화 작업
                // 암시적 객체생성
                // String 객체게만 주어지는 객체 생성법
		

String s1 = new String("거북이"); 
                // 명시적 객체생성
                // 객체들이 생성할 때 사용하는 생성법
```

※ 암시적 객체생성이 가능한 이유 - 자주 사용해서 <br>


String 객체가 서로 다른이유<br>

※ 객체 비교는 주소비교이다<br>

```java
package pm;

public class Ex3_String {
	public static void main(String[] args) {
		
		String str = ""; // 초기화 작업
		                 // 암시적 객체생성
		                 // String 객체게만 주어지는 객체 생성법

		String s1 = new String("거북이"); 
					     // 명시적 객체생성
						 // 객체들이 생성할 때 사용하는 생성법
		if (str == s1) {
			System.out.println("서로 같다");
		}else {
			System.out.println("서로 다르다");
		}
		
	}
}
```
<a href="https://docs.oracle.com/javase/8/docs/api/index.html">자바 API 문서 </a><br>