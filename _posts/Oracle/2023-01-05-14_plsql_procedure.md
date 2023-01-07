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

> ### 특징

- 처리속도가 빠르다
- 대량 자료처리 시 유리하다
- 잘 만든 프로시저에 한해서 유리한 것이지 무조건적으로 유리한 것은 아님
- DB자원을 직접 사용하기 때문에 DB자체에 부하를 주게 되므로 남용해서는 안된다
- 관리적 측면에서 JAVA등의 기타 언어 소스코드, 오라클 코드 동시에 형상관리하기가 어렵다
  - 프로시저는 SQL안에서만 관리가 가능하기 때문에 어디에선가 오류가 발생할 시 프로시저의 문제인지 다른 언어 소스코드들 중에서 문제가 난 것인지 파악하기 어려움

=> 결론 : 한번에 처리되는 데이터량이 많고 높은 성능을 요구하는 처리들은 대체로 DB상에서 처리하는 것이 성능측면에서 좋지만,  
소스관리(유지보수)/형상관리 측면에서는 자바 등의 기타 언어들이 더 좋을 수 있다

<br>

> ### PROCEDURE 생성(매개변수X)

```sql
[표현법]
CREATE [OR REPLACE] PROCEDURE 프로시저명 [(매개변수)]
IS
BEGIN
  실행부
END;
/

[이후 실행 방법]
EXEC 프로시저명;

-- 매개변수 없는 프로시저 예시
CREATE PROCEDURE DEL_A_TABLE
IS
BEGIN
  DELETE FROM A_TABLE
  COMMIT;
END;
/

EXEC DEL_A_TABLE;
```

- 프로시저 생성 시 원하는 동작을 넣어 생성할 수 있다
- 생성해둔 프로시저는 EXEC로 얼마든지 다시 불러와 실행시킬 수 있다
- `SELECT * FROM USER_PROCEDURES;` : 데이터 딕셔너리로 현재 유저의 프로시저들을 확인하는 구문

<br>

> ### PROCEDURE 생성(매개변수O)

```sql
-- 매개변수 있는 PROCEDURE 생성 예시
/* IN  : 프로시저 실행시 필요한 값을 받는 변수
   OUT : 호출한 곳으로 결과값을 되돌려주는 변수 */
CREATE PROCEDURE PRO_SELECT_TABLE( AID IN A_TAVLE.ID_COLUMN%TYPE
                                   ANAME OUT A_TABLE.NAME_COLUMN%TYPE,
                                   ABONUS OUT A_TABLE.BONUS_COLUMN%TYPE)
IS
BEGIN
  SELECT NAME_COLUMN, BONUS_COLUMN
    INTO ANAME, ABONUS
    FROM EMPLOYEE
    WHERE ID_COLUMN = AID;
END;
/

-- 매개변수 있는 PROCEDURE 사용예시
VAR A_NAME VARCHAR2(20);
VAR A_BONUS NUMBER;
/* 바인드 변수 선언 */

EXEC PRO_SELECT_TABLE('MYID', :A_NAME, :A_BONUS);
/* OUT으로 돌려준 값들이 위 변수들에게 담기는데 이때 꼭 ':' 기호를 붙여주어야 한다 */

PRINT A_NAME;
PRINT A_BONUS;

-- 에러 예시
EXEC PRO_SELECT_TABLE('MYID');
/* 매개변수가 3개인 프로시저에 변수값을 1개만 넣어주었기 때문에 에러가 발생한다
   따라서 프로시저의 매개변수 갯수에 맞게 변수들을 모두 넣어주어야 한다 */

```

- 프로시저의 매개변수를 정의할 때 `IN`과 `OUT` 중 어떤 것을 넣는지에 따라 활용방법이 달라지니 주의가 필요하다
- IN : 프로시저 실행시 필요한 값을 받는 변수로 자바에서의 매개변수와 동일한 역할을 한다
- OUT : 프로시저의 실행부에서 나온 결과값을 호출한곳으로 되돌려주는 역할을 한다
- 프로시저 실행과 동시에 모든 바인딩 변수를 출력하기 위해서는 `SET AUTOPRINT ON;`을 실행시켜야 하니 주의

<br>

## FUNCTION

PROCEDURE와 거의 유사하지만 실행결과를 <u>반환</u> 받을 수 있게끔 해준다  
PROCEDURE는 실행결과를 반환하는 것이 아니라 매개변수에다 담아주기만 해주는 것으로 FUNCTION과는 약간 차이가 있다

<br>

> ### FUNCTION 생성

```sql
[표현식]
CREATE [OR REPLACE] FUNCTION 함수명[(매개변수)]
RETURN 자료형
IS
BEGIN
  실행부분
END;
/

[실행방법]
함수명(인수);

-- 생성 예시
CREATE OR REPLACE FUNCTION MYFUNC(A_STR VARCHAR2)
RETURN VARCHAR2
IS
  RESULT VARCHAR2(1000);
BEGIN
  RESULT := '*' || A_STR || '*';
  RETURN RESULT;
END;
/

-- 실행 예시
SELECT MYFUNC('앞뒤로 별이 붙을겁니다') FROM DUAL;
```

- JAVA에서의 일반 함수와 같이 매개변수를 받아 값을 RETURN해주는 식으로 동작한다
- 사용시에도 JAVA에서와 같이 원하는 곳에서 `함수명()` 이라고 불러서 사용하면 된다
