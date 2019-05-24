---
layout: post
section-type: post
title: " Annotation이란? Reflection이란? @Component? @Repository? @Service? @Controller?"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---
# 1. Reflection이란?
스프링에선 리플렉션을 너무 많이 사용중이라고 한다.
근데 처음 들어봤다.

Reflection이란 프로그램이 실행 중에 자신의 구조와 동작을 검사하고, 조사하고, 수정하는 것입니다.

객체 지향 프로그래밍 언어에서 reflection을 사용하면 컴파일 타임에 interface, field, method의 이름을 알지 못해도, 실행 중에 각 요소에 접근할 수 있다.
또한 새로운 객체의 인스턴스화 및 메소드 호출을 허용합니다.
이 말은 밑에 일단 아직 컴파일이 완료되지 않아서, 객체화가 되지도 않은 class의 인스턴스를 만들어준다는건가? 의 뜻인가?


## 스프링에서 Reflection 활용기1.
스프링에서 BeanFactory 라는 Container를 공부할 때 객체가 호출되면 객체의 인스턴스를 생성하게 되는데, 이 때 필요하다.  
일단 아직 컴파일이 완료되지 않아서, 객체화가 되지도 않은 class의 인스턴스를 만들어준다는건가?
<b> 즉 프레임워크에서 유연성 있는 동작을 위해 쓴다. </b>


## 스프링에서 Reflection 활용기2.

리플랙션은 annotation 지정만으로 원하는 클래스를 주입하는데,
클래스 주입은 enum을 사용해서 한다?
enum은 변수를 선언시 변수타입으로 사용가능하다.를선언

### 사용법
``` Java
enum Season

Unknown macro: {winter, spring, summer, fall}
// 변수 time은 가질 수 있는 값이 제한되어 Season의 값 4개 중 하나만 가질 수 있다. 값 4질
Season time = Season.spring;
```


기본적으로 private이어서, new 로 새로운 인스턴스를 만들 수 없다.
https://jojoldu.tistory.com/122
여기서 enum을 사용한 프로젝트가 있다.(후에 프로젝트에 도입 해야지)


annotation 자체는 아무런 동작을 가지지 않는 단순한 표식일 뿐이지만,  
리플렉션을 사용하면 어노테이션의 적용 여부와 엘리먼트 값을 읽고 처리할 수 있다.




# 2. Annotation이란?
# 의미
- 사전적 의미는 주석이지만 java에서는 메타 데이터의 일종
- annotation이 붙은 코드는 annotation의 구현된 정보에 따라 연결되는 방향이 결정


## 용도
- 컴파일러에게 코드의 문법을 체크하도록 정보 제공
- 코드를 자동생성할 수 있또록 정보 제공
- 실행시 특정 기능등을 실행하도록 정보 제공
- 클래스의 역할을 정의하는 것
- 동작

Annotation은 컴파일러에 의해 생성되는 .class파일에 포함되며 그 .class 파일을 통해 읽혀집니다.  
JVM 실행 시, annotation은 보관되며 reflection을 통해 자세히 읽을 수 있습니다.


## Built-in annotation

- @Override
  - 메소드가 Override되어있는지 확인
- @Deprecated, @SuppressWarnings 등이 있다.


## Annotation
annotation 에 사용되는 annotation
- @Inherited
  - annotation이 달린 class의 하위 class에 상속될 annotation을 표시합니다.
  - 기본적으로 annotation은 하위클래스에 상속되지 않습니다.







┌────────────┬─────────────────────────────────────────────────────┐
│ Annotation │ Meaning                                             │
├────────────┼─────────────────────────────────────────────────────┤
│ @Component │ generic stereotype for any Spring-managed component │
│ @Repository│ stereotype for persistence layer                    │
│ @Service   │ stereotype for service layer                        │
│ @Controller│ stereotype for presentation layer (spring-mvc)      │
└────────────┴─────────────────────────────────────────────────────┘


---
참고자료:

1. Reflection이란? 참고자료:
 https://qssdev.tistory.com/27



2. Annotation 좋은 글이자 참고자료:
http://www.nextree.co.kr/p5864/
