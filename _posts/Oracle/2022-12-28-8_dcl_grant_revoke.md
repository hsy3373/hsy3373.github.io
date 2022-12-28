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

> ### GRANT

```sql
[표현법]
GRANT 권한|ROLE명칭 TO 사용자계정
```

사용자에게 권한(ROLE)을 부여하는 명령어
