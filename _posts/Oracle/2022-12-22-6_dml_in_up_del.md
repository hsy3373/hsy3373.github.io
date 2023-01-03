---
title: "[Oracle] SQL문법 6. DML(INSERT, UPDATE, DELETE)"
excerpt: "INSERT, UPDATE, DELETE 기본 문법"

categories:
  - Oracle
tags:
  - [Oracle, SQL]

comments: true
toc: true
toc_sticky: true

date: 2022-12-22
last_modified_at: 2022-12-22
---

## DML (DATA MANIPULATION LANGUAGE)

데이터 조작언어로  
테이블에 새로운 데이터를 삽입(INSERT)하거나 기존의 데이터를 수정(UPDATE)하거나 삭제(DELETE)하는 구문이다

<br>

> ### INSERT

테이블에 새로운 행을 추가하는 구문

| 구문            | 특징                                                                      |
| --------------- | ------------------------------------------------------------------------- |
| INSERT INTO     | 1개의 테이블에 1개의 행을 입력하기                                        |
| INSERT SELECT   | 테이블2에서 검색한 컬럼의 데이터들을 테이블1의 컬럼에 삽입(복사+붙여넣기) |
| INSERT ALL INTO | 여러 테이블에 여러 행 입력, 다른 테이블에 동시에 같은 행 입력하기         |

<br>

#### [ INSERT INTO ]

한개의 테이블에 하나의 행을 입력한다

```sql
[표현법 1]
INSERT INTO 테이블명 VALUES(값1, 값2, ...);
--예시
INSERT INTO EMPLOYEE
VALUES('홍길동', '001213-3155674', 2200000, NULL, SYSDATE, DEFAULT ...);

[표현법 2]
INSERT INTO 테이블명(컬럼명1, 컬럼명2, ...) VALUES(값1, 값2, ...);
--예시
INSERT INTO EMPLOYEE(EMP_NAME, EMP_NO, EMAIL, PHONE, SALARY, GENDER, HIRE_DATE, JOB_CODE)
VALUES('홍길동', '001213-3155674', 'HONG@kh.co.kr', '01099999999', 2200000, NULL, SYSDATE, DEFAULT);

[표현법 3]
INSERT INTO 테이블명(서브쿼리);
--예시
INSERT INTO BOARD_IMAGE(
    SELECT 1 AS BOARD_IMAGE_NO , 'ABC.jpg' AS ORIGIN_NAME, '20221220012345.jpg' AS CHANGE_NAME
    FROM DUAL
);
```

- 표현법1 : `INSERT INTO 테이블명 VALUES(값1, 값2, ...);`

  - 특정테이블의 <u>모든 컬럼</u>에 대해 추가하고자 하는 값을 직접 기술하여 <u>한 행</u>씩 INSERT 할때 쓰는 구문
  - 컬럼의 순서, 자료형, 갯수를 맞춰서 VALUES 괄호 안에 값을 나열해야한다
    - 부족하게 제시했을 경우 : 컬럼의 갯수가 부족하다는 에러 발생
    - 값을 더 많이 제시했을 경우 : TOO MANY VALUES 에러 발생

- 표현법2 : `INSERT INTO 테이블명(컬럼명1, 컬럼명2, ...) VALUES(값1, 값2, ...);`

  - 테이블의 <u>특정 컬럼</u>만 선택해서 해당 컬럼에 추가할 값만 제시하고자 할 때 사용한다
  - 기본적으로 <u>한 행 단위</u>로 추가되기때문에 선택이 안된 컬럼에는 자동으로 NULL / DEFAULT 값이 들어간다
  - NOT NULL, PRIMARY KEY 제약조건이 걸려있는 컬럼은 반드시 직접 값을 넣어주어야한다  
    => 다만 NOT NULL이지만 DEFAULT 설정이 되어있는 경우는 예외

- 표현법3 : ` INSERT INTO 테이블명(서브쿼리);`
  - VALUES로 값을 직접 기술하는 것이 아니라, 서브쿼리로 조회한 결과값을 통째로 INSERT 하는 구문이다  
    => VALUES 대신 서브 쿼리를 이용한 것이다
  - 한번에 여러행을 INSERT 할 수 있다

<br>

#### [ INSERT ALL INTO ]

여러개의 테이블에 동시에 데이터를 입력한다  
단, 이때 사용되는 서브쿼리의 조건절은 동일해야 한다

```sql
[표현법 1]
INSERT ALL
  INTO 테이블1 VALUES(값들 나열)
  INTO 테이블2 VALUES(값들 나열)...
서브쿼리;
--예시
INSERT ALL
  INTO EMP_JOB VALUES (EMP_ID, EMP_NAME, JOB_NAME)
  INTO EMP_DEPT VALUES (EMP_ID, EMP_NAME, DEPT_TITLE)
SELECT EMP_ID, EMP_NAME, JOB_NAME, DEPT_TITLE
FROM EMPLOYEE
JOIN JOB USING(JOB_CODE)
JOIN DEPARTMENT ON (DEPT_CODE = DEPT_ID)
WHERE SALARY >= 3000000;

[표현법 2]
INSERT ALL
  WHEN 조건1 THEN
    INTO 테이블명1 VALUES(컬럼명)
  WHEN 조건2 THEN
    INTO 테이블명2 VALUES(컬럼명)
서브쿼리;
--예시
INSERT ALL
  WHEN HIRE_DATE < '2010/01/01' THEN
    INTO TABLE_1( EMP_ID, EMP_NAME, HIRE_DATE, SALARY)
  WHEN HIRE_DATE >= '2010/01/01' THEN
    INTO TABLE_2( EMP_ID, EMP_NAME, HIRE_DATE, SALARY)
SELECT EMP_ID, EMP_NAME, HIRE_DATE, SALARY -- 위와 갯수를 맞춰주어야 함
FROM EMPLOYEE;
```

- 표현법1 : `INSERT ALL INTO 테이블1 VALUES(값들 나열)... 서브쿼리;`

  - 서브쿼리로 조회한 값들을 각 테이블상에 넣어준다

- 표현법2 : `INSERT ALL WHEN 조건1 THEN INTO 테이블명1 VALUES(컬럼명)... 서브쿼리;`

  - 테이블에 조건에 맞는 값만 넣고 싶을 때 사용하는 구문

<br>

> ### UPDATE

테이블에 기록된 컬럼 값을 수정하는 구문으로 테이블의 전체 행 개수는 변경되지 않는다

```sql
[표현법]
UPDATE 테이블명
SET 컬럼명 = (서브쿼리)
WHERE 조건; -- 생략가능

--예시1
UPDATE EMP_SALARY
SET DEPT_CODE = (SELECT DEPT_CODE
                 FROM EMPLOYEE
                 WHERE EMP_NAME = '선동일')
WHERE EMP_NAME = '홍길동';

--예시2
UPDATE DEPT_COPY
SET DEPT_TITLE = '전략기획팀'
WHERE DEPT_ID = 'D9';
```

- SET에 기술된 컬럼의 값을 서브쿼리를 수행한 결과값 혹은 리터럴하게 설정한 값으로 변경 가능하다  
  => 기존의 값을 해당 값으로 변경하겠다는 뜻
- WHERE를 생략해도 되지만 이럴경우 모든 행의 컬럼 값이 변경된다

<br>

> ### DELETE

테이블에 기록된 데이터를 <u>행</u> 단위로 삭제하는 구문

```sql
[표현법]
DELETE FROM 테이블명
WHERE 조건; --생략가능

--예시
DELETE FROM EMPLOYEE
WHERE EMP_NAME IN('홍길동','김수한');
```

- WHERE를 생략해도 되지만 이럴 경우 테이블의 <u>모든 행이 삭제</u>된다

<br>

#### [ TRUNCATE ]

테이블의 전체행을 모두 삭제할 때 사용하는 구문

```sql
[표현법]
TRUNCATE TABLE 테이블명;

--예시
TRUNCATE TABLE EMP_SALARY;
```

- DELETE 구문보다 수행속도가 매우 빠르다
- 별도의 조건을 제시할 수 없다
- ROLLBACK이 불가하다

- TRUNCATE와 DELETE 비교

  | TRUNCATE                   | DELETE                  |
  | -------------------------- | ----------------------- |
  | `TRUNCATE TABLE 테이블명;` | `DELETE FROM 테이블명;` |
  | 별도의 조건 제시 불가      | 특정조건 제시가능       |
  | 수행속도 빠름              | 수행속도 느림           |
  | ROLLBACK 불가              | ROLLBACK 가능           |
