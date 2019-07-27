---
layout: post
section-type: post
title: "[Hibernate에 대해서 제대로 알자!] 2탄 Hibernate의 구조를 알자!"
category: Spring
tags: [ 'Spring', 'Java', 'JPA', '글또2기', '시리즈물' ]
comments: true
---

제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---
이 글은 시리즈 물입니다.
[1탄 ORM이란? JPA란? Hibernate란?] https://joosjuliet.github.io/orm_jpa_hibernate/  
[2탄 Hibernate의 구조를 알자!] https://joosjuliet.github.io/hibernate_structure/  
[3탄 Hibernate가 어떻게 obejct를 만드는가?] https://joosjuliet.github.io/hibernate_first_step/  


# 1. Hibernate는?
- ORM의 tool
- 프로그래밍 언어 내에서 사용될 수있는 "virtual object database"가 생성

- Hibernate는 persistence framework
  - Java 환경에서 database로 data를 persist하는데 사용된다.
- <span style="background-color:yellow"><b>Persistence은 영구적인 매체에 데이터를 저장하고, 데이터를 생성 한 애플리케이션이 종료 된 후에도 언제든지 데이터를 검색하는 프로세스</b></span>
  - db가 connection이 연결이 되어 있지 않아도 db를 가지고 일처리를 할 수 있다.]

# 2. Hibernate Architecture

## Hibernate의 최소 구조
<img alt="diagram_of_hibernate_architecture" src = "/images/2019-03-20-hibernate_structure/diagram_of_hibernate_architecture.png"/>


크게 4가지 layers로 되어있다.
- Java application layer
- Hibernate framework layer
- Backhand api layer
- Database layer


### 하이버네이트 framework layer
- 데이터베이스와 응용 프로그램 사이에 레이어를 만든다.
- 데이터베이스 연결 문자열, 엔터티 클래스, 매핑 등의 구성 정보를 로드
- 애플리케이션과 데이터베이스 간의 데이터를 동기화하는 영속 객체를 생성



## Hibernate 중점 구조
<img alt="high_level_architecture_of_hibernate" src = "/images/2019-03-20-hibernate_structure/high_level_architecture_of_hibernate.png"/>


### Hibernate 구조의 elements들

- <b> Hibernate는 데이터를 데이터베이스에 유지하기 위해 엔티티 클래스 (데이터베이스 테이블과 매핑 된 Java 클래스)의 인스턴스를 생성 </b>
- 이 객체는 세션과 아직 연관되지 않았거나 아직 데이터베이스에 유지되지 않았으므로 <b>Transient 객체</b>라고합니다.
- 객체를 데이터베이스에 유지하려면 SessionFactory 인터페이스의 인스턴스가 만들어집니다.

- SessionFactory는 Factory 디자인 패턴을 구현하는 싱글 톤 인스턴스입니다.
- SessionFactory는 hibernate.cfg.xml 파일 (Hibernate 구성 파일, 다음 섹션에서 더 자세하게 설명 됨)을 로드한다.
- TransactionFactory와 ConnectionProvider의 도움을 받아 데이터베이스의 모든 구성 설정을 구현한다.
- Hibernate의 각 데이터베이스 연결은 Session 인터페이스의 인스턴스를 생성함으로써 생성된다.
- 세션은 데이터베이스와의 단일 연결을 나타낸다.
- 세션 객체는 SessionFactory 객체로부터 생성된다.
- 또한 Hibernate는 기본 JDBC 또는 JTA 트랜잭션으로부터 응용 프로그램을 추상화하는 내장 트랜잭션 API를 제공합니다.
- 각 트랜잭션은 단일 원자 단위의 작업 단위를 나타냅니다. 하나의 세션은 여러 트랜잭션을 채울 수 있다.


### elements 하나씩 보기
많은 object로 구성되어 있다.
대표적으로는
- SessionFactory
  - SessionFactory는 ConnectionProvider의 세션 및 클라이언트 팩토리
  - 데이터의 2 차 레벨 캐시 (선택 사항)를 보유
  - org.hibernate.SessionFactory 인터페이스는 Session 객체를 얻기위한 팩토리 메소드를 제공
- Session
  - 세션 객체는 응용 프로그램과 데이터베이스에 저장된 데이터 간의 인터페이스를 제공
  - 수명이 짧은 객체이며 JDBC 연결을 래핑합니다. 트랜잭션, 쿼리 및 기준의 팩토리
  - 데이터의 1 차 수준 캐시 (필수)를 보유합니다.
  - org.hibernate.Session 인터페이스는 객체를 삽입, 갱신, 삭제하는 메소드를 제공
  - 또한 Transaction, Query 및 Criteria에 대한 팩토리 메소드를 제공합니다.
- Transaction
  - 트랜잭션 오브젝트는 원자 단위의 작업 단위를 지정합니다.
- ConnectionProvider
  - JDBC connection을 만드는 공장이다.
  - DriverManager or DataSource의 application을 추상화한다.
- TransactionFactory
- JAVA API
  - JDBC (Java Database Connectivity)
  - JTA (Java Transaction API)
  - JNDI (Java Naming Directory Interface)

session에서 하는 일을 repository가 알아서 해주는 것이다.
- 한건 조회시 기본으로 되는데 findall 을 하면 lazy가 일어나서 n+1문제가 일어나서
해결책 -> 최신 스팩을 사용하면 entitygraph라는 anotate사용하면 join으로 가져올 수 잇게 된다.
그 전이면 query jpql을 사용해서 fetch라는 쿼리를 날리거나

---
사진 출처 : https://viralpatel.net/blogs/introduction-to-hibernate-framework-architecture/  
참고:   
https://viralpatel.net/blogs/introduction-to-hibernate-framework-architecture/  
