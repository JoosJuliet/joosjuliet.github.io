---
layout: post
section-type: post
title: "spring_structure"
category: Spring
tags: [ 'spring', 'java' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

service layer가 있는지도 모르고 뛰어넘었었다.



Front end <--> API Service -> Service -> Repository -> DB

Front end: web client, mobile apps
API Service: Rest Controllers, here I use converters call and
Service: Interfaces with implementations and they contain business logic
Repository: Repository interfaces with automatically by spring data which CRUD operationsand maybesome queries )and maye qupring data whan



참고 :https://softwareengineering.stackexchange.com/questions/348661/should-i-use-a-layer-between-service-and-repository-for-a-clean-architecture-s
