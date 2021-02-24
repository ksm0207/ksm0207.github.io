---
title: Spring 입문서 [기본편 02]
author: Kim
date: 2021-02-22 17:40 +0900   # 2019-08-20 19:34:00 0900
categories : ["Spring", ""]
tags: [Spring,null]
comments : true
---



# [라이브러리 살펴보기]

## 주요 학습내용

*  <a href="https://ksm0207.github.io/posts/spring_study01/">프로젝트 생성하기</a>[ ● ]
* 라이브러리 살펴보기
* View 환경설정
* 빌드하고 실행하기


# Part 02 : 라이브러리 

지난 포스팅에는 프로젝트 생성과 함께 추가한 라이브러리 가 있었습니다
```
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-thymeleaf' HTML 엔진 라이브러리 
	implementation 'org.springframework.boot:spring-boot-starter-web' 웹 라이브러리
	testImplementation('org.springframework.boot:spring-boot-starter-test') default {
		exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
	}
}
```
단순히 추가한건 ```thymeleaf (1) ```  ```web(2) ``` 인데 알고보면 이것만 추가된게 아니였다는 사실을 알게되었습니다<br>
External Libraries를 열어보면 수 많은 라이브러리들이 모여있는데 그 이유가 무엇일까요?<br>
※ External Libraries는 사용할 외부 라이브러리를 가져오는것을 의미합니다

Gradle(Tool) 은 의존관계가 있는 라이브러리를 다운로드 하기 때문입니다 예를들어 ``` starter-web ``` 라이브러리를 가져오면
이에 필요한 라이브러리 들이 줄줄이 가져온다는것 입니다

음식레시피 처럼 메인으로 들어가는 음식이 있고 이어서 서브음식들을 넣어 요리를 만드는것 처럼요 ! <br>
즉 의존관계들을 다 가져오는것 입니다

* 예시 : Gradle : org.springframework.boot:spring-boot-starter-tomcat:2.3.9.RELEASE ...<br>
         ※ 위 라이브러리는 기본적으로 내장되어있는 서버입니다 


# Gradle

의존관계성 있는 라이브러리를 좀더 살펴보겠습니다<br>

먼저 IDE에서 화면 아래 왼쪽을 보면 다음과 같은 아이콘을 클릭해줍니다<br>
<img  style="" src = "/post/images/spring.PNG">
<br>

클릭후 화면 오른쪽 상단에  Gradle 아이콘을 눌러 라이브러리 목록을 확인할 수 있습니다<br>
<img  style="" src = "/post/images/spring2.PNG">

라이브러리중 * 이라고 표시된것은 중복을 제거해준다는 의미입니다<br>
이 과정은 한번쯤은 이런게 있구나 라는걸 살펴보면 좋을 것 같습니다


<h2> Spring Boot Libraries</h2>
* spring-boot-starter-web<br>
  spring-boot-starter-tomcat( 내장되어있는 웹서버)<br>
  spring-webmvc (스프링 웹 MVC 패턴)<br>

* spring-boot-starter-thymeleaf (Templates 엔진 = View)

* spring-boot-starter(공통적) : 스프링부트 + 코어 + 로깅 <br>
  spring-boot
        |
     spring-core<br>
  spring-boot-starter-logging
  logback, ...

<h2> Test Libraries</h2>

* spring-boot-starter-test<br>
  junit : 테스트 프레임워크<br>
  mockito : 목 라이브러리<br>
  assertj : 테스트 코드를 편하게 작성하게 도와줌<br>
  spring-test : Spring 통합 테스트 지원<br>




