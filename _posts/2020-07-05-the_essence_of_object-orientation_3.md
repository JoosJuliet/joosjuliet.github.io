---
layout: post
section-type: post
title: "객체지향의 사실과 오해 3단원 정리"
category: Object
tags: [ '북리뷰' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)  
---  

http://www.yes24.com/Product/Goods/18249021?Acode=101  
위 책의 내용을 요약, 이해하기 쉽게 정리한 포스트 입니다.  
---  

# 3. 타입과 추상화

추상화란 "정확성"을 버리고 "목적"에 집중하는 것이다.  
그러므로 훌륭한 추상화는 얼마나 정확한지가 아니라 원하는 목적에 얼마나 집중했는지 여부이다.  


## 객체지향과 추상화
객체지향 패러다임에서 "객체"란 명확한 경계를 가지고 구별할 수 있는 사람이나 사물이다.  
구별을 하기 위해서는 기준이 필요하다. 그 기준은 바로 공통점이며, 공통점을 기반으로 각각을 묶는다.  
그로 인해 각각의 원소들은 묶여서 집합을 이루게 되는데 그 집합들은 "개념"이 된다.  
그리고 각각의 개념들로 인해 그들은 "분류"가 된다.  




### 개념이란?
개념에는 세가지 관점이 있다.  
- 심볼: 개념을 가리키는 간략한 이름이나 명칭
- 내연: 개념의 의미, 개념을 객체에게 적용할 수 있는지 여부를 판단하기 위한 조건
- 외연: 개념에 속하는 객체들  
개념을 이용해 공통점을 가진 객체들을 분류할 수 있다는 아이디어는 객체지향 패러다임이 복잡성을 극복하는 데 사용하는 가장 기본적인 인지 수단이다.


### 분류란?
분류란 객체에 특정한 개념을 적용하는 작업이며 추상화를 위한 도구이다.  




## 타입
타입에 관련된 두가지 중요한 사실이 있다.  
1. 타입은 데이터가 어떻게 사용되는지 알려준다.  
  - 즉 타입은 데이터가 어떤 타입에 속하는지를 결정하는 것  
2. 타입에 속한 데이터를 메모리에 어떻게 표현하는지는 외부로부터 철저하게 감춰진다.  




## 객체와 타입
객체를 타입에 따라 분류하고 이름을 붙이는 것은 결국 프로그램에서 사용할 새로운 데이터 타입을 선언하는 것이다.  
각각의 객체를 정의하는 것은 행동을 토대로 한다. 결국 분류의 기준은 객체의 행동이다.  

즉 데이터 타입에 관해 언급했던 두 가지 조언은 객체와 타입을 이야기할 때 적용된다.  
1. 어떤 객체가 어떤 타입에 속하는지를 결정하는 것은 객체가 수행하는 행동
2. 객체의 내부적인 표현은 외부로부터철저하게 감춰진다.

동일한 책임을 수행하는 일련의 객체는 동일한 타입에 속한다고 말할 수 있다.  
즉 객체의 타입을 결정하는 것은 객체의 행동뿐이다.  
행동에 따라 객체를 분류하기 위해서는 객체가 외부에서 제공해야 하는 행동을 먼저 생각해 책임-주도 설계를 해야한다.  

*참고: 책임-주도설계*  
데이터-주도 설계의 단점을 개선하기 위해 고안  
객체를 결정하는 것은 행동이다. 데이터는 단지 행동을 따르는 것이다.  




## 타입의 계층
- 일반화/특수화 관계  
일반화/특수화 관계를 결정하는 것은 객체의 상태표현하는 데이터가 아니라 행동이다.  
일반화는 추상화를 위한 도구이다. 특수하다는 것은 일반적인 개념보다 범위가 더 좁다는 것을 의미한다.  
- 일반화/특수화를 결정하는 요인은 상태를 표현하는 데이터가 아니라 행동
  - 즉 내부에 보관한 데이터가 아니라, 외부로 노출된 행동
  - 일반적인 타입: 적은 수의 행동
  - 특수한 타입: 일반적인 타입에 비해 많은 행동을 가지며, 일반적인 타입이 하는 모든 행동을 동일하게 수행


- 동적 모델과 정적 모델
객체지향 애플리케이션을 설계하고 구현하기 위해서는 동적, 정적 모델을 적절히 혼용한다.  
동적모델: 객체의 스냅샷  
정적모델: 객체가 가질 수 있는 모든 상태와 모든 행동을 시간에 독립적으로 표현하는 것  




## 그래서 결국 클래스란?
타입은 객체를 분류하기 위해 사용하는 개념이다. 반면 클래스는 단지 타입을 구현할 수 있는 여러 구현 매커니즘 중 하나이다.  

가장 중요한 것은 동적으로 변하는 객체의 상태와 상태를 변경하는 행위이다. 클래스는 타입을 구현하기 위해 프로그래밍 언어에서 제공하는 구현 메커니즘이다.   

---  
참고자료:  
https://velog.io/@pandahun/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5%EC%9D%98-%EC%82%AC%EC%8B%A4%EA%B3%BC-%EC%98%A4%ED%95%B43%EC%9E%A5  
