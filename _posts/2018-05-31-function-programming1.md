---
layout: post
section-type: post
title: "함수형 프로그래밍이란?"
categories: Programming_Tech
tags: ['functional-programming' ]
comments: true
---

제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)


함수형 프로그래밍은 <span style="background-color:yellow"><b>선언적 프로그래밍 패러다임(declarative programming paradigm)</b></span>입니다.
함수형 프로그래밍은 function이 아닌 객체 또는 procedures 가 프로그램의 기본 구성 요소입니다.

# 이글을 쓴 이유

객체 지향과 함수형 프로그래밍을 대비하는 글이 많은데 그건 제 생각에는 잘못 된 견해 같습니다.
그래서 어떻게 잘못 된 지에 대한 저의 의식의 흐름을 글로 옮기고 싶어서 글을 썼습니다.

일단!
*실제로 함수형 프로그래밍의 대비 되는 것은 명령형 프로그래밍이고,
객체지향 프로그래밍과 대비 되는것은 절차 지향 프로그래밍입니다.*

# 함수형 프로그래밍이란?

상태값을 지니지 않는 함수값들의 연속

자료 처리를 수학적 함수의 계산으로 취급하고 상태와 가변 데이터를 멀리하는 프로그래밍 패러다임의 하나이다.


쉽게 말해 one-to-one Correspondence했으면 하는게 함수형 프로그래밍이다.
함수형 프로그램과 상반 대는 개념이 명령형 프로그래밍인데 같은 input값에도 다른 output값이 나오는 그런 프로그래밍 이다.

가장 쉽게 일어날 수 있는 법(?)은 함수 안에 random함수를 넣으면 일어난다.

여기에는 세가지 함수를 쓰는게 목표인데
1. 순수한 함수
즉, 함수의 실행이 외부에 영향을 끼치지 않는 함수를 뜻한다. 따라서 순수한 함수는 스레드 안전하고, 병렬적인 계산이 가능

2. 익명 함수
3. 고계 함수

함수를 다루는 함수를 뜻한다. 사실 함수형 언어에서는 함수도 '값(value)'으로 취급
Map, filter,reduce 같은 것


함수형 프로그래밍은 자료 처리를 수학적 함수의 계산으로 취급하고 상태와 가변적인 데이터를 배제하는 프로그래밍 기법

---

참고자료 :
https://medium.com/@gertienyesh/functional-programming-and-function-chaining-in-javascript-76628d3cf1f5
