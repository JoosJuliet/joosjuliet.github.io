---
layout: post
section-type: post
title: "many to many"
category: Spring
tags: [ 'spring', 'java' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

# many to many
기본 으로 생각하면 employee랑 resort가 many to many의 relation이긴하다.

그런데 jpa many to many는 join된 table이 hide 될 수 있다고 한다.



이론적으로 many-to-many database는

두개의 parent table를 foreign key로 reference를 하는 것을 가지고 있는 세번째 table이 있다.

이걸 구현하는 두가지 방법이 있는데

1.  java.util.List 2. java.util.Set

이 있다.

Usingjava.util.List
- that don’t entail any specific ordering.


참고문헌: https://vladmihalcea.com/the-best-way-to-use-the-manytomany-annotation-with-jpa-and-hibernate/
