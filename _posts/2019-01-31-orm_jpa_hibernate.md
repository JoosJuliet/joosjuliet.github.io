---
layout: post
section-type: post
title: "[Hibernate에 대해서 제대로 알자!] 1탄 ORM이란? JPA란? Hibernate란?"
category: Spring
tags: [ 'Spring', 'Java', 'SKEncar', 'JPA', '글또2기', '시리즈물' ]
comments: true
---
이 글은 시리즈 물입니다.
[1탄 ORM이란? JPA란? Hibernate란?] https://joosjuliet.github.io/orm_jpa_hibernate/  
[2탄 Hibernate의 구조를 알자!] https://joosjuliet.github.io/hibernate_structure/  
[3탄 Hibernate가 어떻게 obejct를 만드는가?] https://joosjuliet.github.io/hibernate_first_step/  


*db위주 프로그래밍에서 벗어나기*
DB중심 위주의 프로그래밍이 아닌 현실 위쥐의 객체지향적 프로그래밍으로 전환해야겠다.
- DB설계 → 프로그램설계 가 아니라
- 프로그램 설계 → DB설계로 바꿔야겠다.

# ORM이란?
- <span style="background-color:yellow"><b>객체가 테이블이 되도록 매핑 시켜주는 프레임워크</b></span>
- 관계와 RDB 간의 차이를 중간에서 해결해 주는 것

# 패러디임의 불일치
RDB는 데이터 중심으로 구조화 되어있고, 집합적인 사고를 요구한다.
그리고 객체 지향에서 이야기하는 추상화, 상속, 다형성 같은 개념이 없다.

## 상속

## 연관관계
- 객체는 참조를 사용해서 다른 객체와 연관관계를 가지고 참조에 접근해서 연관된 객체를 조회
- 테이블은 외래키를 사용해서 다른 테이블과 연관관계를 가지고 조인을 사용해서 연관된 테이블을 조회

## 객체 그래프 탐색
<span style="background-color:yellow"><b>이 패러다임의 불일치를 해결하기 위한 결과물이 JPA</b></span>


# JPA란?(Java Persistence API)
- <span style="background-color:yellow"><b>자바 진영의 ORM 기술 표준</b></span>
- ORM을 사용하기 위한 인터페이스를 모아둔 것
- 개발자는 SQL을 직접 작성하는 것이 아니라 어떤 SQL이 실행될지 생각만 하면 된다.

# Hibernate Framework란?
<span style="background-color:yellow"><b>JPA를 사용하기 위해서 JPA를 구현한 ORM 프레임워크</b></span>

<img alt="success" src = "/images/2019-01-31-hibernate/Hibernate.png"/>



---
참고자료:
https://victorydntmd.tistory.com/195
자바 ORM 표준 JPA 프로그래밍 (책)
https://www.javatpoint.com/hibernate-tutorial
