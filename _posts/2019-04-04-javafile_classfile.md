---
layout: post
section-type: post
title: "[legacy 환경설정으로 얻은 지식들] java를 컴파일 하기 위해서 변하는 파일포맷들, class파일이란, 컴파일러란?, JVM이란?"
category: Spring
tags: [ 'Spring', '환경설정', 'SKencar' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

Java의 실행과정

Hello.java ----- Compiler ----- Hello.class ----- JVM ----- Hello



# Compiler란?
프로그래밍 언어로 작성된 프로그램을 기계어로 변환하는 소프트웨어


## 특징
- .java파일에 오류가 있는지 검사
- 특정 컴퓨터를 위한 코드를 생성하는 것이 아니라 JVM을 위한 코드(bytecode)를 생성


# .class파일이란?
source code 파일(.java)을 byte code로 바꾼 파일이다.
배포할 때에는 실행파일인 바이트코드 파일, 즉 class파일만 배포한다.

특징은 JVM (Java Virtual Machine 자바 가상 머신)을 위한 코드입니다.
그리하여 자바를 실행할 수 있는 모든 장치에서 실행이 가능합니다.


## 어디에 저장되나?
컴파일 할 때 옵션을 줘서 어느 폴더에 저장될지 지정해준다.

대부분은 자바 파일은 src 이름으로 class file은 binary의 약자 bin 이라는 폴더에 넣는다.

``` shell
javac -d bin src/file_name.java
```
이렇게 하면 bin이라는 폴더 속에 java 파일을 컴파일한 클래스 파일이 생성된다.


# JVM이란?
- 자바의 바이트코드를 해당 컴퓨터의 명령어로 해석해주는 프로그램




---
참고:
출처: https://droptable.tistory.com/42 [DropTable]

https://wanzargen.tistory.com/12
