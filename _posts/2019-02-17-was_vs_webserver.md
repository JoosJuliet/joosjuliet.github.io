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
  - DB 서버와 같이 서비스를 수행
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


---
출처:
https://parkbrother.tistory.com/entry/Web-%EC%84%9C%EB%B2%84%EC%99%80-Was-%EC%84%9C%EB%B2%84%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90  
