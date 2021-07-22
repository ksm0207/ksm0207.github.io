---
title:  자바기반의 응용SW개발자 양성과정 11일차 - String 과 배열
author: Kim
date: 2021-07-20 06:00:00 +0900
categories : [Increpas]
tags: [Increpas]
---

# 오전시간

- String 클래스의 암시적 객체 생성 명시적 객체 생성
- Heap 영역에 어떻게 들어갈까?
- 내용비교 해보기

## String 암시적 명시적 생성 

```java
String s1 = "Test"; // 초기화 작업
                      // 암시적 객체생성
                      // String 객체게만 주어지는 객체 생성법

String s2 = new String("Test"); 
                     // 명시적 객체생성
                    // 객체들이 생성할 때 사용하는 생성법

String s3 = "Test"; // 암시적 객체생성                    
```

주소가 같은지 코드를 한번 돌려보았다<br>

```java
package am;

public class Ex1_String {
	public static void main(String[] args) {
		
		String s1 = "Test";
		String s2 = new String("Test");
		String s3 = "Test";
		
		System.out.println(System.identityHashCode(s1)); // 210 445 7164
		System.out.println(System.identityHashCode(s2)); // 152 111 8594
		System.out.println(System.identityHashCode(s3)); // 210 445 7164
		
		if (s1 == s2) {
			System.out.println("주소가 같다");
		}else {
			System.out.println("주소가 다르다");
		}
		if (s1 == s3) {
			System.out.println("s1 == s3 " + true);
		}else {
			System.out.println("s1 == s3" + false);
		}
	}
}

출력

주소가 다르다
s1 == s3 true
```

위 코드를 그림판으로 직접그리면 다음과 같은 구조가 나온다<br>

<img src = "/post/Java/string.png"><br>


- 암시적 객체생성 : Heap 영역에 등록하려 할때 똑같은 문자열이 있다면 이미 존재하는<br>
                    메모리 주소로 찾아가게 되고 메모리 관리의 효율성이 높아진다<br>

- 명시적 객체생성 : Heap 영역에 "새롭게" 별도로 생성하게 된다 이 말은 메모리 주소도<br>
                    새로 등록된다는 얘기가 된다<br>


암시적 과 명시적 의 차이는 아래 코드만 봐도 바로 알수있다<br>

```java
String s1 = "Test";
String s2 = new String("Test");
String s3 = "Test";
		
System.out.println(System.identityHashCode(s1)); // 210 445 7164
System.out.println(System.identityHashCode(s2)); // 152 111 8594
System.out.println(System.identityHashCode(s3)); // 210 445 7164
```
주석으로 처리된 숫자들은 객체들의 참조값을 나타낸다 이걸 콘솔로 확인하면 16진수값이 나와<br>
System.identityHashCode() 여기에 객체를 전달하면 10진수로 반환해서 나온 숫자이다<br>

<a href ="/posts/obrAddress/">자바 객체 주소값 확인</a> 에서 다뤘던 내용이었는데<br>

공부해봤던 것을 다시 응용해볼 수 있어서 메모리의 개념이 어느정도 잡혀가는 것 같다<br>

객체의 내용을 비교하려면 equals 메소드로 확인할 수 있다

```java
if (s1.equals(s2)) {
        System.out.println(" 같은 내용 입니다.");
}else {
    System.out.println(" 다른 내용 입니다.");
}
    
if (s2.equals(s3)) {
    System.out.println(" 같은 내용 입니다.");
}else {
    System.out.println(" 다른 내용 입니다.");
}
```

만약 이런 경우면 어떻게 처리해야 할까?<br>

```java
String s1 = "TEST";
String s2 = new String("Test");

```

s1 변수는 대문자 이고 s2 에는 소문자 이다 대소문자를 비교할땐<br>
equalsIgnoreCase() 메소드를 활용하여 내용을 비교할 수 있다<br>

```java

// 대소문자 비교
if (s1.equalsIgnoreCase(s2)) {
    System.out.println(" 같은 내용 입니다.");
}else {
    System.out.println(" 다른 내용 입니다.");
}

출력

같은 내용 입니다.
```

※ 비밀번호 체크할때 사용하면 좋을 것 같다.<br>

## String 클래스가 가지고 있는 기능들 활용

- 입력을 받고 문자열의 길이를 체크한다
- 문자열에 숫자가 포함되었다면 이를 알려주는 프로그램을 만들자

같이 실습한 코드 <br>

```java
package am;

import java.util.Scanner;

public class Ex2_String {
	public static void main(String[] args) {
		 // 1. 입력한 길이를 체크하기
		
		Scanner scan = new Scanner(System.in);
	
		String str = scan.next();
		int val = str.length();

		// 2. 숫자 포함 체크
		for (int i = 0 ; i < val ; i ++) {
			
			char ch = str.charAt(i);
			if (ch >= '0' && ch <= '9') {
				System.out.println("문자에 숫자가 포함되었습니다");
				break;
			} 
		}
	}
}
```

문자열 역시 유니코드 이기때문에 String 클래스의 charAt() 메소드를 활용하여<br>
숫자를 체크해줄 수 있는 방법을 배웠다<br>

구글링 하다가 찾게된 메소드 matches() <br>

```java
package am;

import java.util.Scanner;

public class Ex2_String2 {
	public static void main(String[] args) {
		
		Scanner scan = new Scanner(System.in);
		String s = scan.next();

		for (int i = 0 ; i < s.length() ; i ++) {
			if (s.matches(".*[0-9].*")) {
				System.out.println("입력한 길이 :" + s.length());
				System.out.println("숫자가 포함되었습니다");
				break;
			}else {
				System.out.println("입력한 길이 :" + s.length());
				System.out.println("숫자가 포함되지 않았습니다");
				break;
			}
		}
	}
}
```

- matches() 정규식을 이용해서 문자열을 검색해주는데 특정 문자열을 검색할때 사용하기 보다<br>
            한글 + 숫자 + 등과 같은 해당 문자열이 존재하는지 사용하는것이 좋다고한다<br>

- 반환형 : 포함하면 true 미포함 이면 false


# 오후시간


(1) 문제<br>

```java
package pm;

import java.util.Scanner;

public class Ex2_String {
	public static void main(String[] args) {
		
		// 1. 키보드로 부터 한줄의 문자열을 입력받는다
		// 2. 문자열 안에 숫자 이외의 값이 입력될 때는
		// 3. "숫자외 다른 값을 입력하시면 안됩니다."
		// 4. 숫자들로만 이루어졌다면 "정확한 입력값이 맞습니다 출력"
		
		Scanner scan = new Scanner(System.in);
		String s = scan.nextLine();
		String res  = "";
		
		for (int i = 0 ; i < s.length() ; i ++) {
			char ch = s.charAt(i);
	
			if (ch >= 'a' || ch <= 'Z') {
				res = "숫자 외 다른 값을 입력하시면 안됩니다.";
				break;
			}else{
				res = "정확한 입력이 맞습니다";
				break;
			}
		}
		System.out.println(res);
	}
}
```

숫자 외의 다른 입력값을 받으면 안되고 숫자만 받을 수 있도록 하는 프로그램을 위 코드처럼 짜봤는데<br>
강사님이 직접 짠 코드는 아래코드와 같다, 내가 더 많이 공부하고  좀 더 많이 노력해야겠다는 생각이들었다..<br>

```java
package pm;

import java.util.Scanner;

public class Ex2_String {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		String str = scan.nextLine();
	
		int len = str.length();
		boolean chk = false;
		
		for (int i = 0 ; i < len ; i ++) {
			
			char ch = str.charAt(i);
			
			// 숫자가 아닌 것을 가려낸다.
			if (ch < '0' || ch > '9') {
				// 숫자가 아닌 경우를 만났으니
				// 더이상 반복문을 수행할 필요가 없다
				chk = true;
				break;
				// 반복문을 최소화 시킨 방법
			}
		}
		if (chk) {
			System.out.println("잘못된 값 입니다");
		}else {
			System.out.println("정확한 입력입니다");
		}
	}
		
}
```

강사님이 구현한 코드는 반복문을 최소화를 해서 결과를 내신건데<br>
아마 우리한테도 이런 방법도 있다 라는걸 알려주신 것 같았다<br>
확실히 내가 구현한 코드는 if 문에서 많은 데이터를<br>
하나씩 비교하다보니 돌아가긴해도 최소화 시키진 못한게 맞다<br>

다시확인 해보는 내 코드 중 반복문 과 비교문<br>

```java
for (int i = 0 ; i < s.length() ; i ++) {
    char ch = s.charAt(i);

    if (ch >= 'a' || ch <= 'Z') {
        res = "숫자 외 다른 값을 입력하시면 안됩니다.";
        break;
    }else{
        res = "정확한 입력이 맞습니다";
        break;
    }
}
System.out.println(res);
}
```

강사님 코드 <br>

```java
for (int i = 0 ; i < len ; i ++) {
    char ch = str.charAt(i);
    if (ch < '0' || ch > '9') {
        chk = true;
        break;
    }
}
    if (chk) {
        System.out.println("잘못된 값 입니다");
    }else {
        System.out.println("정확한 입력입니다");
    }
```



## 배열

- 자바에서는 배열을 객체로 인식한다.

배열을 만들떄는 3가지가 있다<br>

- (1) 배열선언

```java
int [] ar;
```

- (2) 배열생성

```java
ar = new int [3];
```

- (3) 배열 초기화

```java
ar[1] = 200;
ar[0] = 100;
ar[2] = 200;
```

위 그림을 표현하면 다음과 같다<br>

<img src = "/post/Java/array1.png"><br>

배열을 다음의 값으로 초기화를 해주었다<br>

- ar[0] = 1000
- ar[1] = 2000
- ar[2] = 3000

```java
for (int i = 0 ; i < ar.length ; i ++) {
    ar[i] = (i+1) * 1000;
    System.out.println(ar[i]);
}
```
(i+1) * 1000 이 부분으로 초기화 해준게 핵심이다..<br>
※ 배열의 길이는 length 로 정해주는게 유지보수에 좋다고 하셨다<br>