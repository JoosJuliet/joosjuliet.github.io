---
layout: post
section-type: post
title: "Title"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)


면졉관이 JPA가 dirty check, life cycle관리 등을 위해  thread 범위 내에서 하는 일이 많아서 느리다는 이야기를 대충 표현했는지도 모르겠군요. 그런데 그게 결국 stateful 한거하고 일맥상통하는 이야기입니다. (ehttps://www.youtube.com/watch?v=2zQdmC0vnFU 아 bulk성 데이터를 핸들링할때라는 전제가 있었습니당~stateful 해서 느리다는건 너무 과한 일반화 아닐까 생각되요. stateful 해서 빠를수도 있는 조건이 있는데요.

dirty check는 뭐 체크할 게 있나 찝적대는 상태
