---
layout: post
section-type: post
title: "Naive_Bayes_Classification"
category: machine_learning
tags: [ 'machine_learning', '글또1기', 'Naive_Bayes_Classification' ]
comments: true
---

# 1. 글을 쓴 이유
친구의 데이터마이닝 수업의 기말고사를 도와주는 도중 나이브 베이즈 분류를 자세히 설명해야할 상황이 와서 설명하다가 글을 쓰게 되었다.

# 2. 내용
## 나이브 베이즈 분류를 하기전에 선행지식

### 조건부 확률(conditional probability)
어떤상황이 주어졌을 때 다른 상황이 일어날 확률
조건부 경우
1.서로 영향을 끼칠 때-0
비가오는날에 우산이 잘팔린다.

2.서로 영향을 끼치지 않을 때
초록색옷을 입었을 때 잭팟이 터진다.

### 베이즈 정리
>무언가를 결정하는데 필요한 변수들이 각자 독립된 환경에서 이루어진다.


## 나이브 베이즈
나이브 베이즈는 이전에 일어났던 일의 확률과 유사성을 토대로 이후에  일어날 확률들을 알아내는 조건부 확률모델이다.

>P(Ci|X)=      P(X|Ci)P(Ci)
>                 P(X)

카테고리 종류 Ci에 속한 tuple =(x1,x2…xn)이 있다. 그 tuple은 n개의 각각의 독립된 특성을 가진 X이다.
그 카테고리 종류에 연관된 독립된 특성을 가지고 사후확률P (Ci | X)을 최대화하는 classification이 나이브 베이즈 분류이다.


이를 좀 더 쉽게 보여준 것은
>posterior = prior * likelihood
>                evidence
(posterior : 사후 확률, prior : 사전확률, likelihood : 우도, evidence : 관찰값)


>P(A|B) = P(A)P(B|A)
>          P(B)

P(A|B) : posterior, 사건 B로 인하여 A가 일어날 확률
P(A): prior, 사건 B를 알기 전의 확률
P(B|A): likelihood, 사건 A로 인하여 B가 일어날 확률
P(B): evidence:증거



# 나이브 베이즈 분류 장점
 첫째, 일부의 확률 모델에서 나이브 베이즈 분류는 지도학습 (Supervised Learning) 환경에서 매우 효율적으로 훈련 될 수 있다.
 둘째, 분류에 필요한 파라미터를 추정하기 위한 트레이닝 데이터의 양이 매우 적다는 것이다.
 셋째, 간단한 디자인과 단순한 가정에도 불구하고, 나이브 베이즈 분류는 많은 복잡한 실제 상황에서 잘 작동한다.

# 나이브 베이즈 분류 한계

조건이 각 속성들간이 독립적 관계라고 하는데 생각보다 그렇게까지 독립적인 것이 없다.

참고자료

https://www.youtube.com/watch?v=qPfygGvc2Rc
https://ko.wikipedia.org/wiki/%EB%82%98%EC%9D%B4%EB%B8%8C_%EB%B2%A0%EC%9D%B4%EC%A6%88_%EB%B6%84%EB%A5%98
https://stats.stackexchange.com/questions/183056/what-does-it-mean-disadvantage-of-naive-bayes-classifier-strong-feature-indepe
