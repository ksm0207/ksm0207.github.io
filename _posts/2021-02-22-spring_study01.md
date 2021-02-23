---
title: Spring 입문서 [기본편 01]
author: Kim
date: 2021-02-22 16:40 +0900   # 2019-08-20 19:34:00 0900
categories : ["Spring", ""]
tags: [Spring,null]
comments : true
---

# Spring 입문 첫번째 [프로젝트 환경설정]

## 주요 학습내용

* 프로젝트 생성하기
* 라이브러리 살펴보기
* View 환경설정
* 빌드하고 실행하기


# Part 01 : 준비

* Java 11 설치하기
<a href="https://www.oracle.com/java/technologies/javase-jdk11-downloads.html">Java 11 Downloads</a><br>
※ 오라클 계정이 있어야 다운로드를 가능해서 계정 만들고 설치를 진행합니다<br>


* IDE : Intellij 혹은 Eclipse 설치하기<br>

Downloads 1: <a href="https://www.jetbrains.com/ko-kr/idea/download/#section=windows">Intellij Downloads</a><br>
Downloads 2: <a href="https://www.eclipse.org/downloads/">Eclipse</a><br>

Intellij 설치완료. ★

※ 자신의 운영체재에 적절하게 설치하기

# Part 01-2 : 프로젝트 생성하기

옛날에는 Spring 프로젝트를 밑바닥 부터 시작해서 만들었다고 합니다<br>
하지만 오늘날에는 Spring Boot를 이용하여 편리하게 개발을 할수있도록 도와주는 사이트를 알아보았습니다<br>
※ Spring 기반 프로젝트 생성할때 아주 유용함 !

<a href="https://start.spring.io/">Sprin initializr </a>

* Project<br>

Maven VS Gradle 어떤걸 해야할까?<br>
먼저 Maven 이랑 Gradle 이 무엇인지 알아봤습니다 과거에는 필요한 라이브러리를 가져오고<br>
빌드하는 라이프사이클 까지 관리해주는 Tool 이라고 합니다 옛날에는 Maven 을 많이 했지만<br>
요즘에는 Gradle가 추세되는중 이라 하여 Gradle Project를 선택하였습니다

* Language - Java 선택

* Spring Boot - 여기에서는 버전을 선택하는곳 입니다 (SNAPSHOT + M1 은 아직 구현중인 버전 이라고 함)<br>
※ SNAPSHOT M1 은 아직 정식 릴리즈 버전이 아니라는 뜻<br>
정식릴리즈 버전중에 있는 2.3.9 버전을 선택합니다

* Project Metadata<br>

```
1 Group : com.example / 보통 기업명(도메인)을 적어주는곳 현재 학습이 목적이므로 아무렇게 지어줍니다
2 Artifact : demo / Builld 될때 어떠한 결과물이 나옵니다 이것 또한 위와 같이 진행합니다 (프로젝트명)
3 Name : demo / Artifact 명을 지을때 자동으로 필드에 값이 들어가져있습니다 건들필요 X
4 Description : Demo project for Spring Boot X
5 Package name : com.example.demo  X
6 Packaging : [Jar] [War] X
7 Java : [15] [11] [8]  버전에 맞게 선택

중요 ★ Dependencies - Spring 개발을 시작하는데 어떤 라이브러리를 사용할건지 선택하는것!!
       검색어에 spring Web 선택 (Spring Web 개발)
       HTML을 만들어주는 템플릿 엔진을 필요로하기 때문에
       Thymeleaf 검색 후 선택 (이건 회사마다 다를수있다고 합니다)

       결론 : Spring Web + Thymeleaf
```

Project Metadata를 모두 설정하였다면 GENERATE 버튼을 눌러주도록 합니다 <br>


# Part 01-3 : 프로젝트 구성파일

버튼을 누르면 ZIP 형식으로 파일을 다운로드 할수있는데 이것을 다운로드 하여 압축을 풀어주고<br>
IDE에서 파일 오픈후 build.gradle 을 선택하여 열어줍니다<br>
※ open as project 클릭<br>

프로젝트 폴더구성은 다음과 같습니다

```
.gradle
.idea // Intellij 가 사용하는 설정파일
gradle // gradle 폴더
========================
src
 main
   java // 소스파일 패키지가 있는곳
       MyApplication 
            |
        Application
  resources  // 자바 코드파일을 제외한 코드들이 들어가있는곳(XML + HTML 등등)
     static  ※ 자바 파일들을 제외한 파일은 resources 폴더 안으로!
     templates
     application.properties    

 test  // 테스트 코드와 관련된 소스코드들
   java
     MyApplication
          |
      Application
========================
.gitignore
build.gradle  ★ 버전설정과 라이브러리를 모아놓은곳

gradlew
gradlew.bat    추후 설명될 파일들
HELP.md       
settings.gradle
```
# build.gradle

```
Spring Boot 사이트에서 설정한 라이브러리 를 가져온것을 확인할수 있습니다
testImplementation 은 기본적으로 재공되어있는 라이브러리 를 뜻합니다

dependencies { 
	implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	testImplementation('org.springframework.boot:spring-boot-starter-test') {
		exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
	}
}

※ implementation 에서 라이브러리를 추가 하고싶을때
mavenCentral 이라는 기본적으로 공개된 사이트에서 다운받아 적용하는 방법이 있습니다

repositories {
	mavenCentral() 설정적용 하나의 도구
}
```

# Part 01-4 : 개발서버 구동하기

경로 : src / main / java / Applcation Folder/ Application 으로 이동하여 다음 소스코드를<br>
       확인해볼 수 있습니다

```
package myfirst_spring.study_spring;  // 패키지명

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication  # Spring 개발할때 필수로 넣어줘야 하는 어노테이션
public class StudySpringApplication {
                     Java의 가장 기본인 Main Method
              ▼       스타크래프트로 따지면 커맨드센터
	public static void main(String[] args) {          
		SpringApplication.run(StudySpringApplication.class, args);
              (1) 메인 함수가 실행되면 SpringApplication.run()을 실행하게됩니다
	}          ※ 현재 class StudySpringApplication 을 넣어준 상태
}
```

실행단축키 ```CTRL + Shift + F10 ``` 를 이용하여 시작해보면 터미널에서 다양한 메시지들이 올라오는데<br>
그중 아래 메시지를 확인하면 서버를 제공해주고 있다는 느낌이 옵니다<br>

```main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path''```

바로 ```localhost:8080 ``` 을 입력하여 시도해봤더니<br>

아래와 같은 화면이 나오면서 현재 ```TomcatWebServer```를 구동시켰다는걸 깨닫게 된 순간이었습니다
```
Whitelabel Error Page
This application has no explicit mapping for /error, so you are seeing this as a fallback.

Tue Feb 23 10:54:55 KST 2021
There was an unexpected error (type=Not Found, status=404). // 아직 아무것도 없어서 에러페이지 가 나온것
```
여기까지 오류없이 잘 진행됐다면 프로젝트 구성은 성공한것입니다<br>

그런데 왜 ```localhost:8080 ``` 에 접속할수가 있었을까요? 알아보니 ```@SpringBootApplication```이 TomcatWebServer를 내장하고 있기 때문에 가능했던 일 이었습니다

다음 포스팅 에는 라이브러리를 살펴보도록 하겠습니다 감사합니다.




