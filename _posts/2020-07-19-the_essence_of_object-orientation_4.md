---
layout: post
section-type: post
title: "객체지향의 사실과 오해 4단원 정리"
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
# 4. 역할, 책임, 협력
객체의 세계에서도 협력이라는 문맥이 객체의 행동 방식을 결정한다.  
우리는 객체들 사이에서 이뤄지는 협력의 품질을 높여 전체 품질을 높여야 한다.  
따라서 설계자는 협력에 초점을 맞춰 애플리케이션을 설계해야 한다.  
그렇게 하면 협력이 자리를 잡으면 저절로 개체의 행동이 나오고 뒤이어 적절한 객체의 상태가 결정되어서 조화를 이루며 상호작용하는 협력적인 객체들이 만들어진다.  




## 협력
협력은 다수의 요청과 응답으로 구성되며 전체적으로 협력은 다수의 연쇄적인 요청과 응답의 흐름으로 구성된다.  
그러므로 협력 안의 요청과 응답에 초점을 맞춰야 한다.  




## 책임
- 책임은 객체에 의해 정의되는 응집도 있는 행위의 집합
- 객체의 책임은 객체가 "무엇을 알고 있는가(knowing)"와 "무엇을 할 수 있는가(doing)"로 구성
  - doing
    - 객체를 생성하거나 계산을 하는 등의 스스로 하는 것
    - 다른 객체의 행동을 시작시키는 것
    - 다른 객체의 활동을 제어하고 조절하는 것
  - knowing
    - 개인적인 정보에 관해 아는 것
    - 관련된 객체에 관해 아는 것
    - 자신이 유도하거나 계산할 수 있는 것에 관해 아는 것
- 책임은 객체의 공용 인터페이스를 구성


### 책임과 메시지
객체가 다른 객체에게 주어진 책임을 수행하도록 요청을 보내는 것을 메시지 전송  
- 메시지
  - 협력에 참여하는 두 객체 사이의 관계를 강조  
  - 협력을 위해 한 객체가 다른 객체로 접근할 수 있는 유일한 방법




## 역할  
책임의 집합이 의미하는 것  


### 역할이 답이다.
역할을 사용하면 세가지 협력을 모두 포괄할 수 있는 하나의 협력으로 추상화할 수 있다.  
동일한 역할을 수행하는 객체들이 동일한 메시지를 수신할 수 있기 때문에 동일한 책임을 수행할 수 있다는 것은 중요하다.  
역할은 객체지향 설계의 단순성(simplicity), 유연성(flexibility), 재사용성(reusability)을 뒷받침하는 핵심 개념이다.  


### 협력의 추상화
구체적인 객체를 추상적인 역할로 대체함으로써 하나의 추상적인 협력으로 대체할 수 있다. 즉 역할을 이용하면 협력을 추상화함으로써 단순화 할 수 있다.  
이 때 주의할 점은 객체의 역할을 대체하기 위해서는 행동이 호환돼야 한다.  


### 객체의 모양을 결정하는 협력
객체지향 시스템에서 가장 중요한 것은 충분히 자율적인 동시에 충분히 협력적인 객체를 창조하는 것 이다.





## 객체지향 설계 기법
- 책임-주도 설계
  - 시스템의 책임을 객체의 책임으로 변환
  - 필요한 정보나 서비스를 제공해줄 협력자를 찾아 해당 협력자에게 책임을 할당하는 순차적인 방식으로 객체들의 협력 공동체를 구축
- 디자인 패턴
  - 책임 - 주도 설계는 개체의 역할, 책임, 협력을 고안하기 위한 방법과 절차를 제시한다면 디자인 패턴은 책임 - 주도 설계의 결과를 표현
  - 디자인 패턴은 공통으로 사용할 수 있는 역할,책임,협력의 템플릿
- 테스트 주도 개발
  - 실패하는 테스트 작성하고 통과하는 가장 간단한 코드를 작성 후 리팩토링을 통해 중복을 제거해 작동하는 깔끔한 코드를 얻는 것
  - 객체지향에 대한 깊이 있는 지식을 요구함으로 역할,책임, 협력에 집중하고 객체지향의 원칙을 적용하려는 깊이 있는 고민과 노력을 통해서만 혜택을 누릴 수 있다.
