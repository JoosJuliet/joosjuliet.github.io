---
layout: post
section-type: post
title: "[tech interview 1 편] DB"
categories: Tech_Interview
tags: [ 'interview', 'technology', 'it', 'DB' ]
comments: true
---
이글은 tech interview를 볼 때 기본적으로 물어보는 것들을 정리하기 위해 쓴 글입니다.
깊이 보다는 compact 성을 강조합니다.
---
이 글은 시리즈 물입니다.

[tech interview 1 편] DB https://joosjuliet.github.io/db_technical_interview/  
[tech interview 2 편] JAVA https://joosjuliet.github.io/java_technical_interview/  
[tech interview 3 편] Network https://joosjuliet.github.io/network_technical_interview/  
[tech interview 4 편] Operating System
 https://joosjuliet.github.io/os_technical_interview/  
[tech interview 5 편] WEB https://joosjuliet.github.io/web_technical_interview/  
[tech interview 6 편] SPRING https://joosjuliet.github.io/spring_technical_interview/
---


1. db 정규화란?
관계형 db에서 중복을 최소화하기 위해 db를 구조화하는 작업입니다.

2. 트랜잭션(Transaction)이란 무엇인가?
트랜잭션은 작업의 완전성을 보장해주는 것이다. 즉, 논리적인 작업 셋을 모두 완벽하게 처리하거나 또는 처리하지 못할 경우에는 원 상태로 복구해서 작업의 일부만 적용되는 현상이 발생하지 않게 만들어주는 기능이다.

3. 트랜잭션은 어떠한 특성을 만족해야할까?
Transaction 은 다음의 ACID 라는 4 가지 특성을 만족해야 한다.

- 원자성(Atomicity)
만약 트랜잭션 중간에 어떠한 문제가 발생한다면 트랜잭션에 해당하는 어떠한 작업 내용도 수행되어서는 안되며 아무런 문제가 발생되지 않았을 경우에만 모든 작업이 수행되어야 한다.

- 일관성(Consistency)
트랜잭션이 완료된 다음의 상태에서도 트랜잭션이 일어나기 전의 상황과 동일하게 데이터의 일관성을 보장해야 한다.

- 고립성(Isolation)
각각의 트랜잭션은 서로 간섭없이 독립적으로 수행되어야 한다.

- 지속성(Durability)
트랜잭션이 정상적으로 종료된 다음에는 영구적으로 데이터베이스에 작업의 결과가 저장되어야 한다.


4. 트랜잭션에서 주의해야 할 점은?
트랜잭션의 단위를 너무 작게 하면 속도가 느려지고, 속도를 생각해서 트랜잭션의 단위를 늘리면 dirty read, unrepeatable read, lost update등이 일어날 수 있다.
즉 속도와 트랜잭션은 트레이드 오프되는 것들이다.

5. 교착상태란 무엇인가
복수의 트랜잭션을 사용하다보면 교착상태가 일어날수 있다. 교착상태란 두 개 이상의 트랜잭션이 특정 자원(테이블 또는 행)의 잠금(Lock)을 획득한 채 다른 트랜잭션이 소유하고 있는 잠금을 요구하면 아무리 기다려도 상황이 바뀌지 않는 상태가 되는데, 이를 교착상태라고 한다.

6. Database에서 Index란?

인덱스는 데이터베이스 분야에 있어서 테이블에 대한 동작의 속도를 높여주는 자료 구조를 일컫는다.
고속의 검색 동작뿐만 아니라 레코드 접근과 관련 효율적인 순서 매김 동작에 대한 기초를 제공한다.
인덱스를 저장하는 데 필요한 디스크 공간은 보통 테이블을 저장하는 데 필요한 디스크 공간보다 작다.

---
참고 자료:
https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Database#transaction
http://hahahoho5915.tistory.com/16 [넌 잘하고 있어]
