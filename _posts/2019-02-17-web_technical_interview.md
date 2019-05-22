---
layout: post
section-type: post
title: "[tech interview 5 편] WEB"
categories: Tech_Interview
tags: [ 'interview', 'technology', 'it', 'web' ]
comments: true
---


제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---
이글은 tech interview를 볼 때 기본적으로 물어보는 것들을 정리하기 위해 쓴 글입니다.
깊이 보다는 compact 성을 강조합니다.
---
이 글은 시리즈 물입니다.

[tech interview 1 편] DB https://joosjuliet.github.io/db_technical_interview/  
[tech interview 2 편] JAVA https://joosjuliet.github.io/java_technical_interview/  
[tech interview 3 편] Network https://joosjuliet.github.io/network_technical_interview/  
[tech interview 4 편] Operating System
 https://joosjuliet.github.io/os_technical_interview/  
[tech interview 5 편] WEB https://joosjuliet.github.io/web_technical_interview/  
[tech interview 6 편] SPRING https://joosjuliet.github.io/spring_technical_interview/
---
1. WAS와 웹서버의 차이점은?
- 웹 서버와 WAS를 구별 짓는 것은 동적 서버 콘텐츠를 수행하는가? 만약 수행한다면 WAS로 보면 된다.
- 웹 서버(Web Server)
  - 정적인 HTML이나 이미지를 제공하는 서버.
  - Apache, 엔터프라이즈 서버, Nginx
- WAS(Web Application Server)
  - HTTP를 통해 컴퓨터나, 장치에 애플리케이션을 수행해주는 미들웨어이다.
  - 동적인 처리를 담당하는 서버.
  - Tomcat,
- 실무에서 둘을 연동하여 사용하는데, WAS는 동적 처리에 최적화 되어 있는 서비스이기 때문에처리속도를 위해,  
정적처리는 웹서버에서 처리를 하고, 동적 컨텐츠는 WAS에서 처리한다.


2. 개발시에 중요하다 생각하는 요소를 3가지 기술해 보시오.

3. json이란?
``` javascript
{
    data : 'data1',
    data2 : 'data2',
    ary_data : ['1', '2', '3', '4']
}
```
javascript에서 “{ }” 문법은 객체 리터럴 이다. 즉 위의 코드는 객체를 정의하기 위한 코드이다. json은 객체를 정의하기 위한 문법이라고 볼 수 있다.


---

1번 참고 :
https://unabated.tistory.com/entry/WAS와-웹서버Web-Server-의-차이 [랄라라]
3번 참고 : https://blog.seotory.com/post/2016/04/understand-jsonp
