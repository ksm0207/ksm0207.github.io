---
title: 재귀호출 알고리즘 알아보기

author: Kim
date: 2021-05-20 23:53 +0900   # 2019-08-20 19:34:00 0900
categories : ["java"]
tags: [Java,null]
comments : true
---

# 재귀 알고리즘 기초





# StackOverFlow Error

```java
package Math;

public class Recursion {
	public static void main(String[] args) {
		
		RecurstionTest();
		
	}
	
	public static void RecurstionTest() {
		
		System.out.println("안녕하세요 ?1");
		RecurstionTest();
	}
}
실행결과 : Exception in thread "main" java.lang.StackOverflowError 발생

```


# 테스트 1

```java
package Math;

import java.util.Scanner;

public class Recursion {
	public static void main(String[] args) {
		
		Scanner scan = new Scanner(System.in);
		
		int input = scan.nextInt();
		
		RecurstionTest(input);
		
	}
	
	public static void RecurstionTest(int value ) {
		//	                              ▲ 매개변수
		
		if (value == 0) {
			System.out.println("코드가 종료되는 BaseCase 입니다 " + value);
			return ;
		}else {
			System.out.println("안녕하세요 ? " + value);
			// ▼ value -1 에 해당하는 값을 매개변수로 전달
			RecurstionTest(value -1 );
	
		}
		
	}

}
```