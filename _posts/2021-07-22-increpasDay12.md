---
title:  자바기반의 응용SW개발자 양성과정 12일차 - 배열
author: Kim
date: 2021-07-22 06:00:00 +0900
categories : [Increpas]
tags: [Increpas]
---

# 오전시간


## 배열의 난수값을 넣고 중복값 제거하기.

1 ~ 9 난수를 발생해야 한다 I 번째보다 앞에있는 모든 요소 들의 값을 비교한다<br>
비교시 같은 값이 있다면 난수를 다시 발생하여 I번째에 대입한다<br>

- 난수를 받는 for 문 하나
- 비교를 하는 for 문 둘

<strong>직접 구현해봤던 코드</strong><br>

```java
package personal_study;

public class Ex7_Array {

	public static void main(String[] args) {
		 // 도전문제
		
		// 정수 3개를 저장할 수 있는 배열을 만든다
		// 1 ~ 9 까지의 값들 중 난수를 발생한다
	    // 중복을 허용하면 안된다
		
		int [] array = new int [3];
		boolean flag = true;

		for (int i = 0 ; i < array.length;  ) {
			array[i] = (int)(Math.random()* 10) +1;	
			flag = true;

			for (int j = 0 ; j < i ; j ++) {
				if (array[i] == array[j]) {
					flag = false;
					System.out.println("중복값이 존재합니다 " + array[i] + " i 진행 횟수 : " + i);
					break;					
				}
			}// end of for loop(2)
			if (flag) {
				i++;				
			}
		} // end of for loop(1)
		// 출력
		for (int i = 0 ; i < array.length; i ++) {
			System.out.println("array[i] ===== > " + array[i]);
		}
	}
}
```

<strong>강사님 코드</strong><br>

```java
package pm;

public class Ex7_Array2 {
	public static void main(String[] args) {
		
		int [] ar = new int [3];
		// 1 ~ 9 중 난수 발생하여 배열의 각 요소에 저장하는 반복문
		for (int i = 0 ; i < ar.length ;) {
			
			// 난수 발생과 배열에 대입
			ar[i] = (int)(Math.random()*9 + 1);
		
			boolean chk = false;
			
			// 중복된 값이 있는지 판단하는 반복문
			for (int j = 0 ; j < i ; j ++) {
				
				// 현재 배열의 i번째 요소와 그 이전의 요소들을 비교하여
				// 같은 값이 있는지 찾아준다
				
				if (ar[i] == ar[j]) { // ar[i] == ar[0]
					chk = true;
					System.out.println("중복값 발생 : " + ar[i] + " " + ar[j]);
					break;
				}
			}
			if(!chk) { // 같은 값이 있다는 것을 판단(chk true 일때)
			 i++;      // 즉 같은 값이 있을 때는 i 값이 증가하면 안된다    
			}          // chk 가 false를 유지할 때만 i값 증가해야한다.
			           // chk 가 flase 이면 반대값인 true 로 인식한다
		}
		
		for (int i = 0 ; i < ar.length ; i ++) {
			System.out.println(ar[i]);
		}
	}
}
```

## String 객체 연습

