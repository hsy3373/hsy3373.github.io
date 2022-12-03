---
title: "Java 문법 7.  다형성 (polymorphism) 과 추상클래스(abstract class)"
excerpt: "Java 다형성과 추상클래스의 이해"

categories:
  - JavaGrammar
tags:
  - [Java, Grammar]

comments: true
toc: true
toc_sticky: true

date: 2020-12-01
last_modified_at: 2020-12-01
---

## 다형성 (polymorphism)

> ### 1. 객체지향개념에서의 다형성

- 객체지향 프로그래밍의 3대 특징 중 하나
- 여러가지 타입을 한가지 타입으로 처리할 수 있는 기술
- 자바에서는 한 타입의 참조변수로 여러타입의 객체를 참조할 수 있다  
  => 부모 클래스 타입의 참조변수로 자식클래스의 인스턴스 참조 가능
  => 자식 클래스 타입의 인스턴스를 생성할 때, 부모 클래스 타입의 참조변수 이용 가능

- 장점
  - 하나의 부모 타입으로 모든 자식 객체들을 받을 수 있다
  - 편리함, 코드 수 감소, 생산성 증대를 가져온다

<br>

> ### 2. 클래스 형변환

클래스 간의 형 변환은 반드시 상속관계에 있는 클래스끼리만 가능하다

- 업 캐스팅(Up Casting)

  ```java
  Parent p = new Child();
  //=> Parent p = (Parent) new Child();
  ```

  - <u>상속 관계</u>에 있는 클래스간에 부모타입의 참조형 변수가 모든 자식타입의 객체 주소를 받을 수 있다
  - 자동 형변환의 개념으로 부모타입으로의 형변환은 자동으로 되므로 생략이 가능하다

- 다운 캐스팅(Down Casting)

  ```java
  Parent p = new Child();
  p.printParent();
  ((Child) p).printChild();
  ```

  - 강제 형변환의 개념으로 자식타입으로의 형변환은 생략이 불가능하다
  - 반드시 후손타입을 명시해서 형변환을 진행해야 한다

<br>

> ### 3. 다형성 활용

- 객체배열

  ```java
  Parent[] pArr = new Parent[3];

  pArr[0] = new Child1();
  pArr[1] = new Child2();
  pArr[2] = new Child3();
  ```

  - 하나의 부모 클래스 타입 배열공간에 여러 종류의 자식 클래스 객체 저장 가능
