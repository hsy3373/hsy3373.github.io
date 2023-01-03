---
title: "[Oracle] SQL문법 10. VIEW 와 SEQUENCE"
excerpt: "VIEW, SEQUENCE 기본 문법"

categories:
  - Oracle
tags:
  - [Oracle, SQL]

comments: true
toc: true
toc_sticky: true

date: 2023-01-03
last_modified_at: 2023-01-03
---

## VIEW (VIEW ORACLE OBJECT)

가상의 테이블(RESULTSET),  
SELECT문을 이용해서 실제 테이블으로부터 데이터를 가져와 가상의 테이블을 만든 것이다  
실제 테이블과는 다르게 실질적인 데이터를 저장하고 있진 않지만 사용자는 테이블을 사용하는 것과 동일하게 DDL구문을 이용하여 생성, 수정, 삭제 등 이용이 가능하다

- <a href="http://www.google.comhttps://hsy3373.github.io/oracle/4_subquery/#%EC%9D%B8%EB%9D%BC%EC%9D%B8-%EB%B7%B0" target="_blank">INLINE-VIEW</a> : FROM 절에 서브쿼리를 사용한 개념(다중열 다중행 서브쿼리)
- STORED-VIEW : 영구적으로 저장하고 사용하는 VIEW(서브쿼리를 가상테이블로 저장시켜둔 것)

<br>

> ### Transaction
