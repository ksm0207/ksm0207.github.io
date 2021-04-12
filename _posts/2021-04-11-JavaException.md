---
title: Java 예외처리
author: Kim
date: 2021-04-11 19:30 +0900   # 2019-08-20 19:34:00 0900
categories : ["Java", ""]
tags: [Java,null]
comments : true
---

# 예외처리

예외처리는 프로그램 실행 시 발생할 수 있는 예기치 못한 ``` 예외의 발생에 대비한 코드 ``` 를 말합니다<br>
즉 예외처리 는 예외의 발생으로 인한 실행중인 프로그램의 갑작스런 비정상 종료를 막고 정상적인 실행상태를<br>
유지할 수 있도록 하는 것 입니다<br>

```java
정수 이외에 다른 문자형을 입력받았을시 프로그램이 종료되지만
userAge = scan.nextInt();

try / catch 키워드를 사용하면 종료되지가 않습니다
```

예를들어 userAge 객체에 정수 이외에 다른 타입의 자료형을 입력하였을때 프로그램은 에러를 발생하면서<br>
종료되는게 일반적인데 예외처리를 해준다면 프로그램은 종료되지 않고 유지할 수 있게됩니다<br>
※ 예외처리를 사용할때 키워드는 ``` try / catch ``` 를 사용합니다<br>

* (1) 예시에 userAge에 정수 이외에 다른 문자가 입력되면 에러가 발생합니다 (Java에서 미리 구현된 예외 발생)<br>
* (2) 예외가 발생할 때는 적절한 예외처리를 해주지 않는다면 프로그램 이 그대로 종료됩니다<br>
* (3) 예외는 상황별로 여러가지 예외가 발생할 수 있습니다<br>
* (4) 자바에서는 예외를 던져진다 혹은 던저졌다 라고 하는 것으로 표현되며 이것을 throw 라고 합니다<br>

### 예외처리 종류는 다양하게 있다

* (1) InputMismatchException : 지정한 변수 타입과 다른 타입을 입력받았을 때 발생하는 예외

* (2) ArithmeticException : 0으로 나누려할 때 발생하는 예외

* (3) NullPointerException : 값이 null인 참조변수의 멤버를 호출하려고 할때 발생하는 예외

* (4) ArrayIndexOutOfBoundsException : 배열의 범위를 벗어났을 때 발생하는 예외

* (5) NumberFormatException : 문자를 숫자로 변환하려고 할 때 발생하는 예외

* (6) FileNotFoundException : 존재하지 않는 파일의 이름을 입력했을 때 발생하는 예외

* (7) ClassNotFoundException : 클래스 로딩에 실패했을 때 발생하는 예외

※ 출처: <a href = "https://ande226.tistory.com/24">[안디스토리]</a><br>

자바에서 이런 예외가 발생했다면 해결방법은 작성한 코드를 절차지향을 따르는지 체크한다음<br>
답이 안나온다면 위대한 구글링을 통해 해결하는 것이 가장 좋습니다<br>

# (1) InputMismatchException

### 지정한 변수 타입과 다른 타입을 입력받았을 때 발생하는 예외를 발생시켜 학습하기

간단한 예시로 Scanner로 정수를 입력받아야 하지만 다른 자료형 타입을 입력받았을때<br>
예외처리는 어떻게 해야하는지 알아보는 예제입니다

* 상황 1 : 예외처리를 처리하지 못했을때

```java
package BlogPost;
import java.util.Scanner;

public class InputNumber {

    public void print() throws Exception {

        System.out.println("정수만 입력하세요");
        Scanner scan = new Scanner(System.in);

        int value = scan.nextInt();

        System.out.println(value + "입니다");
    }
    public static void main(String[] args) throws Exception {
        InputNumber in = new InputNumber();
        in.print();
    }
}
---
정수만 입력하세요
190RR

Exception in thread "main" java.util.InputMismatchException ※ 의도한 예외 발생
	at java.base/java.util.Scanner.throwFor(Scanner.java:939)
	at java.base/java.util.Scanner.next(Scanner.java:1594)
	at java.base/java.util.Scanner.nextInt(Scanner.java:2258)
	at java.base/java.util.Scanner.nextInt(Scanner.java:2212)
	at BlogPost.InputNumber.print(InputNumber.java:11)
	at BlogPost.InputNumber.main(InputNumber.java:19)
```
위 코드는 정수만을 입력해야 하지만 정수 외 다른 자료형 타입을 입력해서 Java에서 에러를 알려줍니다<br>
에러메시지를 해석해보면 19번 main 에서 11번 라인을 실행시켰는데 여기에서 에러가 발생한 것 같으니<br>
확인한번 해보고 11번 라인의 윗줄에서 예외를 던지는 것 같아 라고 해석할 수 있습니다<br>

이제 우리가 만들 수 있는 예외처리 방법은 try / catch 키워드를 사용하는 것 입니다<br>

try 블럭 내에서 예외가 발생한다면 ?<br>

* (1) 발생한 예외와 일치하는 catch 블럭이 있는지 확인합니다
* (2) 일치하는 catch 블럭을 찾으면 이것을 실행하고 전체 try / catch 키워드 안을 빠져나간다음<br>
      실행시켜야 할 문장을 계속해서 수행할 수 있게 되고<br>
      만약 일치하지 않는 catch를 찾지못하면 처리되지 않습니다<br>


try 블럭 내에서 예외가 발생하지 않은 경우는?<br>
* (1) catch 블럭을 거치지 않고 try / catch 키워드를 빠져나가 수행을 계속합니다<br>

예시로 기재된 코드에서 사용자가 제대로 입력할 때 까지 while 반복문을 무한으로 돌린 코드입니다<br>

```java
package BlogPost;
import java.util.InputMismatchException;
import java.util.Scanner;

public class InputNumber {
    public void print(){
        Scanner scan = new Scanner(System.in);
        int value = 0;
        while (true){
            try {
                System.out.println("try 블럭에 오신것을 환영합니다.");
                System.out.println("정수를 입력해볼까요?");
                value = scan.nextInt();
                System.out.println("잘하셨습니다 입력한 값은 " +value + " 입니다 ");
                break;
            }catch (InputMismatchException errorRes) {
                System.out.println("-----------------------------");
                System.out.println("try 블럭에 예외가 발생했습니다. ");
                System.out.println("정수만 입력해주세요.");
                scan = new Scanner(System.in);
                System.out.println(errorRes); // 23 ~ 24 에러메시지 출력
                System.out.println(errorRes.getClass().getName() + " 예외처리된 내용 : " + errorRes.getMessage());
                System.out.println("-----------------------------\n");

            } // end of try / catch
        } // end of while
    } // end of InputNumber Class
    public static void main(String[] args) throws Exception {
        InputNumber in = new InputNumber();
        in.print();
    }
}
```

try 키워드안에 존재하는 코드들은 무조건 의도한 대로 실행되야 하는곳 입니다<br>
먄약 정수형 이 아닌 다른 자료형 타입을 입력했을 경우 try 키워드는 실행되지 않고 예외가 발생하게 됩니다<br>

```java
try {
System.out.println("try 블럭에 오신것을 환영합니다.");
System.out.println("정수를 입력해볼까요?");
value = scan.nextInt();
System.out.println("잘하셨습니다 입력한 값은 " +value + " 입니다 ");
break;
}
```
try 키워드 안의 코드가 InputMismatchException 예외를 던진다면<br>
바로 이곳에서 예외를 처리하게 됩니다 catch가 실행되는 동안은 프로그램이 종료되지 않습니다
```java
}catch (InputMismatchException errorRes) {
    System.out.println("-----------------------------");
    System.out.println("try 블럭에 예외가 발생했습니다. ");
    System.out.println("정수만 입력해주세요.");
    scan = new Scanner(System.in);
    System.out.println(errorRes); // 21 ~ 22 에러메시지 출력
    System.out.println(errorRes.getClass().getName() + " 예외처리된 내용 : " + errorRes.getMessage());
    System.out.println("-----------------------------\n");
}
※ 에러메시지를 제대로 출력해서 보려면 catch 의 매개변수인 errorRes 를 통해서 21~22번을 참고할 수 있습니다<br>
```

위 코드를 실행시킨 결과 <br>
```java
(1) Java의 절차지형 식 코드 읽기로 바로 try 키워드를 실행합니다

try 블럭에 오신것을 환영합니다.
정수를 입력해볼까요?
정수를 입력하고 싶지 않습니다 

(2) 예외발생 - 정수를 입력하고 싶지 않습니다

-----------------------------
try 블럭에 예외가 발생했습니다. 
정수만 입력해주세요.
java.util.InputMismatchException
java.util.InputMismatchException 예외처리된 내용 : null
-----------------------------

(3) 실행시켜야 할 문장을 계속해서 진행하게 되고 정수 입력 후 break로 종료

try 블럭에 오신것을 환영합니다.
정수를 입력해볼까요?
100
잘하셨습니다 입력한 값은 100 입니다 
```