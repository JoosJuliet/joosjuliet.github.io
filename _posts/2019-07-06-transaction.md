---
layout: post
section-type: post
title: "[1편] 트랜잭션 (트랜잭션의 정의, 대상, ACID)"
category: Algorithm
tags: [ 'transaction' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---
*이 글은 시리즈물 입니다.*
- [1편] 트랜잭션 (트랜잭션의 정의, 대상, ACID)
  - https://joosjuliet.github.io/transaction/  
- [2편] DB에서의 트랜잭션( 제어어(TCL)[COMMIT, ROLLBACK, SAVEPOINT], mysql에서의 트랜잭션)
  - https://joosjuliet.github.io/tcl/
- [3편] SPRING에서의 트랜잭션(jpa에서 transaction이란)
  - https://joosjuliet.github.io/jpa_transaction/  
---

# 트랜잭션(transaction)
- 데이터베이스의 상태를 변화시키기 해서 수행하는 작업의 단위를 뜻한다.

# ACID
- 트랜잭션의 특성
- Atomicity
  - All or nothing
- Consistency
  - Consistent한 상태의 데이터 베이스가 트랜잭션이 완료된 후에도 또 다른 Consistent 상태(특정 제약조건이나 cascade나 trigger 같은 것들이 만족된 상태)로 바뀐다. => transaction 실행 하기전에 가져온 data는 transaction에서 transaction 하기 전의 data를 부른다면 그 상태가 유지된다.
- Isolation
  - 트랜잭션이 하나 실행되는 동안 다른 트랜잭션이 실행 되지 못한다.
- Duration
  - 한 트랜잭션이 한번 완료되면 이 트랜잭션이 갱신한 것은 그 이후에 시스템에 고장이 발생하더라도 손실되지 않는다. 성공적으로 트랜잭션이 적용되면 영원히 적용된다.
