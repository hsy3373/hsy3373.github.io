---
title: "[Oracle] SQL문법 8. DCL(GRANT, REVOKE)"
excerpt: "GRANT, REVOKE 기본 문법"

categories:
  - Oracle
tags:
  - [Oracle, SQL]

comments: true
toc: true
toc_sticky: true

date: 2020-12-28
last_modified_at: 2020-12-28
---

## DCL (DATA CONTROL LANGUAGE)

데이터를 제어하는 언어로 DB에 대한 보안, 무결성, 복구 등 DBMS를 제어하는 용도로 쓰인다  
※ 원래 데이터 정의어로 분류되었지만, 데이터베이스 제어기능이 중요해지고 다양한 제어 기능이 소개되면서 독립되었다

<br>

> ### 권한 종류

- 시스템 권한

  - 객체 생성, 변경, 소멸 등 DB의 생성과 관리 전반에 관한 권한으로 SYS(SYSTEM/관리자계정)에게 부여한다
  - 시스템 권한은 매우 강력한 기능을 가지므로 대부분 관리자나 개발자에게만 부여하도록 한다

- 개체 권한
  - 사용자가 특정 개체에 대해 특정 작업을 수행 가능하도록 일반 사용자에게 부여하는 권한이다

<br>

> ### GRANT

```sql
[표현법]
GRANT 권한|ROLE명칭 TO 사용자계정
```

사용자에게 권한(ROLE)을 부여하는 명령어
