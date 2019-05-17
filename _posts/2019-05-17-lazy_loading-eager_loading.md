---
layout: post
section-type: post
title: "lazyloading이란?, fetch type - 로딩기법(lazy loading, eager loading)"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---


# 기본적으로 lazyloading이란?
- Lazy loading은 객체가 필요한 시점까지 객체 초기화를 연기하기 위해 컴퓨터 프로그래밍에서 일반적으로 사용되는 디자인 패턴

- 필요한 정보 만 필요한 부분을로드하는 개념을 나타 내기 위해 데이터베이스에서 자주 사용되는 용어입니다.
- 여러 테이블을 조인 한 레코드가 필요하다고 가정합니다.
- 한 번에 모두 가져 오면 주 테이블 만 가져 오는 것보다 오래 걸릴 것입니다.
- lazy-loading을 사용하면 나머지 정보는 필요한 경우에만 가져옵니다. 따라서 특정 시나리오에서는 실제로 '효율적인로드'입니다.

참고자료 : https://code.i-harness.com/ko-kr/q/8db2


이걸 spring에서 적용해보자

# 즉시로딩은 뭔가?
- 엔티티 매니저를 통해 엔티티를 조회하면 연관관계에 매핑되어 있는 엔티티도 함께 조회


아래와 같이 Member 테이블에 Phone 엔티티가 즉시로딩 전략으로 설정되어 있다고 하자.
이와같이 설정이 되어 있을 때 Member 엔티티를 조회하게 되면 Member에 속한 Phone 엔티티들도 함께 조회된다.
조회가 되면 Member와 Phone 엔티티는 영속성 컨텍스트내에 영속 상태로 존재한다.

``` java
@OneToMany(fetch = FetchType.EAGER, cascade = CascadeType.PERSIST, mappedBy = "member")
private Collection<Phone> phones = new ArrayList<>();
```

# 지연로딩은 뭔가?
- 엔티티 매니저를 통해 엔티티를 조회하면 연관관계에 매핑되어 있는 엔티티를 실제 사용할 때 조회

이번에는 지연 로딩 설정으로 되어 있다고 하자.
다음과 같이 설정이 되어 있을 때 Member 엔티티를 조회하게 되면 Phone 엔티티는 DB에서 조회하지 않는다.
그렇다고 phones 인스턴스가 null로 되어 있지는 않다. proxy 형태로 생성되어 있을 뿐이다.
실제 Phone 엔티티가 초기화 되는 시점은 phones.get(0).getId() 와 같이 엔티티를 사용했을 때이다.

``` java
@OneToMany(fetch = FetchType.LAZY, cascade = CascadeType.PERSIST, mappedBy = "member")
private Collection<Phone> phones = new ArrayList<>();
```

## 구체적 예제

지연 로딩과 즉시 로딩은 어떻게 사용될 수 있을까요?
- 페이스북 " 댓글 더보기 "에서 즉시 로딩을 사용할 경우 " 댓글 더보기 "를 누르지 않았음에도 이미 댓글이 조회 돼버리기 때문에 성능이 느려질 수 있습니다.
- 이 때는 " 댓글 더보기 "를 클릭 했을 때 댓글 목록을 불러오도록 하는 지연 로딩 방식이 좋을 것입니다.

- 반면 쇼핑몰에서는 장바구니에서 유저와 상품을 같이 보여줘야 하므로 즉시 로딩 방식을 사용하면 좋겠죠.





# Fetch 기본 전략

@ManyToOne , @OneToOne 어노테이션의 경우 FetchType.EAGER ( 즉시로딩 )을 기본 전략으로 사용하며,
@OneToMany, @ManyToMany 어노테이션의 경우 FetchType.Lazy ( 지연로딩 )을 기본 전략으로 사용합니다.





성능 면에서 지연 로딩을 사용하는 것이 더 좋기 때문에 애플리케이션 개발 시 모두 지연 로딩으로 한 뒤에,
성능 최적화가 필요한 부분을 즉시 로딩으로 바꿔주면 좋을 것입니다.



---

출처: https://victorydntmd.tistory.com/210 [victolee]

출처: https://lng1982.tistory.com/m/278
