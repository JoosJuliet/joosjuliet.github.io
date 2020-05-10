---
layout: post
section-type: post
title: "http의 개념, https가 생긴 이유, http와 https의 차이"
category: Computer_science
tags: [ 'computer_science', 'network', '글또3기' ]
comments: true
---
https를 알기 앞서 http를 먼저 설명 고!

# HTTP(HyperText Transfer Protocol)란?
HTTP는 클라이언트와 서버 사이에 이루어지는 요청/응답(request/response) 프로토콜이다.


# HTTP의 큰 특징인 Connectless & Stateless
HTTP는 Connectless 방식으로 작동한다. 서버에 연결하고, 요청해서 응답을 받으면 연결을 끊어버린다.  
기본적으로는 자원 하나에 대해서 하나의 연결을 만든다. 이런 작동방식은 각각 아래의 장점과 단점을 가진다.  
- 장점 : 불특정 다수를 대상으로 하는 서비스에 적합한 방식이다. 수십만명이 웹 서비스를 사용하더라도 접속유지는 최소한으로 할 수 있기 때문에, 더 많은 유저의 요청을 처리할 수 있다.
- 단점 : 연결을 끊어버리기 때문에, 클라이언트의 이전 상태를 알 수가 없다. 이러한 HTTP의 특징을 stateless라고 하는데, connectless로 부터 파생되는 특징이라고 할 수 있다. 클라이언트의 이전 상태 정보를 알 수 없게 되면, 웹 서비스를 하는데 당장에 문제가 생긴다. 예컨데, 클라이언트가 과거에 로그인을 성공하더라도 로그 정보를 유지할 수가 없다. HTTP는 cookie를 이용해서 이 문제를 해결하고 있다.


http에 대한 자세한 정보는  
https://joosjuliet.github.io/http/  
여기에서 봐 주시길 바랍니다.  



# HTTPS란?
## HTTP의 보안적 취약점은?
HTTP는 평문 데이터를 기반으로 하기 때문에, 유저정보와 같은 민감한 정보가 인터넷 상에 그대로 노출된다.  
또한 http의 큰 특징인 connectless이기 때문에, 클라이언트를 정확히 판단할 수 없다.
그래서 중간자 공격(Man-in-the-middle attack)을 할 수 있게 된다.  
이를 막기 위한 방법 중 하나가 바로 https이다.  


*참고* 중간자 공격이란?  
서버와 클라이언트 사이에서 데이터 전송이 이루어지는 동안 공격자가 두 사이에 자신을 배치하고 데이터를 가로채 잘못된 정보를 전달하는 것이라고 할 수 있다.  
양측이 서로 이야기하고 있다고 믿고 있지만 실제로는 가해자와 소통을 해 일어나는 일이다.


## 그래서 HTTPS의 역할은?
정보는 중간에 수집되거나 변조될 수 있는 중간자 공격을 막기 위해 HTTPS 통신을 해 SSL 인증서를 이용해서, 접속 사이트를 신뢰할 수 있는지 평가할 수 있다.
https는 SSL프로토콜 내부에서 돌아가는 프로토콜입니다.

## HTTPS란?

![https](/images/2019-09-08-http_vs_https/https.png)

SSL은 데이터 보안을 위해서 개발한 통신 레이어다.  
HTTPS는 SSL 레이어 위에 HTTP를 통과 시키는 방식이다. 
즉 평문의 HTTP 문서는 SSL 레이어를 통과하면서 암호화 돼서 목적지에 도착하고, 목적지에서는 SSL 레이어를 통과하면서 복호화 돼서 웹 브라우저에 전달된다. 
또한 SSL은 표현계층의 프로토콜로 응용 계층 아래에 있기 때문에, 어떤 응용 계층의 데이터라도 암호화해서 보낼 수 있다.  


간혹 HTTPS를 하나의 프로토콜로 인식하기도 하는데, HTTP와 SSL은 전혀 다른 계층의 프로토콜의 조합이다. HTTPS over SSL로 보는게 좀더 정확한 시각이다.





*참고* OpenSSL이 뭘까??
보통의 경우 웹서비스에 https를 적용할 경우 SSL인증서를 VeriSign라는 곳에서 발급받아야 하는데, 이때 비용이 발생하기 때문에 실제 운영서버가 아니면 발급 받기에 부담이 될 수 있다.  
이 때 OpenSSL을 사용하여 인증기관을 직접 만들고, Self Signed Certificate 를 생성하고, SSL인증서를 발급하면 된다.   
발급된 SSL인증서는 Apache httpd 등의 웹서버에 설치해서 쉽게 https의 서비스를 이용할 수 있다.  

---
참고자료

http에 대한 설명  
https://ko.wikipedia.org/wiki/HTTP  
https://www.joinc.co.kr/w/Site/Network_Programing/AdvancedComm/HTTP +https설명까지  

중간자 공격 설명  
https://blog.naver.com/PostView.nhn?blogId=ucert&logNo=221201640816&categoryNo=37&parentCategoryNo=0  
