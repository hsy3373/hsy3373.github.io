---
title: "Java 문법 7. 추상클래스(abstract class) 와 인터페이스(interface) "
excerpt: "Java 추상클래스와 인터페이스의 이해"

categories:
  - JavaGrammar
tags:
  - [Java, Grammar]

comments: true
toc: true
toc_sticky: true

date: 2020-12-01
last_modified_at: 2020-12-04
---

## 추상클래스(abstract class)

> ### 1. 추상 클래스란

- 미완성된 클래스로 반드시 `abstract` 키워드를 붙여준다
- 선언되어있지만 구현되지 않은, 미완성의 메소드(추상 메소드)를 포함하고 있는 클래스
- 클래스로서의 <u>객체 생성이 불가</u>하다
- 부모 클래스로 이용 가능하다(상속 가능)
