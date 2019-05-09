---
layout: post
section-type: post
title: "[MSA] 장애전파를 막는 circuit breaker, Fall-back messaging"
category: Algorithm
tags: [ 'msa', 'circuit_breaker', 'Fall-back_messaging' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

# MSA의 장점
한 서비스는 다른 서비스에 영향을 안 끼친다.


# MSA에서 일어나는 장애전파의 문제점
그렇지만 다른 서비스에 디펜던시가 있는 서비스들은 영향을 끼친다.  
즉 MSA에서 서비스간 장애가 전파될 때가 있다.  
마이크로 서비스 아키텍쳐 패턴은 시스템을 여러개의 서비스 컴포넌트로 나눠서 서비스 컴포넌트간에 호출하는 개념을 가지고 있다  
이로 인해 생긱는 문제점은  
- 하나의 컴포넌트가 느려지거나 장애가 나면 그 <span style="background-color:yellow"><b>장애가 난 컴포넌트를 호출하는 종속된 컴포넌트까지 장애가 전파</b></span>된다.




## 장애 상황의 예시


### 과도한 트래픽에 의한 장애 가정
- 서비스는 감당할 수 있는 Request의 수를 정해놓고 그 이상의 Request가 오게 되면 큐에 쌓이게 되고 순차적으로 처리가 됩니다. (tomcat의 max-thread)
- 현재 서비스B 는 과도한 트래픽으로 인해 큐에 많은 수의 Request가 쌓여있는 상태
- 서비스A는 서비스B를 호출하게 되면 큐가 다 비워질 때까지 기다려야 된다.
- 하지만 우리는 이것을 대비하여 timeout을 설정
- 그래서 책 서비스가 개인화 서비스를 호출했을 때, 설정한 timeout을 넘어가게 되면 에러를 발생시켜 무작정 기다리는 것을 방지하지만 timeout 만큼 기다려야 합니다.



### 서비스 B에 장애 가정
<img alt="success" src = "/images/2019-05-09-circuit-breaker/problem.png"/>

- Service A가 Service B를 호출을 하는데, 문제가 발생해 Service B가 응답을 못준다.
- Service A에서 Service B를 호출한 쓰레드는 응답을 받지 못했기에, 계속 응답을 기다리는 상태로 잡혀있다.
- 지속해서 Service A가 Service B를 호출을 하게 되면 앞과 같은 원리로 각 쓰레드들이 응답을 기다리는 상태로 변한다.
- 결과적으로는 남은 쓰레드가 없어 다른 요청을 처리할 수 없는 상태가 된다.





# 장애 전파에 대한 해결책
그것이 바로 <span style="background-color:yellow"><b>circuit breaker</b></span>

## 기본적인 원리
<img alt="success" src = "/images/2019-05-09-circuit-breaker/solution1.png"/>

- Service A와 Service B에 Circuit Breaker를 설치한다.
- Service B로의 모든 호출은 이 Circuit Breaker를 통하게 되고 Service B가 정상적인 상황에서는 트래픽을 문제 없이 bypass 한다.
- 만약에 Service B가 문제가 생겼음을 Circuit breaker가 감지한 경우에는 Service B로의 호출을 강제적으로 끊어서 Service A에서 쓰레드들이 더 이상 요청을 기다리지 않도록 해서 장애가 전파하는 것을 방지 한다.
- 강제적으로 호출을 끊으면 에러 메세지가 Service A에서 발생하기 때문에 장애 전파는 막을 수 있지만, Service A에서 이에 대한 장애 처리 로직이 별도로 필요하다.




## Fall-back 메시징
- circuit breaker를 더 발전 시킨것이 <span style="background-color:yellow"><b> Fall-back messaging </b></span>
- Circuit breaker에서 Service B가 정상적인 응답을 할 수 없을 때, <span style="background-color:yellow"><b> Circuit breaker가 룰에 따라서 다른 메세지를 리턴하게 하는 방법 </b></span>
- 대표적으로는 Default 값을 설정
- 그렇게 되면 마비가 일어나도, 에러 없이 자연스러운 연출
- 또한 timeout만큼 기다리지 않아도 된다.



## Fall-back messaging 예제
<img alt="success" src = "/images/2019-05-09-circuit-breaker/solution2.png"/>

- Service A는 상품 목록을 화면에 뿌려주는 서비스이다.
- Service B는 사용자에 대해서 머신러닝을 이용하여 상품을 추천해주는 서비스이다. 그리고 Service B가 장애가 나면 상품 추천을 해줄 수 없다.
- 이때 상품 진열자 (MD)등이 미리 추천 상품 목록을 설정해놓고, Service B가 장애가 났다.
- Circuit breaker에서 이 목록을 리턴해주게 하면 머신러닝 알고리즘 기반의 상품 추천보다는 정확도는 낮아지지만 최소한 시스템이 장애가 나는 것을 방지 할 수 있고 다소 낮은 확률로라도 상품을 추천하여 꾸준하게 구매를 유도할 수 있다.




# 구현체
- Fall-back messaging은 넷플릭스에서 자바 라이브러리인 Hystrix로 구현이 되었있다.
- 이렇게 소프트웨어 프레임웍 차원에서 적용할 수 있는 방법도 있지만 인프라 차원에서 Circuit breaker를 적용하는 방법도 있는데, envoy.io 라는 프록시 서버를 이용하면 된다.
- 소프트웨어를 사용하는 경우 관리 포인트가 줄어드는 장점은 있지만, 코드를 수정해야 하는 단점이 있고, 프로그래밍 언어에 따른 종속성이 있다.
- 반대로 인프라적인 접근의 경우에는 코드 변경은 필요 없으나, Circuit breaker용 프록시를 관리해야하는 추가적인 운영 부담이 늘어나게 된다.






---
출처: https://bcho.tistory.com/1247?category=431297 [조대협의 블로그]  
https://alwayspr.tistory.com/26  
https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=113808876  
