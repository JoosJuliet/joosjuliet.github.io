---
layout: post
section-type: post
title: "WAS와 웹서버(WAS 도입효과)"
category: Web
tags: [ 'Web', 'WAS', 'web_server' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)


<span style="background-color:yellow"><b> 웹 서버와 WAS를 구별 짓는 것은 동적 서버 콘텐츠를 수행하는가? 만약 수행한다면 WAS로 보면 된다. </b></span>


# 웹 서버(Web Server)
- <span style="background-color:yellow"><b>정적인 HTML이나 이미지를 제공하는 서버.</b></span>
- 클라이언트로부터 HTTP 요청을 받아들이고, HTML 문서와 같은 웹 페이지를 정적으로 처리해 반환하는 프로그램
- 웹 페이지를 클라이언트로 전달하고, 클라이언트로부터 컨텐츠를 전달 받는 역할
- 인증, 정적 컨텐츠 관리, HTTPS지원, 컨텐츠 압축, 가상 호스팅, 대용량 파일 지원 등의 기능을 지원
- Apache, 엔터프라이즈 서버, Nginx




# WAS(Web Application Server)
  - <span style="background-color:yellow"><b>HTTP를 통해 컴퓨터나, 장치에 애플리케이션을 수행해주는 미들웨어</b></span>
  - <span style="background-color:yellow"><b>동적인 처리를 담당하는 서버</b></span>
  - DB와 연결되어 데이터를 주고 받거나 프로그램으로 데이터 조작이 필요한 경우에는 WAS를 활용 해야 한다.
  - 분산 트랜잭션, 보안, 메시징, 쓰레드 처리 등의 기능 처리
  - Tomcat
- 실무에서 둘을 연동하여 사용하는데, WAS는 동적 처리에 최적화 되어 있는 서비스이기 때문에처리속도를 위해,  
정적처리는 웹서버에서 처리를 하고, 동적 컨텐츠는 WAS에서 처리한다.


## WAS의 일반적인 기능
  - Web 환경을 위한 n-tier Architecture 플랫폼
  - GUI과 Business Logic의 분리 운영
  - Thread 관리
  - 부하조절(Load Balancing) 기능 지원
  - 장애대책(Fail-Over) 기능 지원
  - Transaction 처리 자동화
  - Web Service 플랫폼으로써의 역할




# WAS 도입효과
- 안정된 시스템 구성
  - 안정적 서비스 보장, 자동적인 어플리케이션 복구 기능 제공, 업무 로직이 중간 어플리케이션 서버에 존재, 쉽고 빠르게 구축
- DB성능 보장
  - WAS서버가 DB서버와의 최적 사용 조절화, DB connection pool을 조절해 DB connection 관리 및 트랜잭션 처리
- 비용절감
  - 서버 리소스의 원활한 사용




  아파치(Apache)란 무엇일까?
  1995년 처음 발표된 WWW(World Wide Web) 서버용 소프트웨어를 말합니다. 대부분의 운영체제에서 운용이 가능하며 오픈소스 라이선스를 가지고 있어 자유롭게 사용할 수 있습니다. 쉽게 말해서 표현한다면 웹 서버(Web Server)라고 표현하면 되겠네요.




  톰캣(Tomcat)이란 무엇일까?
  그렇다면 톰캣은 무엇일까요? 아파치 소프트웨어 재단에서 개발한 서블릿 컨테이너만 있는 웹 애플리케이션 서버를 말합니다. WAS(Web Application Server)라고 말하는데, 이는 웹 서버와 웹 컨테이너의 결합으로 다양한 역할을 수행할 수 있는 서버를 말합니다. WebLogic, Jeus, Tomcat 등이 있답니다. (Tomcat을 WAS라고 보면 안 된다는 의견도 있지만! 우선 WAS라는 관점으로 봅시다.) 클라이언트의 요청이 들어오면 내부의 실행 결과를 만들어내고 이를 다시 전달해주는 역할을 합니다.


https://madplay.github.io/post/apache-tomcat-modjk

그렇다면 왜 아파치와 톰캣을 연동할까?
"왜 WAS만 사용하지 않고 웹 서버와 같이 사용할까?"
WAS


만일 웹 서버가 없이 WAS만 사용한다고 가정해봅시다.
웹 페이지(Web Page)에는 정적인 리소스뿐만 아니라 동적인 리소스가 함께 존재합니다. WAS의 정적 데이터 처리로 인해 동적 데이터에 대한 처리는 늦어지게 될 것이고 결과적으로 본다면 클라이언트의 요청에 대한 응답 시간은 전반적으로 늘어나게 될겁니다.

그러니까 사용 목적에 따라 다르다고 볼 수 있는데요. HTML 파일이나 이미지 파일과 같은 정적 컨텐츠들은 WAS까지 거치는 것보다 웹 서버를 바로 통하는 것이 더 빠릅니다. 이러한 맥락으로 본다면 웹서버인 아파치와 WAS인 톰캣을 연동하여 각자의 역할 분담이 가능하므로 더 좋겠지요? 또! 하나의 웹 서버에 여러 개의 톰캣을 연결해서 분산시킬 수 있는 로드 밸런싱(Load Balancing)을 구현할 수도 있습니다.


이글이 제일 was랑 webserver설명과 톰캣과 아파치 설명이 명확하다

https://uroa.tistory.com/67?category=657568

spring mvc에 대한 설명이 명확하다
https://uroa.tistory.com/68?category=657568
---
출처:
https://parkbrother.tistory.com/entry/Web-%EC%84%9C%EB%B2%84%EC%99%80-Was-%EC%84%9C%EB%B2%84%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90  
