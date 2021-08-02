---
title: 자바 컬렉션 프레임워크 - Collection Framework (List Set Map)
author: Kim
date: 2021-08-03 01:00:00 +0900
categories : [Java]
tags: [Java]
pin: true
---

# 컬렉션 프레임워크 

도움받은 참고자료 : <a href = "https://coding-factory.tistory.com/550">코딩팩토리 님</a><br>

※ Collection : 수집품 , 소장품<br>

※ Framework : 어떠한 구현을 재사용 가능하도록 협업화된 형태로 클래스를 제공한다<br>
              클래스 + 인터페이스 의 집합<br>

우리가 알고있는 배열에는 크기가 항상 고정적으로 지정한 후 데이터를 다루는데<br>
이런 문제는 비효율적인 문제라고 생각하게 된다 배열의 단점을 꼽아보자면<br>
크기가 항상 고정적 이라는 것 이다 만약 배열의 길이를 넘어서게 되면<br>

ArrayIndexOutOfBoundsException 이라는 예외내용을 맞서게 되거나<br>
배열요소에 데이터를 삭제하면 Index의 데이터는 비어있게되어 메모리가 낭비되는<br>
단점이 있다 하지만 자바에서는 배열의 이런 문제점을 해결하기 위해<br>

자료구조를 바탕으로 객체나 데이터들을 효율적으로 관리 할 수 있는 구조를 만들어놓았다<br>

그럼 데이터는 어떻게 관리한다고 하는걸까?<br>

- 추가
- 삭제
- 검색
- 저장

위 네가지를 합쳐만든 자료구조들이 있는 라이브러리를 `컬렉션 프레임워크` 라고 부른다<br>
대표적으로는 List Set Map Stack Queue 등 다양하게 많다<br>

<img src = "/post/Java/col.png"><br>
이미지 출처 : <a href ="https://coding-factory.tistory.com/550">코딩팩토리</a><br>

이제 List 부터 Set 그리고 Map 까지 차근차근 알아보도록 하자<br>

# List 컬렉션 프레임워크

List 컬렉션은 객체를 일렬로 늘어놓은 구조를 가지고 있다 이 컬렉션은 주로<br>
Index로 관리하기 때문에 객체를 저장하게 되면 자동으로 인덱스가 부여되며<br>

Index 값으로 객체를 검색하거나 삭제할 수 있는 기능을 제공한다<br>
※ 각 Index에는 데이터가 저장되어 있는 참조 값을 가지고 있는다<br>

List 컬렉션은 객체 `자체` 를 저장하는 것이 아닌 `객체의 주소값을 참조` 한다<br>
동일한 객체의 ` 중복을 허용하며 ` 중복이 허용된 객체들의 집합은<br>
동일한 주소값을 참조하고 null 값도 저장이 가능하지만<br>
Index는 참조하지 않는다<br>

List 컬렉션을 구현하는 대표적인 클래스는 다음과 같다<br>

- ArrayList

- LinkedList

- Vector

위 세가지 클래스는 List 인터페이스를 같이 상속하고 있으며 이 들은 공통적으로<br>
메소드를 사용한다 사용할 수 있는 메소드는 다음 과 같다<br>

```java

- boolean add(E e) : 객체를 `맨 끝` 에 추가한다

- void add(int index, E element) : Index에 객체를 추가한다

- set(int index, E element) : Index에 저장된 객체를 주어진 객체로 바꾼다

- boolean contains(Object o) : Index에 객체가 있는지 여부를 판단하며 true / false를 반환한다<br>

- E get(int index) : Index 의 저장된 객체를 리턴한다

- isEmpty() : Index 의 값이 비어있는지 여부를 판단하며 true / false를 반환한다

- int size() : 전체 객체의 `수` 를 리턴한다

- E remove() : Index 의 저장된 객체를 삭제한다

- void clear() : Index의 모든 요소를 삭제한다

```
## List 컬렉션 예제

<a href="/posts/List/">ArrayList + LinkedList  + Vector 클래스 활용예제</a><br>


# Set 컬렉션 프레임 워크





