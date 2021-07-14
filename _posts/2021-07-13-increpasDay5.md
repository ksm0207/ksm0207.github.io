---
title:  자바기반의 응용SW개발자 양성과정 5일차 - 데이터베이스 모델링
author: Kim
date: 2021-07-12 10:30:00 +0900
categories : [Oracle,SQL]
tags: [Oracle,SQL]
---

# 데이터베이스 설계

- PK , FK 정리

모델링 도구 : ERwin (Tool)<br>

- 모델링 - 프로그램
- 요구사항 분석 - 요청자의 의도를 파악하여 분석 후 프로그램 개발 목표 
- 논리적 모델링 - 요구사항에 맞게 테이블이나 테이블 관계들이 논리적 이어야함<br>
  Column : 속성<br>

- 물리적 모델링 - 객체속성 , 식별자들을 테이블 , 컬럼 , 키등으로 변환

최종 구현 : SQL<br>



# 데이터 모델링

- 논리적 모델링

데이터베이스 구축의 요구분석 단계에 해당되고 Entity(객체 , 테이블 , 시퀀스) 에 필요한<br>
컬럼(속성) 들을 정의하고 관계를 이루기 위해 관련 작업을 포함해야 함<br>

- 물리적 모델링

데이터베이스 구축의 설계 단계에 해당됨 , 데이터 형식과 각종 제약조건이 이루어져있고<br>
Index 등을 설정하는 작업<br>



DB관계도는 ERD 라고 부르며 각 테이블의 관계를 다이어그램 으로 표현할 수 있습니다<br>



# MySQL - ERD

ERD로 첫 테이블 만들기 연습 입니다 먼저 만들어볼 테이블은 다음 과 같습니다<br>

- book_t   - 도서
- author_t - 저자
- sales_t  - 판매

먼저 Mysql 의 워크벤치 메뉴에서 ``` File --> New Model``` 을 눌러줍니다<br>
※ 단축키 : Ctrl + N<br>

<img src = "/post/Mysql/model.png"><br>

그럼 위와 같이 모델링 탭이 생기는데 시작하기전에 스키마 이름을 변경해주도록 하겠습니다<br>

※ 스키마 : DB 구조와 제약조건에 전반적인 명세를 기술한 것 , 즉 어떤 구조로 데이터가<br>
  저장되는지 나타낼 수 있는 데이터 구조 입니다<br>

<br>

원형을 이룬 접시모양에 마우스 우클릭을 눌러주면 팝업창이 나오는데요 , 여기서<br>
```Edit Schema ``` 를 눌러주면 아래와 같이 하단에 창이 생기고 이름을 변경해줍니다<br>

<img src = "/post/Mysql/model2.png"><br>



<img src = "/post/Mysql/model3.png"><br>


<br><br>

그럼 이름 변경 까지 끝났으면 이제  ```ADD Diagram``` 아이콘을 더블클릭 해볼까요?<br>
<img src = "/post/Mysql/model4.png"><br>

## ERD 작업을 시작하기<br>
<img src = "/post/Mysql/model5.png"><br>


- <strong>아래 이미지에서 보이는 것 처럼 동그미라 친 부분을 누르면 테이블 생성이 가능합니다</strong><br>

<img src = "/post/Mysql/model6.png"><br>

생성된 테이블을 더블클릭하면 아래화면에 컬럼을 설정할 수 있는 화면이 보입니다<br>
여기서 원하는 컬럼을 추가 및 설정 해줄 수 있습니다<br>


<img src="/post/Mysql/model7.png"><br>


## ERD 관계기호

<img src="/post/Mysql/model7.png"><br>

- ``` One```  : 1: 多 혹은 일대일 관계
- ``` Many```  : 多 : 多 관계
- ``` One(and only one)```  : 일대일 , 단하나의 row끼리 연결된 데이터
- ``` Zero or one```  : 1 : 多 혹은 1 : 1 관계
- ``` One or many```  : 1 : 1 or 多 : 多 관계는 갖고는 있지만 한개 아닌 여러개로 불확실 할때
- ``` Zero or many```  : 1 : 多 , 1 : 1 , 多 아예 없을수도 있고 불확실 할때


<br>


## 첫번째 ERD 테이블 완성

<img src="/post/Mysql/erd1.png"><br>

기존에 ```CREATE TABLE ``` 구문으로 테이블을 만들어봤다면 ERD로는 위와 같이 만들 수 있습니다<br>
앞으로도 이 방법으로 모델을 구현할 것 같습니다 . 이 상태에서 DB를 만들려면<br>
CTRL + G 키를 눌러 만들 수 있습니다<br>


<img src="/post/Mysql/erd2.png"><br>

그럼 이런 화면이 나오는데 설정할 건 없어서 Next를 눌러주다보면<br>
아래화면 처럼 나옵니다 ERD를 왜 쓰는지 그리고 한번 써본 후기는.. 정말 놀랍다는 말밖에..<br>

<img src="/post/Mysql/erd3.png"><br>

<strong>쭉쭉 진행하다보면 딱 봐도 성공했다는 표시가 보였습니다 그럼 이제 <br>
로그인 되어있는 계정으로 다시 돌아가서 SCHEMAS 를 새로고침 해줍니다 </strong>
<img src="/post/Mysql/erd4.png"><br>

<strong>ERD 그저 최고..</strong><br>
<img src="/post/Mysql/done.png"><br>

★ 이미지 width , height 크기 조절할 것.
