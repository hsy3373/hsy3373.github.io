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

<br>

#### [ if 문 ]

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

- 위와같은 방식으로 사용하며 제일 위에 있는 조건식부터 순차적으로 실행된다
- 위에서부터 조건식을 실행시키며 내려오다 결과값이 true인 조건식을 만나면 그 안의 문장을 수행시킨 후 종료되며 나머지 조건식들은 실행되지 않는다
- 여기서 `else {}`는 앞의 조건식들에 해당하는 경우를 제외한 모든 경우를 뜻한다

<br>

#### [ switch 문 ]

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

- 위와 같은 방식으로 사용하며 if문과는 다르게 <u>shwitch의 조건식은</u> true/false값이 아닌 정수, 문자, 문자열과 같이 <u>다른 자료형들이 들어갈 수 있다</u>
- 조건식 하나로 많은 경우의 수를 처리할 때 사용한다
- 조건식의 결과값과 일치하는 `case문`으로 이동하여 그 안의 코드를 실행한다
- 주의! 각 case문 안에 `break;`가 없다면 <u>switch문이 종료되지 못하고</u> 계속해서 돌며 다른 case들 안의 코드들을 실행하고 break;를 만날때까지 혹은 switch문의 끝까지 계속된다
- 만약 조건식의 결과값과 일치하는 case문이 없다면 default문 안의 코드가 실행된다
