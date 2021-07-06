---
title: Java 설치하기 , JDK + 환경변수 테스트
author: Kim
date: 2021-07-06 16:14 +0900   # 2019-08-20 19:34:00 0900
categories : [Java]
tags: [Java]
comments : true
---

## 컴퓨터 32비트 & 64 비트 확인하기

※ 윈도우 기준<br>
<img src ="/post/JavaDownload/pc.png"><br>

설치전 컴퓨터 비트 알아보기 : ``` 내 PC  --> 오른쪽 마우스 클릭 --> 속성  클릭 ```

<img src = "/post/JavaDownload/pc_bit.png"><br>

※ 컴퓨터 비트를 먼저 알아 본 이유는 앞으로 설치 할 JDK버전 호환성 때문에 알아 보았습니다.<br>
※ JDK : 자바를 개발 할 수 있는 하나의 키트.


## Java 설치하기

자신의 컴퓨터 비트를 알아냈다면 오라클에 접속 해 줍니다.<br>
<a href="https://www.oracle.com/java/technologies/javase-downloads.html">

※ ```JDK 다운로드 하기 위해선 계정이 필요하므로 꼭 계정 생성을 해주세요``` <br>

(1) 선택 한 버전은 ``` Java SE 11 (LTS) ``` 이고 보라색 체크로 되어 있는 부분을 클릭 해 줍니다.<br>
<img src = "/post/JavaDownload/download_java.png">

(2) 그 다음 약간 스크룰을 내려 아까 확인했 던 자신의 비트에 맞는것을 찾아 다운로드를 진행 해 줍니다<br> 
<img src = "/post/JavaDownload/down_ing.png">

(3) 다운로드 파일을 열어보면 다음과 같은 창이 뜨게 되고 ```Next -> 클릭```<br>
<img src = "/post/JavaDownload/java_next.png">

(4) 그 다음은 JDK를 설치 할 경로를 지정 해 주는 것 입니다 , 기본경로를 사용하여 설치를 이어 진행 합니다<br>
※ 위 사진 의 경우 기본경로는 ``` C:\Program Files\Java\jdk-11.0.11\ ```<br>
※ 설치경로는 나중에 진행 할 환경변수 설정 , 이클립스 설정 시 필요로 합니다<br>
<img src = "/post/JavaDownload/java02_png.PNG">

(5)이어서 Next를 눌러주고 아래와 같이 사진이 나온다면 설치가 성공적으로 완료 된 것 입니다<br>
※ JRE 설정은 기본경로로 설치 해 줍니다.<br>

<img src ="/post/JavaDownload/java_suc.png">

여기까지 진행 해 왔다면 Java를 설치하는데 아무런 문제 없이 설치가 마무리 되었습니다<br>
그 다음은 환경변수 설정 하는 법을 알아보겠습니다<br>




## 환경변수 설정하기

```※ 시작 -> 제어판 -> 검색돋보기 -> 환경변수 입력 -> 시스템 환경 변수 편집 클릭 (방패 모양)```<br>
<img src ="/post/JavaDownload/path.png">


(1) 시스템 환경 변수 편집 클릭 후 ``` 환경 변수 ``` 버튼 클릭<br>
<img src ="/post/JavaDownload/path2.png">

(2) 그 다음 ``` 시스템 변수(S) ``` 에서 새로 만들기를 눌러 변수 이름을 만들어 줍니다<br>
<img src ="/post/JavaDownload/path3.png">
<img src ="/post/JavaDownload/path4.png">

* ※ 변수 이름 : JAVA_HOME (대문자 필수)<br>
* ※ 변수 값 : JDK가 설치 된 ``` 기본 경로 ``` 를 말합니다.<br>
* ※ JDK가 설치된 폴더로 들어가 경로를 복사하면 쉽게 처리 할 수 있습니다.<br>

★ 값이 잘 들어 갔는지 확인<br>

<img src ="/post/JavaDownload/path5.png">



(3) 이제 마지막 으로 ```시스템 변수(S)``` 안에 있는 ``` 변수 목록에 Path``` 를 더블클릭 해 줍니다<br>
그리고 ``` 새로 만들기``` 를 클릭하여 방금 생성한 변수 이름 : ```JAVA_HOME``` 을 붙여 줄 것 입니다<br>

※ Path 클릭<br>
<img src ="/post/JavaDownload/path6.png">

※ 새로 만들기 에서 ``` %JAVA_HOME%\bin ``` 입력
<img src ="/post/JavaDownload/path7.png">

(4) ```%JAVA_HOME%\bin``` 을 넣어 주고 확인을 누르면 이제부터 컴퓨터에 자바를 실행할 수 있는<br>
환경을 구축하였습니다 이제 테스트를 통해 정말 Java 가 잘 설치 됐는지 확인 해 보겠습니다<br>

(5) 테스트 안될 때 : 환경 변수 편집 --> 새로 만들기 --> ```C:\Program Files\Java\jdk-11.0.11\bin```<br>
    입력하고 가장 위로 이동시켜보기.<br>


## Java 실행 확인 테스트 

테스트 하는 방법은 간단합니다, 윈도우 + R을 눌러서 cmd를 입력 후 엔터를 쳐 보면<br>
다음과 같은 화면이 나오는데 이곳에서 테스트를 진행할 수 있습니다<br>

<img src ="/post/JavaDownload/final.png">


바로 테스트를 해 볼까요?<br>

* 명령어 : ```java -version``` <br>

<img src ="/post/JavaDownload/final2.png">

테스트 결과 자바를 사용할 준비가 모두 된 것 이라고 볼 수 있겠습니다.<br>
