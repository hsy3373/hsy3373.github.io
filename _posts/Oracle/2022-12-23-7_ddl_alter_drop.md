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
last_modified_at: 2020-12-28
---

## DDL (DATA DEFINITION LANGUAGE)

> ### ALTER

```sql
[표현법]
ALTER TABLE 테이블명 수정할 내용;
```

객체 구조에 대해 ADD(추가), RENAME(이름변경), MODIFY(수정), DROP(삭제) 할 수 있는 구문으로 크게 3가지 내용을 변경할 수 있다

- 테이블의 이름변경
- 컬럼의 이름변경 / 추가 / 수정 / 삭제
- 제약조건의 이름변경 / 추가 / 삭제  
   => 제약조건 <u>수정은 불가</u>하므로 수정이 필요하다면 삭제 후 추가를 해주어야 한다

<br>

#### [ 이름 변경 ]

```sql
[표현법]
-- 테이블
ALTER TABLE 테이블명 RENAME TO 새테이블명;
-- 컬럼
ALTER TABLE 테이블명 RENAME COLUMN 컬럼명 TO 새컬럼명;
-- 제약조건
ALTER TABLE 테이블명 RENAME CONSTRAINTS 제약조건명 TO 새제약조건명;

--예시
ALTER TABLE TABLE_TEST RENAME TO NEW_NAME_TABLE;
ALTER TABLE NEW_NAME_TABLE RENAME COLUMN A_CALUMN TO Z_CALUMN;
ALTER TABLE NEW_NAME_TABLE RENAME CONSTRAINTS TEST_A_CALUMN_PK TO NEW_TEST_A_PK;
```

- 표현법 : `ALTER TABLE 테이블명 RENAME [COULMN/CONSTRAINTS] [컬럼명/제약조건명] TO 바꿀이름`

<br>

#### [ 컬럼 변경 ]

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
- 새로운 컬럼은 테이블 맨 마지막에 추가된다  
   => 만약 컬럼의 위치를 옮기고 싶다면 오라클 12c이상에서 제공하는 컬럼 INVISIBLE(숨김), VISIBLE(보이기) 속성을 사용 하면 된다  
  => 원하는 위치 아래의 컬럼들을 모두 INVISIBLE 처리했다가(옮기려는 컬럼 제외) 다시 VISIBLE 해주는 방식이다

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
- 컬럼 삭제 시 참조하고 있는 컬럼이 있다면 삭제가 불가능하다

<br>

##### 컬럼 비활성화(SET UNUSED)

```sql
[표현법]
ALTER TABLE 테이블명 SET UNUSED(컬럼명);

-- 예시
ALTER TABLE TABLE_TEST SET UNUSED(A_COLUMN);
```

- 컬럼을 삭제하지 않지만 컬럼의 사용을 제한(비활성)한다
- 컬럼을 무조건 삭제해 버리는 것이 위험할 경우 (ex. 접근중인 사용자가 많을 때 등) 우선 비활성을 시켜두고 이후에 DROP 을 진행하는 식으로 사용한다
- SET UNUSED를 진행하면 DROP과 마찬가지로 이후, 데이터를 복구시킬 수 없다

<br>

#### [ 제약조건 변경 ]

##### 제약조건 추가(ADD)

```sql
[표현법] -- [ ]는 생략가능
-- PRIMARY KEY, UNIQUE
ALTER TABLE 테이블명 ADD [CONSTRAINT 제약조건명] 제약조건(컬럼명);

-- FOREIGN KEY
ALTER TABLE 테이블명 ADD [CONSTRAINT 제약조건명] FOREIGN KEY(컬럼명) REFERENCES 참조테이블[(참조컬럼)];

-- CHECK
ALTER TABLE 테이블명 ADD [CONSTRAINT 제약조건명] CHECK(컬럼에 대한 조건);

-- NOT NULL
ALTER TABLE 테이블명 MODIFY 컬럼명 [CONSTRAINT 제약조건명] NOT NULL;

-- 예시
ALTER TABLE TABLE_TEST
ADD CONSTRAINT A_PK PRIMARY KEY(A_COLUMN)
ADD CONSTRAINT B_UQ UNIQUE(B_COLUMN)
ADD FOREIGN KEY(C_COLUMN) REFERENCES Z_TABLE
ADD CHECK(D_COLUMN IN('Y', 'N'))
MODIFY E_COLUMN CONSTRAINT E_NN NOT NULL;
```

- CONSTRAINT
  - 생략 가능하며 따로 제약조건명을 부여하고자 할 때 사용한다
  - 생략시 SYS\_~~ 와 같은 이름의 제약사항으로 자동 생성된다
- PRIMARY KEY : `ADD PRIMARY KEY(컬럼명);`
- FOREIGN KEY : `ADD FOREIGN KEY(컬럼명) REFERENCES 참조할 테이블[(참조할 컬럼)];`
  - 참조할 컬럼 생략 가능하며 생략시 해당테이블의 PK 컬럼을 자동으로 참조한다
- UNIQUE : `ADD UNIQUE(컬럼);`
- CHECK : `ADD CHECK(컬럼에 대한 조건식);`
- NOT NULL : `MODIFY 컬럼명 NOT NULL;`
  - 다른 제약조건들과는 다르게 ADD가 아닌 <u>MODIFY</u>로 추가할 수 있다  
    => NULLABLE(기본값)에서 NOT NULL로 수정하는 것으로 이해하면 된다  
    => 다른 제약조건들과는 다르게 유일하게 수정할 수 있는 제약조건이다
    => NOT NULL을 제외한 다른 제약조건들은 수정이 되지 않기때문에 내용 변경을 원할 시 삭제 후 새로 추가를 해주어야 한다

<br>

##### 제약조건 삭제(DROP)

```sql
[표현법]
-- PRIMARY KEY, FOREIGN KEY, UNIQUE, CHECK
ALTER TABLE 테이블명 DROP CONSTRAINT 제약조건명;

-- NOT NULL
ALTER TABLE 테이블명 DROP MODIFY 컬럼명 NULL;

-- 추가 방법
ALTER TABLE 테이블명 DROP PRIMARY KEY;
```

- 기본적으로 제약조건명을 제시해서 삭제하여야 하므로 정확한 제약조건명을 조회 후 실행해야 한다
- NOT NULL
  - 제약조건 추가와 같이 삭제 또한 MODIFY를 붙여주어야 한다

<br>

> ### DROP

```sql
[표현법]
DROP 객체종류[TABLE, USER, VIEW...] 삭제하고자하는 객체이름;

-- 자식테이블의 외래키 제약조건도 같이 삭제한다
DROP TABLE 테이블명 CASCADE CONSTRAINT;
-- 유저가 생성한 테이블이 있을 경우 그냥 삭제되지 않기 때문에 CACADE 사용
DROP USER 유저명 CASCADE;

-- 예시
DROP TABLE TABLE_TEST;
DROP USER USER_TEST;
```

- 객체 자체를 삭제하는 구문이다  
   => 만약 TABLE을 DROP하게 되면 해당 테이블 자체가 삭제된다
- 단 어딘가에서 참조되고 있는 부모테이블은 일반적인 방법으로는 삭제되지 않는다
  - 방법1) 자식테이블을 먼저 삭제 후 부모테이블을 삭제한다
  - 방법2) 부모테이블만 삭제하되 맞물려있는 있는 외래키 제약조건도 함께 삭제한다
- CASCADE CONSTRAINT
  - 부모테이블을 삭제시키면서 자식테이블의 외래키 제약조건도 같이 삭제시키는 구문
  - 자식테이블에 걸려있던 외래키 제약조건만을 삭제시키며 자식테이블상의 데이터 자체는 그대로 남아있게 된다(NULL 등으로 변경/삭제되지 않는다)

<br>

#### [ DELETE, DROP, TRUNCATE의 차이 ]

| 구분 | 종류           | ROLLBACK 가능여부 | 비고                                                                                                                                                                                        |
| ---- | -------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DML  | DELETE         | 가능              | 데이터가 지워지지만 테이블의 용량이 줄어들지 않는다<br>TRIGGER가 걸려있다면 각 행이 삭제될 때마다 실행된다<br>이전에 할당되었던 영역은 삭제되어 빈 TABLE이나 CLUSTER에 그대로 남아있게 된다 |
| DDL  | TRUNCATE TABLE | 불가능            | 데이터가 지워지며 테이블의 용량이 줄어든다<br>TABLE과 관련된 구조(CONSTRAINT, TRIGGER 등)과 권한에 영향을 주지 않는다<br>TABLE에 걸려있는 TRIGGER는 실행되지 않는다                         |
| DDL  | DROP TABLE     | 불가능            | 데이터뿐만 아니라 테이블 자체가 삭제된다<br>모든 관련된 INDEX, CONSTRAINT, TRIGGER도 삭제된다                                                                                               |

- DDL문은 실행시 ROLLBACK이 되지 않는다
