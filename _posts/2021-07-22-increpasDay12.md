---
title:  자바기반의 응용SW개발자 양성과정 12일차 - 배열 , String 클래스 , StringBuffer , Calendar 
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

# 오후시간

## String - 불변적특징

- String은 불변적 특징을 가지고 있다 
- 값을 절대 바꿀수 없도록 되어있다.

아래 코드를 보자 str 과 str2는 각 INCREPAS! 값을 가지고 있다<br>

```java
String str = "INCREPAS!"; 
String str2 = "INCREPAS!";
```
먼저 주소의 값을 비교하면 다음과 같다<br>

```java
if (str == str2) {
System.out.println("같은 주소입니다");
출력
같은 주소입니다
```

그렇다면 str 참조변수에 "INCREPAS!" 가 들어있다 이 문장 중 '!' 를 '#'으로 바뀌려면<br>
어떤 메소드가 필요했을까 ? 바로 replace () 메소드를 사용하면 됐었다<br>

문자열을 바꾸고나서도 str 과 str2는 같은 주소를 나타낼까 ?<br>
```java
System.out.println(str.replace("!", "#") == str2);
```

답은 false를 나타낸다 그 이유는 그림으로 표현 해 보았다<br>

<img src = "/post/Java/string4.png"><br>



## StringBuffer

- 문자열 편집이 용이한 클래스

- String 클래스 와 StringBuffer 클래스는 움직임이 다르다

※ 자료형 타입이 다르기 때문<br>

그럼 여기서 String 'Buffer' 는 무엇을 의미하는걸까 ?<br>

- Buffer : 임시 기억 장소 라는 개념이다

즉 내부에서 문자열을 처리하는 것 이며 append() or insert() 메소드 등 호출하면<br>
수정작업을 해준다고 이해하면 된다<br>

```java
StringBuffer sb1 = new StringBuffer("1.문자열");
StringBuffer sb2 = sb1;
```

위 둘의 객체 주소는 같은 곳에 있을까 아니면 다른곳에 있을까?<br>

답은 같은 주소에 속한다<br>

```java
if (sb1 == sb2) {
	System.out.println(true);
}else{
	System.out.println(false);
}
System.out.println(System.identityHashCode(sb1));
System.out.println(System.identityHashCode(sb2));

출력
1521118594
1521118594
```

이 클래스를 배우는 이유는 문자열을 수정해야 할 때가 있을때 사용해야한다고 이해했다<br>

만약에 아래와 같은 문자열을 합칠 수 있을까?<br>

```java
String str = "1.문자열";
		
str = str + 2 + ".문자열";
System.out.println(str);
```

출력은 1.문자열2.문자열 이렇게 나오지만 이 방법은 그다지 추천하지 않는 방법이라고 하셨다<br>

※ 문자열의 불변적 특징으로 인해 내부적 변경이 이루어 질수 없다<br>
※ 변경된 것 처럼 보이지만 사실 변경된 것이 아니라 새롭게 객체가 생성된 것이다<br>

왜 안좋은지 강사님의 그림을 보고 다시 그려보았는데 결과는 다음과 같다<br>

<img src = "/post/Java/string5.png"><br>

한번 문자열을 합치는 작업은 str +2 + ".문자열" 이런 방법도 있지만 메모리 상에서는<br>
한번에 저런 많은 작업이 이루어질 수 있다고 하셔서 메모리의 효율성이 떨어지신다고 하셨다<br>
특히 JVM 입장에서 보면 한번에 많은 일이 이루어져야 하니 버거운 일을 하는 것 이라고 이해했다<br>

※ 회색으로 직선을 그린 부분은 메모리 상에서 소멸되는 점을 그려본 것 이다<br>

StringBuffer 에서 append () 기능과 insert 기능 등 예전에 알고리즘을 공부했을 떄 많이 사용해본<br>
기억이 있어서 그런지 다소 익숙했지만 여기서 toString() 메소드의 역활을 잘 알게되었다<br>

새로운 String 객체로 반환한다는 기능을 알게되서 앞으로도 필요할때 사용할 수 있을 것 같다<br>


## 날짜 구하기 - Calendar 클래스

- Calendar 클래스는 추상클래스 이기 때문에 new 하여 객체 생성이 불가능하다

- 상속받고 있는 GregorianCalendar 를 이용해야 하기 때문에 다음과 같은 메소드를 사용한다<br>

※ 참조변수 . getInstance() <br>

<a href = "https://moonong.tistory.com/10">Calendar 클래스 예제</a><br>

- 2021-07-22 문자열 만들기

문자열 편집에는 StringBuffer 라는 클래스가 있다 이것을 이용해서 만들어 보았는데<br>

내가 구현해본 코드는 다음과 같다.<br>

```java
Calendar cal = Calendar.getInstance();
		
int yy = cal.get(Calendar.YEAR);
int mm = cal.get(Calendar.MONTH); // 1월이 0으로 기억됨 
int dd = cal.get(Calendar.DAY_OF_MONTH); // 현재 월의 날짜

StringBuffer sb = new StringBuffer();
sb.append(yy + "-").append(  (mm+1 + "-") ).append(dd);
String res = sb.toString(); // StringBuffer 객체를 String 객체로 변환
System.out.println(res);
```

내가 놓친게 하나있었는데 문자열과 + 연산자를 사용해버린것<br>
이렇게 쓰면 메모리상에 문제가 될 수 있다고..<br>

강사님은 이런 방법을 권유하셨다<br>

```java
sb.append(yy);
sb.append("-");
sb.append((mm+1));
sb.append("-");
sb.append(dd);
```

자꾸 작은 차이때문에 실수하게 되는데 좀더 담부턴 더 꼼꼼하게 생각하고 코드를 짜자!<br>