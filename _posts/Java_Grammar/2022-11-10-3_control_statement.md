---
title: "Java 문법 3. Control statement(제어문)"
excerpt: "Java 제어문의 이해"

categories:
  - JavaGrammar
tags:
  - [Java, java-grammar]

comments: true
toc: true
toc_sticky: true

date: 2020-11-10
last_modified_at: 2020-11-10
---

## Control Statement(제어문)

<br>

> ### 1. 조건문

조건을 달아 선택적으로 실행시키고자 할 때 사용하는 제어문

#### if 문

```java
if(조건식1) {
수행될 문장;
} else if(조건식2) {
수행될 문장;
} else if(조건식3) {
수행될 문장;
} else {
수행될 문장;
}
```

위와같은 방식으로 사용하며 제일 위에 있는 조건식부터 순차적으로 실행된다  
위에서부터 조건식을 실행시키며 내려오다 결과값이 true인 조건식을 만나면 그 안의 문장을 수행시킨 후 종료되며 나머지 조건식들은 실행되지 않는다  
여기서 `else {}`는 앞의 조건식들에 해당하는 경우를 제외한 모든 경우를 뜻한다

#### switch 문

```java
switch(조건식) {
  case 값1:
    수행될 문장;
    break;
  case 값2:
    수행될 문장;
    break;
  default:
    수행될 문장;
}
```

위와 같은 방식으로 사용하며 if문과는 다르게 shwitch의 조건식은 true/false값만이 아닌 정수나 문자열 등 <ul>다른 자료형들도 들어갈 수 있다</ul>
