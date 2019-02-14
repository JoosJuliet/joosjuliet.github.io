---
layout: post
section-type: post
title: "JPA에서 Entity란?"
category: Spring
tags: [ 'Spring', 'Java', 'SKEncar', 'JPA' ]
comments: true
---

# Entity란
- JPA entity class는 POJO(Plain Old Java Object)이다.
- 데이터베이스에있는 객체를 나타내는 능력을 가진 것으로 annotated된 일반 자바 클래스.
- JPA를 사용한 database에서 특정 object를 저장하기 위해서 우리는 entity class를 저장해야한다.
- 개념적으로 이는 serialize class와 비슷하며, serialize할 수 있는 능력이 있다는 것을 보여준다.

# 제약조건
- 반드시 no-arg(파라미터가 없는)생성자를 가지고 있어야합니다.

파라미터가 있는 생성자를 가지고 있어도 되지만, 이 경우 반드시 public혹은 protected의 접근자를 가진 no-arg생성자를 선언해주어야 합니다.

직접 정의한 생성자가 하나도 없다면, 따로 생성자를 작성할 필요는 없습니다.


- 엔티티는 최상위 클래스 이어야합니다.
enum이나 interface타입으로 정의해서는 안됩니다.

- 엔티티 클래스는 final이어서는 안됩니다.
메소드가 없거나 영속성 필드가 없는 경우에는 final으로 선언해도 됩니다


---
참고자료:
https://www.objectdb.com/java/jpa/start/entity
https://chan180.tistory.com/167