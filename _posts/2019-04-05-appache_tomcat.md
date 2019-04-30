---
layout: post
section-type: post
title: "[WAS와 Web-server 2편]Appache와 Tomcat은 무슨관계인가?"
category: Web
tags: [ 'Web', 'WAS', 'web_server' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

이 글은 시리즈 물입니다.
1편 : https://joosjuliet.github.io/was_vs_webserver/  
2편 : https://joosjuliet.github.io/appache_tomcat  
---

# 아파치(Apache)란?
대부분의 운영체제에서 운용이 가능하며 오픈소스 라이선스를 가지고 있어 자유롭게 사용할 수 있습니다. 쉽게 말해서 표현한다면 웹 서버(Web Server)

# 톰캣Tomcat이란?
아파치 소프트웨어 재단에서 개발한 서블릿 컨테이너만 있는 웹 애플리케이션 서버를 말합니다.
WAS(Web Application Server)라고 말하는데, 이는 웹 서버와 웹 컨테이너의 결합으로 다양한 역할을 수행할 수 있는 서버를 말합니다.
클라이언트의 요청이 들어오면 내부의 실행 결과를 만들어내고 이를 다시 전달해주는 역할을 합니다.

# 톰켓의 디렉토리 구조
- bin
  - 톰캣 서버 실행과 관련된 쉘 스크립트 파일 (.sh, bat 등)을 모아둔 곳입니다.
- conf
  - 톰캣 서버를 실행할 때 참조할 설정 파일을 모아둔 곳입니다.
- lib
  - 톰캣 서버를 구성하는 자바 클래스(classs) 라이브러리들을 모아둔 곳입니다.
- logs
 - 톰캣 서버를 실행하는 동안 실행 정보와 오류 정보를 기록한 파일을 모아둔 곳입니다.
 - client로부터 get 요청이 들어왔는지 post 요청이 들어왔는지도 알 수 있고 마지막으로 요청한 정보가 무엇인지, ip address는 어떻게 되는지 등도 알 수 있습니다.
- temp
  - 톰캣 서버가 실행하는 동안 임시 데이터를 보관하는 디렉토리입니다.
- work
  - 톰캣 서버가 JSP를 실행할 때 그 중간 파일을 보관하는 곳입니다.
- webapps
  - 웹 애플리케이션을 모아둔 곳입니다.

---
참조:
https://madplay.github.io/post/apache-tomcat-modjk   
출처:
톰켓의 디렉토리구조 : https://uoonleen.tistory.com/59
