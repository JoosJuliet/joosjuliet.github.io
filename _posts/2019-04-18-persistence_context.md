---
layout: post
section-type: post
title: "[JPA]영속성 컨텍스트 (Persistance Context)"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

# Persistance Context
- Entity를 영구 저장하는 환경, 논리적 개념


## Entity Manager
- Entity 저장, 조회 시 Entity Manager는 영속성 컨텍스트에 Entity 보관, 관리
- persist()
  - Entity Manager의 method는 Entity Manager를 사용해 회원 Entity를 영속성 context에 저장
- 생성 시 하나 만들어진다.



# Entity 생명주기
- 비영속


# ORM
- 객체 연관관계, 테이블 연관관계 매핑
- 방향(Direction)
  - 단방향 : 회원 -> 팀  or 팀 -> 회원 한쪽만 참조
  - 양방향 : 회원 -> 팀 and 팀 -> 회원 서로 참조

테이블은 *항상* 양방향이다.
- 다중성(Multiplicity)
  - 다대일
    - 여러 회원을 한 팀에 속하므로 회원, 팀
  - 일대다
    - 한 팀에 여러 회원 소속, 팀과 회원
  - 일대일
  - 다대다


연관관계의 주인 : 양방향시 주인을 정해야 한다.


<!-- generic은 미리 선언해놓고 object값을 캐스팅해서 쓰게 한다.
그게 generic method 이다. -->
