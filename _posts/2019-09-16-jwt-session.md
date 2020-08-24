---
layout: post
section-type: post
title: "JWT란? JWT인증방식이란? 세션이란? 세션인증방식이란? JWT와 세션의 차이?"
category: Web
tags: [ 'Web' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---
# JWT와 세션이 나온 이유?

http는 steless하다는 특징이 있다. 그래서 각 request들은 연결이 되있지 않다.
하지만 종종 사용자의 정보 중에 정보를 유지하고 싶은 것들이 있다.

예를 들어 요즘 대세인 MBTI 검사를 한다. 문제들은 각 페이지 별로 있을 때 전 페이지에 나온 문제의 답을 사라지기를 원하지 않을 것이다. 우리는 그 상태들을 저장하고 싶다.

즉 우리는 http의 stateless를 극복하고 싶은 것이다.




# 극복 방법
- 세션 인증 방식
- 토큰 인증 방식
그 중 JWT는 토큰 인증방식을 사용한 것이다.




## 세션 인증 방식
![session](/images/2019-09-16-jwt-session/session.png)

세션은 로그인을 통해서 세션의 아이디를 담은 쿠키를 사용자의 브라우저에 저장을 한다. 로그인이 유지되는 동안, 쿠키는 모든 요청에 함께 보내진다. 서버는 쿠키속에 있는 세션 아이디를 memory 속에 있는 정보를 이용해 유저인증을 한 후 정보를 보게 된다.


## 토큰 인증 방식
![token](/images/2019-09-16-jwt-session/token.png)
token은 로그인 할 때 server에서 암호화 키를 이용해 암호화 한 후 JWT 토큰을 보낸다.
그 후 JWT를 사용자의 브라우저에 저장을 한다. 그래서 모든 요청 때 header에 JWT를 포함시켜서 보낸다. 서버는 가지고 있는 암호키를 이용해 복호화를 한다.




## JWT와 세션의 차이(in microservice)

![session-JWT](/images/2019-09-16-jwt-session/jwt-vs-session.png)
왼쪽에 있는 것이 세션이고, 오른쪽이 JWT이다.

JWT와 세션의 차이는 서버를 스케일 아웃을 할 때 차이가 가장 크게 느껴진다.
JWT의 경우 토큰을 발급하는 서버와 인증하는 서버를 나눌 수 있다.
왜냐하면 각 서버들이 복호화 키만 가지고 있다면, 어느 서버에서든 토큰을 복호화 할 수 있기 때문이다. 이에 반해 세션은 로그인을 한 후에 발급되는 것이 토큰이고, 인증을 하는 방법이 메모리에서 비교를 통한 것이기 때문에 반드시 각 서버들이 한 메모리를 바라보고 있어야 한다. 즉 서버를 키울 때 불편하다.




---
참고 :https://medium.com/@sherryhsu/session-vs-token-based-authentication-11a6c5ac45e4
https://showerbugs.github.io/2017-11-16/OAuth-%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C
