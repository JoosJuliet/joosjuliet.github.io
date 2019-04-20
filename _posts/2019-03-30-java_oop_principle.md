---
layout: post
section-type: post
title: "[java_oop_principle] Java에서 OOP컨셉 및 원리는 무엇이 있는가?(feat. 추상화, 다형성, 캡슐화, 상속란?) "
category: Algorithm
tags: [ 'object_oriented_programming', 'OOP', 'Java' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

---
# Java에는 OOP 원리가 4가지 있습니다.
- Abstraction(추상화)
- Encapsulation(캡슐화)
- Inheritance(상속)
- Polymorphism(다형성)  

이중에서 상속은 점점 안티패턴 취급을 받으며 composition을 사용하는 것이 권장되지만! 일단은 원리입니다!  

관련 설명이 나와있는 url - https://joosjuliet.github.io/java_composition/


# Abstraction(추상화)란?
- 구체적 사물들의 공통된 특징을 파악하여 인식할 수 있는 대상으로 심는 행위
- abstract 구현동화 예)
  - 노트북, 가방, 핸드폰 모두 하나의 객체가 있다.
  - 이 수많은 객체 사이에 공통된 특징을 뽑아내 하나의 집합으로 만들고 싶다.
  - 그 예로는 아이패드, 갤탭

  - 두가지에는 공통된 특징
    - 속성(변수)
      - 디스플레이
      - 카메라
      - 스피커
    - 기능
      - 전원 킨다.
      - 전원 끈다.

  - 공통된 특징을 찾아내 class를 설계하는 것 -> 추상화

## 추상화의 코드화

``` java

public class Tablet {
  private String display;
  private String frontCamera;
  private String backCamera;
  private String speaker;

  public void turnOn(){
    System.out.println("boot on!");
  }

  public void turnOff(){
    System.out.println("shutdown!");
  }
}
```
이렇게 만들 수 있다.

``` java

public class Test{
  public static void main(String[] args){
    Tablet iPad = new Tablet();
    Tablet galaxyTab = new Tablet();

    iPad.turnOn();
    galaxyTab.turnOff();
  }
}
```

다른 물건이지만 공통된 특징과 공통된 기능을 찾아내 태블릿이라는 범주로 묶는 것
## 추상화 정리

- 추상화란 : 특정한 사물들의 공통된 특징을 파악하고 정의하는 행위
- 기대효과 : 프로그래머가 유용하고 재사용 가능한 도구를 만들 수있게 해줍니다.


# Encapsulation(캡슐화)란?

## 캡슐화는 왜 필요할까?
- 항상 요구사항은 변경된다.
- 따라서 요구사항의 변경을 당연하게 받아들이고 이에 대처하는 법을 터득해야 한다.

## 캡슐화는 뭘하면 이루어지나?
- 캡슐화는 정보은닉(알 필요가 없는 정보는 외부에서 접근하지 못하도록 제한)을 하는 것이다.
- ex) 스마트폰을 충전하는 방식은 알더라도 내부에서 어떻게 충전되는 지 알 필요가 없다.

### 정보은닉을 무슨 방법으로 하는게 좋을까?
- 높은 응집도와 낮은 결합도를 갖는다.
- 이를 대처하는 방법이 낮은 결합도와 높은 응집도를 유지하는 것이다





---
참고: https://m.blog.naver.com/PostView.nhn?blogId=gray2ajar&logNo=220239878444&proxyReferer=https%3A%2F%2Fwww.google.com%2F
