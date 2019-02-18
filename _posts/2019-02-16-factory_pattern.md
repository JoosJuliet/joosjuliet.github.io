---
layout: post
section-type: post
title: "Factory Pattern(팩토리 패턴)이란?(feat. Java)"
category: Spring
tags: [ 'Java', 'SKEncarLunchStudy', 'ProxyPattern', 'DesignPattern' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)



객체를 만들어내는 부분을 서브 클래스(Sub-Class)에 위임하는 패턴.
즉, new 키워드를 호출하는 부분을 서브 클래스에 위임하는 겁니다. 결국 팩토리 메소드 패턴은 객체를 만들어내는 공장(Factory 객체)을 만드는 패턴이라 이해하면 됩니다.
참고 : https://blog.seotory.com/post/2016/08/java-factory-pattern
