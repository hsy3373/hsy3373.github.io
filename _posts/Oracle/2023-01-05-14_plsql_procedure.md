---
title: "[Oracle] PL/SQL문법 14. PROCEDURE 와 FUNCTION 기본문법 "
excerpt: "PROCEDURE 기본 문법"

categories:
  - Oracle
tags:
  - [Oracle, SQL, PL/SQL]

comments: true
toc: true
toc_sticky: true

date: 2023-01-05
last_modified_at: 2023-01-05
---

## PROCEDURE

PL/SQL 구문을 <u>저장</u>해서 이용하게 하는 객체이다  
필요할 때마다 복잡한 구문을 다시 입력할 필요 없이 간단하게 호출 가능하게끔 해준다

<br>

> ### PROCEDURE 생성

```sql
[표현법]
CREATE [OR REPLACE] PROCEDURE 프로시져명[(매개변수)]
IS
BEGIN
  실행부
END;
/

[이후 실행 방법]
EXEC 프로시져명;

-- 예시
CREATE PROCEDURE DEL_A_TABLE
IS
BEGIN
  DELETE FROM A_TABLE
  COMMIT;
END;
/

EXEC DEL_A_TABLE;
```
