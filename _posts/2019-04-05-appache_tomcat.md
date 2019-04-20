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


---
참조:
https://madplay.github.io/post/apache-tomcat-modjk   
