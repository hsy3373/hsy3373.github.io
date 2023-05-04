---
title: "[JAVA Framework] JAVA Framework와 Spring"
excerpt: "Framework의 종류와 Spring 이해"

categories:
  - Spring
tags:
  - [Spring, Java-Framework]

comments: true
toc: true
toc_sticky: true

date: 2023-04-26
last_modified_at: 2023-05-04
---

## Framework

> ### Framework 란

개발자가 소프트웨어를 개발함에 있어 코드를 구현하는 개발 시간을 줄이고 코드의 재사용성을 증가시키기 위한 일련의 클래스 묶음이나, 뼈대, 틀을 제공하는 라이브러리를 구현해놓은 것

- 특징

  - 개발자가 따라야하는 가이드 제공
  - 개발할 수 있는 범위가 정해져 있다
  - 개발자를 위한 다양한 도구 및 플러그인 지원

- 장점

  - 개발시간 단축 가능
  - 정형화되어있어 일정 수준 이상의 품질을 기대할 수 있다
  - 유지보수가 쉽다

- 단점

  - 지나친 의존 시 개발자의 능력이 떨어져 스스로 개발하는 것이 어려워질 수 있다
  - 습득 시간이 오래 걸린다

  <br>

> ### Framework 종류

| 구분      | 종류                                          | 설명                                                                                 |
| --------- | --------------------------------------------- | ------------------------------------------------------------------------------------ |
| 영속성    | MyBatis, Hibernate                            | 데이터의 저장, 조회, 변경, 삭제를 다루는 클래스 및 설정 파일을 라이브러리화하여 구현 |
| 자바      | Spring Framework, 전자정부표준 Spring, Struts | Java EE를 통한 웹 애플리케이션 개발에 초점을 맞춰 필요한 요소들을 모듈화해 제공      |
| 화면구현  | Bootstrap, Foundation, MDL                    | Front-End를 보다 쉽게 구현할 수 있게 틀 제공                                         |
| 기능 지원 | Log4j, JUnit 5, ANT                           | 특정 기능이나 업무 수행에 도움을 줄 수 있는 기능 제공                                |

  <br>

## Spring Framework

> ### Spring Framework 란

자바 플랫폼을 위한 오픈소스 애플리케이션 프레임워크
-> 간단하게 스프링(Spring)이라고도 부름
동적인 웹 사이트를 개발하기 위한 여러가지 서비스 제공

Spring 공식 사이트 : [https://spring.io](https://spring.io)

- 특징

  | 종류                                                             | 설명                                                                                                                                                                                                                                            |
  | ---------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | DI (Dependency Injection)<br>의존성 주입                         | 설정 파일이나 어노테이션을 통해 객체 간의 의존 관계를 설정하여<br>개발자가 직접 의존하는 객체를 생성할 필요 없음                                                                                                                                |
  | Spring AOP (Aspect Oriented Programming)<br>관점 지향 프로그래밍 | 트랜잭션, 로깅, 보안 등 여러 모듈, 여러 계층에서 공통으로 필요로 하는 기능의 경우 해당 기능들을 분리하여 관리                                                                                                                                   |
  | POJO(Plain Old Java Object)                                      | 일반적인 J2EE 프레임워크에 비해 특정 라이브러리를 사용할 필요가 없어 개발이 쉬우며 기존 라이브러리의 지원 용이                                                                                                                                  |
  | IoC (Inversion of Control)<br>제어 반전                          | 컨트롤의 제어권이 개발자가 아니라 프레임워크에 있다는 뜻으로<br>객체의 생성부터 모든 생명주기의 관리까지 프레임워크가 주도<br>객체를 생성하고 직접 호출하는 프로그램이 아니라 만들어둔 자원을 호출하여 사용                                     |
  | Spring JDBC                                                      | MyBatis나 Hibernate 등의 데이터베이스를 처리하는 영속성 프레임워크와 연결할 수 있는 인터페이스 제공                                                                                                                                             |
  | Spring MVC                                                       | MVC 디자인 패턴을 통해 웹 애플리케이션의 Model, View, Controller 사이의 의존 관계를 DI 컨테이너에서 개발자가 아닌 서버가 객체들을 관리하는 웹 애플리케이션 구축                                                                                 |
  | PSA (Portable Service Abstraction)                               | 스프링을 다른 여러 모듈을 사용함에 있어 별도의 추상화 레이어 제공 예를 들어 JPA를 사용할 때 Spring JPA를 사용하여 추상화하므로 실제 구현에 있어 Hibernate를 사용하든 EclipseLink를 사용하든 개발자는 모듈의 의존 없이 프로그램에 집중할 수 있음 |

<br>

> ### Spring 구성 모듈

<p align="center">
  <img width="calc(100% - #{$right-sidebar-width-narrow})" height="auto" src="/assets/images/spring/springFramework.png">
</p>

- Data 접근 계층

  - JDBC나 데이터베이스에 연결하는 모듈
  - Data 트랜잭션에 해당하는 기능을 담당하여 영속성 프레임워크의 연결담당

- MVC 계층(MVC/Remoting)

  - Spring Framework에서 Servlet, Struts 등 웹 구현 기술과의 연결점을 Spring MVC 구성으로 지원하기 위해 제공되는 모듈 계층
  - 스프링의 리모팅 기술로 RMI, Hessian, Burlap, JAX-WS, Http 호출자 그리고 REST API 모듈 제공

- AOP 계층

  - Spring에서 각 흐름간 공통된 코드를 한 쪽으로 빼내어 필요한 시점에 해당 코드를 첨부하게 하기 위해 지원하는 계층
  - 별도의 proxy를 두어 동작, 이를 통해 객체간의 결합도를 낮출 수 있음

- Core Container

  - Spring 핵심 부분이라고 할 수 있으며 모든 스프링 관련 모듈은 이 Core Container 기반으로 구축
  - Spring의 근간이 되는 IoC(또는 DI) 기능을 지원하는 영역 담당
  - BeanFactory를 기반으로 Bean클래스들을 제어할 수 있는 기능 지원

- 기타 모듈

  | 모듈 명                | 내용                                                                                              |
  | ---------------------- | ------------------------------------------------------------------------------------------------- |
  | spring-beans           | 스프링 컨테이너를 이용해서 객체를 생성하는 기본기능 제공                                          |
  | spring-context         | 객체 생성, 라이프 사이클 처리, 스키마 확장 등의 기능 제공                                         |
  | spring-aop             | AOP 기능 제공                                                                                     |
  | spring-web             | REST클라이언트 데이터 변환 처리, 서블릿 필터, 파일 업로드 지원 등 웹 개발에 필요한 기반 기능 제공 |
  | spring-webmvc          | 스프링 기반의 MVC 프레임워크, 웹 애플리케이션을 개발하는데 필요한 컨트롤러, 뷰 구현 제공          |
  | spring-websocket       | 스프링 MVC에서 웹 소켓 연동을 처리할 수 있도록 제공                                               |
  | spring-oxm             | XML과 자바 객체 간의 매핑을 처리하기 위한 API 제공                                                |
  | spring-tx              | 트랜잭션 처리를 위한 추상 레이어 제공                                                             |
  | spring-jdbc            | JDBC프로그래밍을 보다 쉽게 할 수 있는 템플릿 제공                                                 |
  | spring-orm             | Hibernate, JPA, MyBatis 등과의 연동 지원                                                          |
  | spring-jms             | JMS서버와 메시지를 쉽게 주고 받을 수 있도록 하기 위한 템플릿                                      |
  | spring-context-support | 스케줄링, 메일발송, 캐시연동, 벨로시티 등 부가기능제공                                            |
