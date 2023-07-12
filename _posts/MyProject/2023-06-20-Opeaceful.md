---
title: "[Opeaceful] Project Opeaceful"
excerpt: "프로젝트 Opeaceful"

categories:
  - MyProject
tags:
  - [Project, Spring]

comments: true
toc: true
toc_sticky: true

date: 2023-06-20
last_modified_at: 2023-07-13
---

## Project [ Opeaceful ]

> ### 프로젝트 소개

##### 사내 그룹웨어 프로그램

실시간 협업, 보안과 접근제어, 업무 문서 및 파일공유
사원 친화적인 그룹웨어를 기획

반응형 웹페이지와 AWS를 통한 배포까지를 목표로 함.

![프로젝트 소개](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/opeaceful.gif)

<ul>
  <li>팀원 : 한승은(조장), 김혜린, 노지의, 박가영, 윤지영, 김진기</li>
  <li><a href="https://github.com/Opeaceful/Opeaceful" target="_blank">깃허브 (바로가기)</a></li>
  <li><a href="/assets/images/MyProject/Opeaceful.pdf" download>한승은 PPT (다운로드)</a></li>
</ul>

<br>

> ### 주요기능 소개 영상

<p><small>※각 메뉴 클릭시 상세 내용 확인가능</small></p>

<details>
<summary> 로그인 / 메인 </summary><br>
<div markdown="1">

![로그인 / 메인](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/login.gif)

</div>
</details>

<details>
<summary> 내정보 </summary><br>
<div markdown="1">

![내정보](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/mypage.gif)

</div>
</details>

<details>
<summary> 연차관리 </summary><br>
<div markdown="1">

![연차관리](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/annual.gif)

</div>
</details>

<details>
<summary> 조직도 </summary>
<div markdown="1">

![조직도](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/darkmode.gif)

</div>
</details>

<details>
<summary> 게시판 </summary>
<div markdown="1">

![게시판](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/board.gif)

</div>
</details>

<details>
<summary> 캘린더 </summary>
<div markdown="1">

![캘린더](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/calendar.gif)

</div>
</details>

<details>
<summary> 근태관리 </summary>
<div markdown="1">

![근태관리](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/darkmode.gif)

</div>
</details>

<details>
<summary> 계정관리 </summary>
<div markdown="1">

![계정관리](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/member.gif)

</div>
</details>

<details>
<summary> 권한관리 </summary>
<div markdown="1">

![권한관리](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/role.gif)

</div>
</details>

<details>
<summary> 급여관리 </summary>
<div markdown="1">

![급여관리](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/salary.gif)

</div>
</details>

<details>
<summary> 전자결제 </summary>
<div markdown="1">
  
  - 전자결재 양식
  ![전자결제양식](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/approvalForm.gif)
  - MY 전자결재
    ![전자결제](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/approval.gif)
  - 전자결재 관리
    ![전자결제관리](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/approvalManage.gif)

</div>
</details>

<details>
<summary> 채팅 </summary>
<div markdown="1">

![채팅](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/darkmode.gif)

</div>
</details>

<details>
<summary> 다크모드 </summary>
<div markdown="1">

![다크모드](https://github.com/Opeaceful/Opeaceful/raw/main/Opeaceful/src/main/webapp/resources/etc/video/darkmode.gif)

</div>
</details>

<br>

> ### 담당기능

- 한승은

  - 기획서 작성

    - <a href="https://docs.google.com/spreadsheets/d/1BetFMp64okyNTD5TSe3A4GyWWF_pxn_f3TOzRJlA34o/edit?usp=sharing" target="_blank">기획서(바로가기)</a>

  - DB 설계
    <p align="center">
      <img width="calc(100% - #{$right-sidebar-width-narrow})" height="auto" src="/assets/images/MyProject/Opeaceful.png">
    </p>

- SQL
  - [Opeaceful_TABLE.sql] : MYSQL 테이블 기본 세팅용 sql파일
- 전자결재 공통 양식 메뉴
  - [ApprovalFormController.java] : 전자결재 양식용 컨트롤러
  - [approvalForm.jsp] : 전자결재 양식 페이지
  - [approvalFormData.js] : 전자결재 양식 페이지용 Ajax를 모아둔 js 파일
  - [approvalFormFront.js] : 전자결재 양식 페이지용 페이지의 기본동작 이벤트를 부여한 js 파일
- 전자결재 관리 메뉴
  - [ApprovalController.java] : MY전자결재, 전자결재 관리 메뉴 공통 컨트롤러
  - [allApproval.jsp] : 전자결재 관리 페이지
  - [allApprovalData.js] : 전자결재 관리 페이지용 Ajax를 모아둔 js파일
  - [allApprovalFront.js] : 전자결재 관리 페이지용 기본동작 이벤트를 부여한 js 파일
- MY전자결재 메뉴
  - [ApprovalController.java] : MY전자결재, 전자결재 관리 메뉴 공통 컨트롤러
  - [myApproval.jsp] : MY전자결재 페이지
  - [myApprovalData.js] : MY전자결재 페이지용 Ajax를 모아둔 js파일
  - [myApprovalFront.js] : MY전자결재 페이지용 기본동작 이벤트를 부여한 js 파일
- 전자결재 공통 파일들
  - Mapper
    - [approval-mapper.xml] : 전자결재 관련 공통 매퍼
  - 메모
    - [memoModal.jsp] : 전자결재 메모 모달 화면
    - [memo.js] : 전자결재 메모 기본동작용 js 파일
  - 전자결재 작성/수정 모달
    - [approvalModal.jsp] : 전자결재 작성/수정용 모달 화면
    - [approvalModal.js] : 전자결재 작성/수정용 모달 기본 동작용 js 파일
  - 전자결재 조회 모달
    - [endApprovalModal.jsp] : 전자결재 문서 조회용 모달 화면
  - 텍스트에디터
    - [tinyEditor.js] : Tinymce 에디터 사용및 세팅을 위한 js 파일
  - 전자결재 알림
    - [AprWebsocketHandler.java] : 전자결재 알림을 위한 웹소켓 핸들러
    - [aprWebsocket.js] : 전자결재 알림용 웹소켓 js 파일

<br>

> ### 사용 기술 스택

- FE (Front-End)

  - <img src="https://img.shields.io/badge/JSP-F46D01?style=flat&logo=JSP&logoColor=white"/>
  - <img src="https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=HTML5&logoColor=white"/>
  - <img src="https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=CSS3&logoColor=white"/>
  - <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=JavaScript&logoColor=white"/>
  - <img src="https://img.shields.io/badge/jQuery-0769AD?style=flat&logo=jQuery&logoColor=white"/>

- BE (Back-End)

  - Language: <img src="https://img.shields.io/badge/JAVA-007396?style=flat&logo=JAVA&logoColor=white"/> <img src="https://img.shields.io/badge/Ajax-2AA5DC?style=flat&logo=Ajax&logoColor=white"/>
  - WAS(Web-Application-Server): <img src="https://img.shields.io/badge/Apache Tomcat-F8DC75?style=flat&logo=ApacheTomcat&logoColor=white"/> 9.0
  - Database
    - <img src="https://img.shields.io/badge/MySQL-232F3E?style=flat&logo=MySQL&logoColor=white"/>
    - MySQL Workbench 8.0 CE
    - <img src="https://img.shields.io/badge/Amazon RDS-527FFF?style=flat&logo=AmazonRDS&logoColor=white"/>
  - Developer tool
    - Java: <img src="https://img.shields.io/badge/STS-6DB33F?style=flat&logo=STS&logoColor=white"/>
    - Server: <img src="https://img.shields.io/badge/Amazon AWS-232F3E?style=flat&logo=AmazonAWS&logoColor=white"/>
  - Framework

    - <img src="https://img.shields.io/badge/Spring-6DB33F?style=flat&logo=Spring&logoColor=white"/>

    - <img src="https://img.shields.io/badge/Bootstrap-7952B3?style=flat&logo=Bootstrap&logoColor=white"/>

- 사용 디자인 패턴: **MVC 패턴**