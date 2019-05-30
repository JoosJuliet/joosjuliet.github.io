---
layout: post
section-type: post
title: "[JPA] @Embedded, @Embeddable VS @OneToOne"
category: Spring
tags: [ 'Spring', 'JPA', '@Embedded', '@Embeddable' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

이 글의 목표는
- @Embeddable 과 @Embedded 을 언제 쓰는지 명확히 알자
- @OneToOne 과의 차이




# @Embeddable 과 @Embedded 란?

``` java

@Embeddable
public class Address{
}

@Entity
public class Person
{
    @Embedded
    private Address address;
}
```

- Embeddable
  - class에서 이 annotation이 달린 class를 embedded 할 수 있다.
- Embedded
  - 이 annotation이 달린 field는 @Embeddable 이 달린 class를 자신의 class에 넣을 수 있다.




## 가장 많이 쓸 때
- entity가 점점 자라날 때 쪼개고 싶을 때 쓴다.
- table은 쪼개지지 않지만 볼 때는 쪼개볼 수 있었으면 할 때 쓴다.
- 그렇다면 OneToOne과의 차이는?




# @OneToOne 과의 차이
- @OneToOne 은 두개의 DB table들을 매핑하는 것이다.

## @Embedded
- @Embedded objects 들은 언제나 그들의 parents들의 lifecycle에 의해 manage된다.
- 만약 parent가 update나 delete될 때, 그들 역시 그것을 따르게 된다.

## @OneToOne
- @OneToOne 객체는 @Join 주석의 cascadeType 옵션을 통해 composition을 모방 할 수 있지만 기본값은 aggregate 다.
- 즉, 라이프 사이클은 부모 객체의 라이프 사이클과 별개입니다.



# 정리
객체를 쪼개고 싶을 때 주로 @Embedded - @Embeddable, @OneToOne 을 쓴다.
@Embedded - @Embeddable 는 table이 분리되어 있지 않지만 종속관계에 있다.
@OneToOne 은 table도 분리하고, 부모와 자식 객체의 라이프사이클이 하나다.

---
참고:
https://stackoverflow.com/questions/35174981/when-to-use-embedded-and-embeddable
