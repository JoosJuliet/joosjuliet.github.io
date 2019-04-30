---
layout: post
section-type: post
title: "브라우저에 네이버를 치면 무슨 일이 일어날까?"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

---

브라우저 구성
- 브라우저 엔진
- js 해석기(v8)
- web storage
- rendering engine

> 쿠키 vs local storage
- 쿠키는 헤더 포함시켜 보낸다.
10메가 쓴다. 쿠키는 정보선택해서 보낼 수 없이 다보낸다
- local storage는 브라우저 내부에서만 쓰인다.
40메가 쓴다. local storage는 선택해서 보낸다.


Interface
browser engine
rdndering engine   storage
js 해석기 / 통신/ it backend


브라우저 엔진은 https://www.naver.com 을 본다.
http는 정해진 규약이 잇어서 그걸로 (header,body이런것을 찾아서)해석한다.
그래서 request message만든다.
# dns
근데 domain을 ip로 바꾸는게 필요하다.
그것이 dns로 간다. 일반적으로 udp를 쓴다.
쓰는 이유는 빠르다.
- tcp를 쓸 때도 있다.(udp의 정보가 512byte넘으면 tcp를 쓴다., 존트랜스퍼상황())

## dns 네가지 있다.
- 1. local dns
- 2. naver.com dns server
- 3. .com server있다.(.kr, .me, org)
  - dns 하이어아키텍처로 있다.
- 4. root dns server
  - 전세계 5대 있어서 터지면 큰일나
  - 안터질려고 udp쓴다.
  - tcp쓰면 너무 3way handshake해서 너무 많다.

### dns는 table을 통해서 어느 129.9.9.1로 가야하는지에 대한 table 있다.
### local dns는 도메인 정보를 캐싱한다.
 -> naver를 한번 들어왔던 애는 다음번에는 캐싱이 되서 빨리온다.
### layer역할을 한다.
어차피 비지니스 로직은 다른 layer에서 한다. 그래서 여러 ip로 해도 상태관리가 안되도 괜찮다.

tcp, udp 모두 소켓통신의 종류이다.

# 이제 ssl이 있다.
dns통해서 ip얻어온다음에 ssl(tls)layer한다.

# 소캣통신한다.


## 소켓통신이란?
소캣을 만들어야한다.
소켓은 입구이다.
소켓통신은 클라에 구멍판다. 서버에 구멍판다.
구멍이 소켓이고, 이걸 땅을 파서 파이프 연결을 한다.
구멍 말고도 버퍼란게 잇다.

## 소켓통신과정
- 서로 연결하는 것은 3way handshake이다.

sync는 tcp header에 들어있다.
- 서로 끊는 것은 4 way handshake
