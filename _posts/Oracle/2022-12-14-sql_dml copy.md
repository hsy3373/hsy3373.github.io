---
title: "[Oracle][SQL] Oracle SQL문법 1.SQL과 DML(Data Manipulation Language) - 기본문법  "
excerpt: "SELECT 등 DML 기본 문법"

categories:
  - Oracle
tags:
  - [Oracle, SQL, DML]

comments: true
toc: true
toc_sticky: true

date: 2020-12-14
last_modified_at: 2020-12-15
---

## SQL(Structured Query Language)

> ### SQL 이란

- 관계형 데이터베이스에서 데이터를 조회하거나 조작하기 위해 사용하는 표준 검색 언어이다
- 원하는 데이터를 찾는 방법이나 절차를 기술하는 게 아닌 <u>조건</u>을 기술하여 작성한다

- 주요 용어
  <p align="center">
    <img width="calc(100% - #{$right-sidebar-width-narrow})" height="auto" src="/assets/images/db/table.png">
  </p>
  1. 행(Row), 튜플
  2. 컬럼, 도메인
  3. 기본키(Primary Key)
  4. 외래키(Foreign Key)
  5. Null
  6. 컬럼값, 속성값

- 분류

  | 분류                               | 용도          | 명령어                                          |
  | ---------------------------------- | ------------- | ----------------------------------------------- |
  | DQL (Data Query Language)          | 데이터 검색   | SELECT                                          |
  | DML (Data Manipulation Language)   | 데이터 조작   | INSERT(추가), UPDATE(수정), DELETE(삭제)        |
  | DDL (Data Definition Language)     | 데이터 정의   | CREATE(생성), DROP(삭제), ALTER(수정/삭제/추가) |
  | DCL (Data Control Language)        | 데이터 제어   | GRANT(권한부여), REVOKE(권한해제)               |
  | TCL (Transaction Control Language) | 트랜잭션 제어 | COMMIT(정상저장), ROLLBACK(취소)                |

  - SLELCT를 위처럼 DQL로 따로 빼기도 하지만 대부분 DML로 포함시킨다

<br>

> ### 주요 데이터 타입

<table>
<thead>
  <tr>
    <th>데이터 타입</th>
    <th>하위 데이터 타입</th>
    <th>설명</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>NUMBER</td>
    <td></td>
    <td>숫자</td>
  </tr>
  <tr>
    <td rowspan="3">CHARACTER</td>
    <td>CHAR</td>
    <td>고정길이 문자(최대 2000바이트)</td>
  </tr>
  <tr>
    <td>VARCHAR2</td>
    <td>가변길이 문자(최대 4000바이트)</td>
  </tr>
  <tr>
    <td>LONG</td>
    <td>가변길이 문자(최대 2기가 바이트)</td>
  </tr>
  <tr>
    <td>DATE</td>
    <td></td>
    <td>날짜</td>
  </tr>
  <tr>
    <td rowspan="2">LOB</td>
    <td>CLOB</td>
    <td>가변길이 문자(최대 4기가 바이트)</td>
  </tr>
  <tr>
    <td>BLOB</td>
    <td>Binary Data</td>
  </tr>
</tbody>
</table>

<br>

#### [ NUMBER ]

- `NUMBER[ ( P [ , S ] ) ]`

  - [ ] : 생략가능
  - P : 표현할 수 있는 전체 숫자 자리 수 (1 ~ 38)
  - S : 소수점 이하 자리 수 (-84 ~ 127)
  - 정수/실수 관계 없이 사용하는 자료형이다

<br>

#### [ CHARACTER ]

- 공통사항

  - [ ] : 생략가능
  - SIZE : 포함될 문자(열)의 크기  
    => 숫자/영문자/특수문자 : 1글자당 1byte  
    => 한글/한자 : 1글자당 3byte
  - 데이터는 ''를 사용하여 표기하고 대·소문자를 구분

- `CHAR( SIZE [ ( byte | char ) ]`

  - 지정한 크기보다 작은 문자(열)가 입력되면 남는 공간은 공백으로 채움  
    => 고정된 길이를 가진다
  - 최대 2000byte 까지 저장가능
  - 주로 들어올 값의 글자수가 정해져 있을 경우 사용한다  
    => ex) 성별 , 주민번호 등
  - 나중에 java 등과 연동했을 때 안에 공백이 포함되어있다면 뜻하지 않은 오류가 발생할 가능성이 높아서 아래 VARCHAR 활용을 추천한다

<br>

- `VARCHAR2( SIZE [ ( byte | char ) ]`

  - 크기가 0인 값은 NULL로 인식
  - 공간대비 저장되는 글자가 크다면 오류발생
  - 최대길이 4000byte 까지 가능하다
  - VAR는 가변, 2는 2개를 의미한다
  - 주로 들어온 값의 글자수가 정해져 있지 않은경우 사용한다
  - 매개변수에 CHAR가 들어온 경우 byte단위로 데이터를 체크하지 않고 문자의 갯수로 체크한다

- `NVARCHAR`

  - 문자열의 바이트가 아닌, 문자 갯수 자체를 길이로 취급한다
  - 유니코드를 지원하기 위한 자료형이다

  <p align="center">
    <img width="calc(100% - #{$right-sidebar-width-narrow})" height="auto" src="/assets/images/db/NVARCHAR2.png">
  </p>

<br>

#### [ DATE ]

- `DATE`
  - 일자(세기/년/월/일) 및 시간(시/분/초) 정보를 관리한다
  - 기본적으로 화면에 년/월/일 정보만 표기한다
  - 날짜 연산 및 비교 가능하다

| 연산           | 결과 타입 | 설명                      |
| -------------- | --------- | ------------------------- |
| 날짜 + 숫자    | DATE      | 날짜에서 숫자만큼 며칠 후 |
| 날짜 - 숫자    | DATE      | 날짜에서 숫자만큼 며칠 전 |
| 날짜 - 날짜    | NUMBER    | 두 날짜의 일수 차         |
| 날짜 + 숫자/24 | DATE      | 날짜 + 시간               |
