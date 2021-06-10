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
유지할 수 있도록 하는 것 입니다.<br>

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
(1) Java의 절차지형 코드 읽기로 바로 try 키워드를 실행합니다

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

# (2) ArithmeticException

### 예외적인 산술 조건이 발생할때 ```java.lang.ArithmeticException``` 

ArithmeticException 예외는 대표적으로 어떠한 ``` 수 ``` 를 0 으로 나누는 경우 발생합니다 ( /by zero)<br>
예시를 돕는 코드는 다음과 같습니다<br>

```java
package BlogPost;

import java.util.Scanner;

public class ArithmeticException{
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);

        int x = 0;
        int y = 0;
        double res = 0.0;

        System.out.println("첫번째 정수를 입력하세요");
        x = scan.nextInt();
        System.out.println("두번째 정수를 입력하세요");
        y = scan.nextInt();

        try {
            res = x / y;
            System.out.println(res);

        }catch (java.lang.ArithmeticException error){
            System.out.println("Error : "+ error.getMessage());
        }
    }
}
```

위 코드를 실행시킨 결과 <br>
```java
첫번째 정수를 입력하세요
1
두번째 정수를 입력하세요
0
Error : / by zero
```

# (3) NullPointerException

### 잘못된 Null 참조를 할 때 발생할때

NullPointerException 은 프로그램이 Null인 객체의 멤버에 접근하려 할 때 발생하는 예외상황을 말합니다<br>

```java
package BlogPost;

public class NullPointerException {

    public static void main(String[] args) {

        Person p = null;
        System.out.println(p.name);

    }
    class Person {
        String name;
        int age;
    }
}
```
위 코드에서 Person p = null 이라고 할당 된 값을 확인할 수 있습니다 이처럼 p 에 아무런 값을 할당하지 않는다면<br>
사실상 p는 무늬만 Person 이고 아무것도 접근할 수 없게 됩니다 코드실행 결과는 다음과 같습니다<br>
```java
Exception in thread "main" java.lang.NullPointerException
at BlogPost.NullPointerException.main(NullPointerException.java:8)
```

일반적으로 객체를 만들땐 Person p = new Person() 명령어를 사용하여서 Person객체를 만들 수 있고<br>
객체를 만들면 Person 을 위해 사용 할 공간을 메모리에 할당 한 후 래퍼런스를 p에 할당하라는 뜻이됩니다<br>

```java
Person p = new Person();
------------
|   main   | 
| Person p |          래퍼런스
|          |   ---> String name 
|          |         int   age
|          |
|----------|

p.name = "Kim";
p.age = ???;
```

하지만 Person p = null 로 할당하게 되면 p 에는 아무런 래퍼런스가 없어서 NullPointerException을 발생합니다<br>
즉 null로 할당한 p를 p.name 으로 접근한다면 잘못된 접근 이라고 볼수 있습니다<br>

이런 상황을 막기 위해서 객체가 null 일 경우 아래와 같이 체크할 수 있습니다<br>

```java
package BlogPost;

public class NullPointerException {
    
    public static void main(String[] args) {
        Person p = null;
        if (p == null) {
            System.out.println("is Null");
            return ;
        }else{
            System.out.println(p.name);
        }

    }
    class Person {
        String name;
        int age;
    }
}
실행결과 ▼
is Null
```
NullPointerException 은 추후 추가로 포스팅 될 예정입니다<br>


# (4) ArrayIndexOutOfBoundsException

### 잘못된 Index에 접근 : -  배열 Index 의 사이즈가 같거나 범위를 벗어날때 발생

배열을 사용하다 보면 종종 ```ArrayIndexOutOfBoundsException``` 이 발생하는 경우가 있습니다<br>
이것은 배열의 원소에 접근하다가 생긴 것 이며 다음 예제와 함께 해결방법을 알아보도록 하겠습니다<br>

```java
package BlogPost;
public class ArrayIndexOutOfBoundsException {
    public void print(int j){
        int [] arr = {1,2,3,4};
        System.out.println("Result = " + arr[j]);
        // Index [] :   0 1 2 3
        // int [] arr : 1 2 3 4
    }
    public static void main(String[] args) {
        ArrayIndexOutOfBoundsException arrException = new ArrayIndexOutOfBoundsException();
        arrException.print(4);
    }
}
실행결과 ▼

Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException:
Index 4 out of bounds for length 4
at BlogPost.ArrayIndexOutOfBoundsException.print(ArrayIndexOutOfBoundsException.java:5)
at BlogPost.ArrayIndexOutOfBoundsException.main(ArrayIndexOutOfBoundsException.java:11)
```

에러내용을 복습해보자면 12번 라인을 실행하였고 5번 위에 thorow를 던지고 있는 상황입니다<br>
5번라인 위에서 발생한 것은 Index 4 out of bounds for length 4 입니다 원인을 살펴보면 다음과 같습니다<br>

현재 int 타입의 배열 arr에  1,2,3,4 값을 넣은 뒤 ```파라미터 int j```를 받아 arr 배열의 ```j번째``` 값을 호출하고<br>
배열의 크기는 4 size 인데 호출하려는 값은 Index 길이를 초과하기 때문에 생긴 예외발생 입니다<br>

```java
int [] arr = {1,2,3,4} 는 Index ㅁ ㅁ ㅁ ㅁ 총 4 size 이지만
arrException.print(4) j번째를 구하려고 한다면
Index ㅁ ㅁ ㅁ ㅁ [ㅁ]?? 를 호출하는 것 과 같기때문에 Index 범위를 벗어남
```

이제 이런 예외가 발생했을 경우 에외처리 방법은 총 3가지가 있습니다<br>
* (1) try / catch 키워드 사용하기

먼저 (1) try / catch 키워드를 사용해서 예외처리를 알아보겠습니다<br>

```java
package BlogPost;

import java.util.Scanner;

public class ArrayIndexOutOfBoundsException {

    public void print(int j) {
        try {
            int [] arr = {1,2,3,4};
            System.out.println("Result : " + arr[j]);
        }catch(java.lang.ArrayIndexOutOfBoundsException error){
            System.out.println("Catch 발생");
            System.out.println("0 ~ 3 까지만 입력하십시오.");
            System.out.println(error.getMessage());
        }
    }

    public static void main(String[] args) {
        System.out.println("배열에 값을 넣어봅시다");
        ArrayIndexOutOfBoundsException arrException = new ArrayIndexOutOfBoundsException();
        Scanner scan = new Scanner(System.in);

        int val = scan.nextInt();
        arrException.print(val);
    }
}
실행결과 ▼
배열에 값을 넣어봅시다
3
Result : 4

배열에 값을 넣어봅시다
11
Catch 발생
0 ~ 3 까지만 입력하십시오.
Index 11 out of bounds for length 4
```
이 코드는 main에서 값을 입력받도록 하였고 파라미터 j는 ```int val = scan.nextInt()``` 정수를 받습니다<br>
그후 try 키워드 안에서 배열의 범위가 벗어나서 예외가 발생할 시 catch 키워드에 지정한 예외처리가 됩니다


# (5) NumberFormatException

### 문자를 숫자로 바꾸려고 할 때 발생하는 예외처리

NumberFormatException 을 읽어볼 때 이름에서도 유추할 수 있듯이 숫자가 아닌 타입을 정수형 으로 변환할때<br>
일어나는 것 입니다 보통 문자열을 int 형으로 변환할 때 사용할때 자주 일어나는 편 입니다 <br>

다음 예제는 main 에서 NumberFormatException 객체에 String 형으로 데이터를 보낸다음<br>
데이터를 받는 parseInt 멤버 메소드에는 try / catch 키워드를 통해 예외처리를 해보는 예제 입니다<br>

```java
package BlogPost;

import java.util.Scanner;

public class NumberFormatException {
    // by kim 

    public int parseInt(String str){
        try {
            System.out.println("Result : " + str);
            return Integer.parseInt(str);

        }catch (java.lang.NumberFormatException error){
            System.out.println("Catch 발생");
            System.out.println(error);
            System.out.println(error.getMessage());
            return 0;
        }
    }

    public static void main(String[] args) {
        NumberFormatException nfe = new NumberFormatException();
        Scanner scan = new Scanner(System.in);
        String strInput = scan.next();
        nfe.parseInt(strInput);
    }
}
```
실행결과는 다음 과 같습니다<br>
```java
123
Result : 123
```

Result = 123 은 return 할때 Integer.parseInt(str) 을 반환 하고 있기 때문입니다<br> 
Integer.parseInt() 메소드는 문자열 을 정수형 으로 변환 할 때 사용하고 알고리즘 문제 풀 때도 자주 사용됩니다<br>
데이터를 처리하는 과정은 str = "123" 을 정수형 123 으로 변환되어서 try 키워드 안에는 예외가 발생하지 않게 됩니다<br>

그럼 NumberFormatException은 어떻게 예외를 일으킬 수 있는지 알아보기 위해 입력을 다음과 같이 해주었습니다<br>

```java
123a
Result : 123a

Catch 발생
java.lang.NumberFormatException: For input string: "123a"
For input string: "123a"

```
아까와 같이 Intger.parseInt() 메소드를 통해 문자열을 정수형으로 변환 할 수 있었지만<br>
123a 를 입력 한 순간에 예외가 발생하였다고 catch 키워드가 알려주는 상황이 되어버렸습니다<br>

※ 123a는 숫자와 문자가 조합된 문자열이기 때문에 Intger.parseInt() 메소드가 제 역할을 못한 것 입니다<br>


# 정리

* (1) 의도치 않은 에러가 발생할때 해결책은 try / catch 키워드를 사용하여<br>
      원인을 알아낼 수 있습니다<br>

* (2) 에러메시지 가 발생하는 지점은 항상 아래에서 부터 시작하여<br>
   위로 올라가면서 예외를 던져주는 곳을 확인 할 수 있습니다<br>

* (3) try 키워드 내에서 예외가 발생하면 catch 키워드로 넘어가 실행시켜야 할 문장을 수행 할 수 있습니다<br>
    단 일치하지 않는 catch를 찾지 못하면 프로그램은 종료된다<br>

* (4) try 키워드 내에서 예외가 발생하지 않은 경우는<br>
      catch 키워드를 거치지 않고 try / catch 키워드를 빠져나가 다음 코드를 실행시킵니다<br>

* (5) 에러가 발생하면 검색을 통해 원인을 알아가는 것도 중요합니다 구글링 짱
