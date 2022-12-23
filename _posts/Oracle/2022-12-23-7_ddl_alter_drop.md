---
title: "[Oracle] SQL문법 7. DDL(ALTER, DROP)"
excerpt: "ALTER, DROP 기본 문법"

categories:
  - Oracle
tags:
  - [Oracle, SQL]

comments: true
toc: true
toc_sticky: true

date: 2020-12-23
last_modified_at: 2020-12-23
---

## DDL (DATA DEFINITION LANGUAGE)

> ### ALTER

```sql
[표현법]
ALTER TABLE 테이블명 수정할 내용;
```

객체 구조를 수정하는 구문으로 크게 3가지 내용을 수정할 수 있다

- 1. 컬럼  
     => 컬럼의 추가/수정/삭제가 가능하다
- 2. 제약조건  
     => 제약조건의 추가/삭제가 가능하다  
     => 제약조건 <u>수정은 불가</u>하므로 수정이 필요하다면 삭제 후 추가를 해주어야 한다
- 3. 명칭  
     => 테이블명, 컬럼명, 제약조건명 수정이 가능하다

<br>

#### [ 컬럼 ]

##### 컬럼 추가(ADD)

```sql
[표현법] (DEFAULT 생략가능)
ALTER TABLE 테이블명 ADD 추가할컬럼명 자료형 [DEFAULT 기본값];

-- 예시
ALTER TABLE TABLE_TEST ADD A_COLUMN VARCHAR2(20);
ALTER TABLE TABLE_TEST ADD B_COLUMN VARCHAR2(20) DEFAULT '한국';
```

- ADD를 사용하여 컬럼 추가가 가능하다
- 컬럼 추가시 DEFAULT 값을 지정해주지 않으면 NULL값이 추가되어 테이블에 반영된다  
   => DEFAULT 값을 지정했다면 해당 값으로 추가된다
- DEFAULT 값 지정은 생략 가능하다

<br>

##### 컬럼 수정(MODIFY)

```sql
[표현법]
-- 컬럼의 자료형 수정
ALTER TABLE 테이블명 MODIFY 수정할컬럼명 변경한자료형;
-- 컬럼의 DEFAULT 값 수정
ALTER TABLE 테이블명 MODIFY 수정할컬럼명 DEFAULT 변경한기본값;

-- 예시1
ALTER TABLE TABLE_TEST MODIFY A_COLUMN VARCHAR2(10);
ALTER TABLE TABLE_TEST MODIFY A_COLUMN DEFAULT 'NAME';
-- 예시2
ALTER TABLE TABLE_TEST
MODIFY  A_COLUMN VARCHAR2(40)
MODIFY B_COLUMN  DEFAULT 'B_아무개'
MODIFY C_COLUMN VARCHAR2(15) DEFAULT 'C_아무개';
```

- MODIFY를 사용하여 컬럼의 자료형과 DEFAULT 값 수정이 가능하다
- 현재 변경하고자 하는 컬럼에 담겨있는 값의 자료형과 완전히 상이한 자료형으로는 변경 불가하다  
   => ex) 실제 '홍길동' 등의 문자열 값이 담겨있는 CNAME컬럼의 자료형을 NUMBER로 바꿀 수는 없다
- 현재 변경하고자 하는 컬럼에 담겨있는 값보다 <u>작게</u>는 변경이 불가능하다  
   => ex) 실제 '홍길동' 등의 값이 담겨있는 CNAME 컬럼의 자료형을 CHAR(1)로 변경할 수는 없다
- 위의 예시2와 같이 한번에 여러개의 컬럼을 변경할 수 있다

<br>

##### 컬럼 삭제(DROP COLUMN)

```sql
[표현법]
ALTER TABLE 테이블명 DROP COLUMN 삭제할컬럼명;

--예시
ALTER TABLE TABLE_TEST DROP COLUMN A_COLUMN;
```

- DROP COLUMN을 사용하여 컬럼을 삭제할 수 있다
- 테이블에 최소 1개의 컬럼은 존재해야한다  
   => 컬럼이 하나밖에 남지 않은 테이블의 컬럼은 삭제할 수 없다
