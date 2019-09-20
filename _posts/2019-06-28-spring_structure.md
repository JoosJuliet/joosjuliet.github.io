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

service layer 를 만들어야 하는 이유


두 도메인과 만나는 로직은 service에 넣는다.
한 도메인 가지고만 할 때는 domain에다가 넣는다. 간단하게, 데이터베이스에서 가져 오는 데이터를 조작할 때



1) @Controller -> 이것으로 주석 된 클래스는 클라이언트 측으로부터 요청을 수신하기위한 것입니다. 첫 번째 요청은 @RequestMapping annotation의 값을 사용하여 요청을 특정 컨트롤러로 전달하는 Dispatcher Servlet에 제공됩니다.

2) @Service -> 이것으로 주석 된 클래스는 클라이언트에서 수신하거나 데이터베이스에서 가져 오는 데이터를 조작하기위한 것입니다. 모든 조작은이 레이어에서 수행해야합니다.

3) @Repository -> 이것으로 주석 된 클래스는 데이터베이스와 연결하기위한 것입니다. DAO (Data Access Object) 계층으로 간주 될 수도 있습니다. 이 계층은 CRUD (작성, 검색, 갱신, 삭제) 조작으로 만 제한되어야합니다. 조작이 필요한 경우 데이터를 @Service 계층으로 다시 보내야합니다.


참고 :https://softwareengineering.stackexchange.com/questions/348661/should-i-use-a-layer-between-service-and-repository-for-a-clean-architecture-s
