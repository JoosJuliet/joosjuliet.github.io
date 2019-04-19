---
layout: post
section-type: post
title: "스트레티지 패턴(Strategy Pattern)"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

---

인터페이스를 이용하여 객체간의 느슨한 결합(Loose Coupling)을 권장했다. 즉 상속을 통한 구현이 아닌 구성(Composition)을 이용한 것이다. 구성이란 A에 B가 있다 라는 것을 의미하며 한 객체에 객체를 포함시키는 것이 아닌 인터페이스를 포함하는 방식으로 많이 사용된다.

# 전략 패턴의 정의
간단하게 말해 어떤 동작을 하는 로직을 정의하고 이것들을 하나로 묶어서(캡슐화) 관리하도록 하는 패턴
로직을 사용하는 객체들은 자기의 입맛에 맞게 로직을 효율적으로 수정할 수 있다. 새로운 로직을 추가하거나 변경할 때 객체의 종류 수 만큼 반복하지 않고, 단 한번으로 반영할 수 있다.

# 예시
여기의 핵심은 행동 역시 객체선언하는 것이다.
그리고 상속보다는 composition을 이용한다.

핵심은
- 로직을 정의하는 행동에도 객체를 선언
- 상속보다는 구성(Composition) 을 이용
- Interface와 로직의 class와의 관계를 composition 하고 유닛에서 상황에 맞는 로직을 쓰게끔 유도


---

https://hyeonstorage.tistory.com/146 ->여기에서 4번 보여주기


https://flowarc.tistory.com/entry/1-Strategy-Pattern

출처: https://flowarc.tistory.com/entry/디자인-패턴-옵저버-패턴Observer-Pattern [Jamin's Dev log]
