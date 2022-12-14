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

date: 2022-12-28
last_modified_at: 2023-01-02
---

## DCL (DATA CONTROL LANGUAGE)

데이터를 제어하는 언어로 DB에 대한 보안, 무결성, 복구 등 DBMS를 제어하는 용도로 쓰인다  
※ 원래 데이터 정의어로 분류되었지만, 데이터베이스 제어기능이 중요해지고 다양한 제어 기능이 소개되면서 독립되었다

<br>

> ### 권한

Oracle 에서 권한은 특정 타입의 SQL문을 실행하거나 데이터베이스 or 객체에 접근할 수 있는 권리를 말한다

- 시스템 권한

  - 객체 생성, 변경, 소멸 등 DB의 생성과 관리 전반에 관한 권한으로 SYS(SYSTEM/관리자계정)에게 부여한다
  - 시스템 권한은 매우 강력한 기능을 가지므로 대부분 관리자나 개발자에게만 부여하도록 한다
  - 백여개 이상의 시스템 권한이 존재한다
  - 권한의 ANY 키워드 : 사용자가 모든 스키마에서 권한을 가짐을 의미  
    => ANY키워드를 일반 사용자에게 부여한다면 다른 사용자의 스키마에 테이블을 만드는 등의 위험이 있기때문에 보통 일반 사용자에겐 부여하지 않는다
  - 대표적인 시스템 권한
    - `CREATE SESSION` : 데이터베이스를 연결할 수 있는 권한으로 이 권한이 있어야 해당 계정으로 로그인 할 수 있다
    - `CREATE ROLE` : 오라클 데이터베이스 역할을 생성할 수 있는 권한
    - `CREATE VIEW` : 뷰 생성
    - `ALTER USER` : 생성한 사용자의 정의를 변경할 수 있는 권한
    - `DROP USER` : 생성한 사용자를 삭제시키는 권한

- 개체 권한

  - 사용자가 특정 개체에 대해 특정 작업을 수행 가능하도록 일반 사용자에게 부여하는 권한이다
  - 객체 내용 조작과 관련된 권한으로, 객체 소유자에게 부여받는 권한이다  
    => ex) 특정 테이블의 행 삭제 등

- 역할(ROLE)

  - 사용자에게 허가할 수 있는 권한들의 집합이다  
    => 시스템 권한만 해도 120가지 이상이 되며 그 많은 권한을 사용자들에게 일일이 부여하기 어렵기 때문에 집합으로 만듦
  - 사용자에게 특정 집합(ROLE)을 권한대신 부여하는 식으로 사용한다
  - 롤은 CREATE ROLE 권한을 가진 USER에 의해서 생성될 수 있다
  - 한 사용자가 여러개의 ROLE을 ACCESS 할 수 있고, 여러 사용자에게 같은 ROLE을 부여할 수 있다
  - Oracle 설치와 동시에 기본적으로 생성되어있는 ROLE
    - `CONNECT` : 오라클에 접속할 수 있는 세션 생성 및 테이블 생성/조회를 할 수 있는 가장 일반적인 권한들이며 CREATE SECTTION 권한도 들어가 있다
    - `RESOURCE` : 객체의 생성, 변경, 삭제(CREATE, INSERT, UPDATE, DELETE) 등의 기본 시스템 권한으로 PL/SQL 사용시에도 해당 ROLE을 부여해주어야 한다
    - `DBA` : 모든 시스템 권한이 부여된 ROLE으로 데이터베이스 관리자에게만 부여해야 한다
    - `SYSDBA` : DB 시작과 종료 및 관리 권한
    - `SYSOPER` : SYSDBA + DB 생성 권한

<br>

> ### 계정 생성

```sql
CREATE USER 사용자명 IDENTIFIED BY 비밀번호;
```

- 계정 종류
  - 관리자 계정 : DB의 생성과 관리를 담당하는 계정으로 모든 권한과 책임을 가지는 계정
  - 사용자 계정 : DB에 대해서 질의, 갱신, 보고서 작성 등의 작업을 수행할 수 있는 계정, 업무에 필요한 최소한만의 권한만 가지는 것을 원칙으로 한다
- 일반 사용자 계정은 위 구문을 사용하여 관리자 계정에서만 만들 수 있다
- 사용자 계정 생성 후 해당 계정에게 권한을 부여(GRANT)하고 권한을 삭제(REVOKE)하기도하며 계정들을 관리하게 된다

<br>

> ### GRANT

```sql
[표현법]
GRANT 권한|ROLE명칭 TO 사용자계정;

-- 예시
GRANT CONNECT, RESOURCE TO USER1;
```

- 사용자에게 권한(ROLE)을 부여하는 명령어이다
- `,`를 사용하여 한번에 여러개의 권한, ROLE을 나열하여 기입할 수 있다
- CONNECT(계정접속), RESOURCE(객체생성/변경/삭제)는 보통 일반 계정이 작업을 하기 위한 최소한의 권한이라고 할 수 있다

<br>

> ### REVOKE

```sql
[표현법]
REVOKE 권한|ROLE명칭 FROM 사용자계정;

-- 예시
REVOKE CONNECT, RESOURCE FROM USER1;
```

- 사용자의 권한(ROLE)을 회수(삭제)하는 명령어이다
- `,`를 사용하여 한번에 여러개의 권한, ROLE을 나열하여 기입할 수 있다
