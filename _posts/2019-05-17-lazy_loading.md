---
layout: post
section-type: post
title: "lazy loading이란? getOne과 findOne차이?"
category: Spring
tags: [ 'Spring', 'JPA' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

# lazyloading이란?
- Lazy loading은 객체가 필요한 시점까지 객체 초기화를 연기하기 위해 컴퓨터 프로그래밍에서 일반적으로 사용되는 디자인 패턴

- 필요한 정보 만 필요한 부분을로드하는 개념을 나타 내기 위해 데이터베이스에서 자주 사용되는 용어입니다.
- 여러 테이블을 조인 한 레코드가 필요하다고 가정합니다.
- 한 번에 모두 가져 오면 주 테이블 만 가져 오는 것보다 오래 걸릴 것입니다.
- lazy-loading을 사용하면 나머지 정보는 필요한 경우에만 가져옵니다. 따라서 특정 시나리오에서는 실제로 '효율적인로드'입니다.

참고자료 : https://code.i-harness.com/ko-kr/q/8db2


# getOne vs findOne
- getOne() 은 lazy-loading 을 통해 객체를 전달한다.
  - getOne API에 따르면 지정된 식별자를 사용하여 엔터티에 대한 참조를 반환합니다.
- findOne() 은 즉시 조회하여 객체를 전달한다.
  - findOne API에 따르면 해당 ID로 엔티티를 검색합니다.

## findOne을 써야만 할 때?
- getOne 메소드는 DB (lazy loading)의 참조만을 반환합니다.
- 따라서 기본적으로 트랜잭션 외부에 있습니다 (서비스 클래스에서 선언 한 Transactional 은 고려되지 않습니다).
- 그래서 오류가 발생할 수 있...지만? 언제? 단지 값만 가져오는 건데?




# JPA getOne 스펙은 아래와 같다.

## getOne
```
T getOne(ID id)
```


- Returns a reference to the entity with the given identifier.
- 파라미터 id는 null일수 없고 , 주어진 구분자에의한 엔티티 참조(프록시를 얘기하는 듯)를 리턴하며, 엔티티가 없을경우 EntityNotFoundException을 던진다.

See Also: EntityManager.getReference(Class, Object)
- 또한 내부적으로 EntityManager.getReference를 사용하는데. EntityManager.getReference는 프록시 객체를 리턴한다.
- 때문에 getOne에서 리턴하는 것도 프록시 객체이고, getOne()에서 리턴된 객체의 null체크는 의미가 없다.

- 그렇기 때문에 lazy-loading되는 시점에 NotFoundEntityException을 발생하는 것으로 볼 수 있다.
- 사실 이 NotFoundEntityException도 EntityManager.getReference()로 부터 발생된다.

### getReference
```

<T> T getReference
(java.lang.Class<T> entityClass,java.lang.Object primaryKey)

```

Get an instance, whose state may be lazily fetched. If the requested instance does not exist in the database, the EntityNotFoundException is thrown when the instance state is first accessed. (The persistence provider runtime is permitted to throw the EntityNotFoundException when getReference is called.) The application should not expect that the instance state will be available upon detachment, unless it was accessed by the application while the entity manager was open.

상태가 느슨하게 페치 (fetch) 될 가능성이있는 인스턴스를 취득합니다. 요청 된 인스턴스가 데이터베이스에 없으면 인스턴스 상태에 처음 액세스 할 때 EntityNotFoundException이 발생합니다. (getReference가 호출 될 때 The persistence provider 런타임은 EntityNotFoundException을 던질 수 있습니다.) 애플리케이션은 엔티티 관리자가 열려있는 동안 애플리케이션이 액세스하지 않는 한 인스턴스 상태가 분리 될 때 사용할 수 있다고 기대해서는 안됩니다.

#### Parameters:
entityClass - entity
classprimaryKey - primary key

#### Returns:
the found entity instance

#### Throws:
IllegalArgumentException - if the first argument does not denote an entity type or the second argument is not a valid type for that entity’s primary key or is nullEntityNotFoundException - if the entity state cannot be accessed

# 다음 findOne()의스펙을 보자
- 파라미터 id는 null이면 안되고, 주어진 id로 엔티티를 리턴하고 또한 못찾는다면 null을 리턴한다,
- 파라미터 id가 null일 경우 IllegalArgumentException을 던진다.
- 내부적으로 EntityManager에 접근한다.
- lazy-loading 된 proxy 객체를 사용하려 할때는 getOne()을 써야겠다.



참고: https://medium.com/@circlee7/jpa-getone-id-findone-id-aa9676dc666d
