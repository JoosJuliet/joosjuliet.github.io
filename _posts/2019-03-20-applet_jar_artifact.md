---
layout: post
section-type: post
title: "[legacy 환경설정으로 얻은 지식들] Applet이란?, JAR파일이란?, WAR파일이란?, Artifact란? "
category: Spring
tags: [ 'Spring', '환경설정', 'SKencar' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

---

# 1. Applet이란?

- 플러그인의 하나로서 전용 위젯 엔진이나 더 큰 프로그램 범위 내에서 실행되는 특정한 작업을 수행하는 조그마한 응용 프로그램
- 웹 브라우저, 제어판과 같은 다른 프로그램에서 실행되는 소프트웨어 구성 요소
- 애플릿은 독립적으로 사용되지 않으며 작은 기능을 가지고 있다.
- 이것은 1993년 애플스크립트에서 처음 도입된 용어
- "서블릿" 같은 한 종류의 클라이언트 플랫폼에서만 동작
- 애플릿의 컨테이너에 의해 기능이 제한
- 스크립트 언어가 아닌 컴파일 가능 언어로 작성되므로 성능 향상이나 다양한 기능을 가져올 수 있다.




# 2. JAR(Java™ Archive)
## JAR 파일이란?
- JAR은 old Unix utility 중 tar을 근간으로 만든 archiving tool이다.
- 여러개의 파일을 하나의 파일로 묶는 JAR명령을 사용하여 생성된다.
- 웹브라우저에서 빠르게 다운로드 할 수 있도록, 클래스, 이미지 및 사운드 파일들을 하나의 파일에 압축하여 담고 있는 파일이다.
- 일반적으로 JAR 파일에는 애플릿 및 응용 프로그램과 관련된 클래스 파일과 보조 리소스가 들어 있다.
- 파일들을 하나의 파일에 압축하여 담으면 다운로드 소요 시간이 절약된다.
- 이렇게 archive 파일로 묶는 이유는 자바로 개발한 여러클래스 파일들 또는 패키지 파일이 있을때, 이를 하나로 묶으면 그 클래스들을 참조하기도 편하고, 다운 받기도 쉽다.


## JAR 파일의 장점
- Security: JAR 파일의 내용을 디지털 서명 할 수 있습니다. 그런 다음 서명을 인식 한 사용자는 필요하지 않은 소프트웨어 보안 권한을 선택적으로 부여 할 수 있습니다.
- Decreased download time: 애플릿이 JAR 파일에 번들되어있는 경우 애플릿의 클래스 파일과 관련 리소스는 각 파일에 대한 새 연결을 열지 않고도 단일 HTTP 트랜잭션으로 브라우저에 다운로드 할 수 있습니다.
- Compression: JAR 형식을 사용하면 효율적인 저장을 위해 파일을 압축 할 수 있습니다.
- Packaging for extensions: 확장 프레임 워크는 Java 핵심 플랫폼에 기능을 추가 할 수있는 수단을 제공하며 JAR 파일 형식은 확장 용 패키지를 정의합니다. JAR 파일 형식을 사용하면 소프트웨어를 확장 기능으로 사용할 수 있습니다.
- Package Sealing: JAR 파일에 저장된 패키지는 패키지가 버전 일관성을 유지할 수 있도록 선택적으로 봉인 될 수 있습니다. JAR 파일 내에서 패키지를 봉인하는 것은 해당 패키지에 정의 된 모든 클래스가 동일한 JAR 파일에서 발견되어야 함을 의미합니다.
- Package Versioning: JAR 파일은 공급 업체 및 버전 정보와 같이 포함 된 파일에 대한 데이터를 보유 할 수 있습니다.
- Portability: JAR 파일을 처리하는 메커니즘은 Java 플랫폼의 핵심 API의 표준 부분입니다.


## Zip 파일과 다른 점
Zip은 압축을 하는 utility로 보관 기능이 중점이다.




# 3. WAR(WebApplication Archive)란?
<span style="background-color:yellow"><b>웹 어플리케이션을 지원하기 위한 압축방식</b></span>
- ~~web archive war는 jar과 이름만 비슷함으로 헷갈릴 필요도 없다~~
- 웹 어플리케이션 저장소이며 웹 어플리케이션을 압축해 저장해 놓은 파일
- 개발한 웹어플리케이션 프로젝트가 <b>WAS에서 돌아갈 수 있는 구조</b>를 담고 있으며 jsp, servlet, gif, html, jar 등을 압축하고 지원해준다.
- jar와 같은 맥락으로 servlet context 접근을 위해 관련된 모든 파일들을 패키지화해준다.


## 배포
WAS에 웹 어플리케이션을 배포하기 위해서는 톰캣을 기준으로 다음의 세가지 방법이 있습니다.
- 1. 웹 어플리케이션 프로젝트 그대로 복사하여 WAS webapps 폴더 하위에 복사하여 배포
  - 웹 어플리케이션 규모가 크고 서버가 외부에 있는 경우 수많은 폴더들과 파일을 통째로 옮겨야 하기 때문에 번거롭다.
- 2. 프로젝트.war 로 압축하여 webapps 폴더 하위에 복사한 후 톰캣을 기동하여 자동 배포
- 3. 톰캣 관리자 페이지에서 프로젝트.war 파일을 등록하여 자동으로 배포

- 2,3번의 경우에는 로컬에서 개발하여 FTP 등을 통해 원격 운영서버로 war파일만 옮겨 배포하는 경우등에 유용




# 4. Aritifact란?
- java 빌드 후 생성되는 것이 아티팩트(artifact)이다.
- artefact는 영국식 영어에서 주로 사용하는 스펠링이고, artifact는 미국식 영어에서 주로 사용하는 스펠링 방식이다
- (in Intelli J) artifact 의 output layout 속에 있는 available elements는 빌드시 사용되는 JAR 파일들이다.


---

1번 참고자료:
https://ko.wikipedia.org/wiki/%EC%95%A0%ED%94%8C%EB%A6%BF  


2번 참고자료 :  
https://coderanch.com/t/613561/java/Jar-Zip  
https://smiler.tistory.com/entry/JAR-파일이란 [아직은 내가 쓴 글보다 퍼온 글이 훨씬 많음]   
https://docs.oracle.com/javase/tutorial/deployment/jar/  

3번 참고자료 :  
https://dololak.tistory.com/31  
https://hashcode.co.kr/questions/778/%EC%9E%90%EB%B0%94%EC%97%90%EC%84%9C-war%EC%99%80-jar%EC%9D%98-%EC%B0%A8%EC%9D%B4%EA%B0%80-%EB%AD%94%EA%B0%80%EC%9A%94  

4번 참고자료 :  
http://a.zany.kr:9003/board/bView.asp?bCode=52299899&aCode=13729  
http://forensic-proof.com/archives/3710  
https://mirrortuttle.tistory.com/entry/What-is-Artifact [업계에서 사용되는 다양한 artifact의 의미를 알고 싶으면 이 url로 들어가야 한다]  
