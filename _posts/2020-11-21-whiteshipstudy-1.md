---
layout: post
section-type: post
title: "1주차 과제: JVM은 무엇이며 자바 코드는 어떻게 실행하는 것인가."
category: Java
tags: [ 'Java', 'whiteship' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)  
---  
# 목표
자바 소스 파일(.java)을 JVM으로 실행하는 과정 이해하기.

# index
JVM이란 무엇인가
컴파일 하는 방법
실행하는 방법
바이트코드란 무엇인가
JIT 컴파일러란 무엇이며 어떻게 동작하는지
JVM 구성 요소
JDK와 JRE의 차이


## JVM이란 무엇인가
- 컴파일된 자바 바이트코드를 받아서 OS가 이해할 수 있는 실행코드로 바꾸어주는 역할
- 언어의 플랫폼 종속적인 특징의 단점을 극복할 수 있는것이 JVM
- 그러나 JVM이 플랫폼 종속적
- JVM 홀로 제공되지 않고 최소한의 배포단위가 JRE다. (JRE에는 JVM + library)




## 컴파일 하는 방법
- .java (소스파일) -> .class[in java.exe(자바 컴파일러)]
자바는 바로 기계어로 바꾸는 것이 아니라 바이트코드로 이루어진 클래스 파일(.class)을 생성을 하고 그것을  JVM이 실행해 어디서든 프로그램이 돌아갈 수 있다.

한번 작성하면 어디서든 프로그램이 돌아간다는 장점이 생기는 것이다.
*참고*
- java 14버전으로 컴파일한 파일을 java 8버전으로 실행하게되면 어떻게 될까?
-> 안된다. 하지만, 하위버전의 클래스파일은 상위버전에서 실행할 수 있다.
하지만 이 문제는 컴파일 시 target 옵션을 줘서 호환되게 할 수 있다.




## 실행하는 방법

- java <options> <classfile> <argument>
- java <options> -jar <file>.jar <argument>




## 바이트코드란 무엇인가

- JVM이 이해할 수 있는 언어로 변환된 코드.
- 자바 컴파일러에 의해 변환되는 코드의 명령어 크기가 1바이트라서 '바이트코드'라고 불린다.
- JVM만 설치되어 있으면 어떠한 운영체제에서라도 실행할 수 있다.




## JIT 컴파일러란 무엇이며 어떻게 동작하는지
- JUST-IN-TIME, 제시간에 컴파일한다.
- jvm은 바이트 코드를 인터프리터 방식으로 실행
- 즉 한줄씩 수행시키는데 그로 인해 실행이 느려 보완된 것이 JIT 컴파일러
- 반복되는 코드를 인터프리터가 해석할 필요가 없이(=캐싱해서) 기계어로 바로 실행할 수 있도록 한다.
- JIT도 일종의 스레드로 동작하고, JIT과 인터프리터는 동시에 실행하고, JVM의 런타임영역에 들어가 있다. JAVA 2,3 부터 포함되어 들어가있다.


# JVM 구성 요소
![jvm](/images/2020-11-21-whiteshipstudy-1/jvm.png)
출처 : https://sjh836.tistory.com/64


# JDK와 JRE의 차이

- JDK : java development kit - 자바 개발도구,
JRE : java runtime environment - 자바 실행환경

*참고*
JAVA 11에서부터는 JRE를 더이상 안 만들어 필요없다.
오라클에서 JDK 1.8 이후로 유료화로 인해 JAVA 개발업체들이 OracleJDK에서 OpenJDK로 전향



----
참고 url
https://www.notion.so/WEEK1-60b72f243541430d9700591aa3a0094b  
