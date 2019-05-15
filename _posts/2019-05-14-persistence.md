---
layout: post
section-type: post
title: "영속성(Persistence)"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)


# 영속성(Persistence)
데이터를 생성한 프로그램이 종료되더라도 사라지지 않는 데이터의 특성을 말한다.
영속성을 갖지 않는 데이터는 단지 메모리에서만 존재하기 때문에 프로그램을 종료하면 모두 잃어버리게 된다.

## Object Persistence(영구적인 객체)
메모리 상의 데이터를 파일 시스템, 관계형 테이터베이스 혹은 객체 데이터베이스 등을 활용하여 영구적으로 저장하여 영속성 부여한다.

## 데이터를 데이터베이스에 저장하는 3가지 방법
1) JDBC (java에서 사용)
2) Spring JDBC (Ex. JdbcTemplate)
3) Persistence Framework (Ex. Hibernate, Mybatis 등)

# Persistence Layer
프로그램의 아키텍처에서, 데이터에 영속성을 부여해주는 계층을 말한다.
JDBC를 이용하여 직접 구현할 수 있지만 Persistence framework를 이용한 개발이 많이 이루어진다.

# Persistence Framework
JDBC 프로그래밍의 복잡함이나 번거로움 없이 간단한 작업만으로 데이터베이스와 연동되는 시스템을 빠르게 개발할 수 있으며 안정적인 구동을 보장한다.
Persistence Framework는 SQL Mapper와 ORM으로 나눌 수 있다.
Ex) JPA, Hibernate, Mybatis 등


---
참고 :
https://gmlwjd9405.github.io/2019/02/01/orm.html
