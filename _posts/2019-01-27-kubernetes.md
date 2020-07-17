---
layout: post
section-type: post
title: "쿠버네티스란? 도커와의 관계는? 도커 와 쿠버네티스의 차이? 도커와 쿠버네티스를 비교? 쿠버네티스 vs 도커 컴포즈?"
category: cloud
tags: [ 'kubernetes', 'docker', 'google', 'gcp' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)
---
# 글을 쓴 이유
빠르게 인기를 끌고 있는 쿠버네티스는 아직 실무에서 한번도 써본 적은 없지만 그래도 다시 한번 글을 다듬어 보려고 한다.
대충이라도 계속 정리를 업데이트를 한다면 나중에 퀄리티 있는 글을 쓰는데 도움이 될 것 같다.




# 요약
도커는 '이미지를 만들고 컨테이너에 띄우는 도구'이고 쿠버네티스는 '도커를 관리하는 툴'이다.


## 쿠버네티스의 탄생설화?
1. 도커라는 쉽게 컨테이너를 만드는 서비스가 탄생을 하였다.
2. 도커는 낮은 진입장벽으로 큰 인기를 얻게 되었고, 그로 인해 상용서비스에도 많이 도입되었다.
3. 그런데 문제는 도커 컨테이너를 많이 만드는데 관리가 쉽지 않은 상황이 왔다.  
4. 그러다 보니 도커를 관리하는 플랫폼이 필요하게 되었다.


## 쿠버네티스
도커 컨테이너를 관리 하는 것을 도커 오케스트레이션이라고 한다.  
그런 작업을 하는 것은 쿠버네티스, 도커 스웜, ecs 등이 있었다.  

<span style="background-color:yellow"><b>즉 쿠버네티스는 container를 관리하는 플랫폼</b></span>


## 결국 쿠버네티스와 도커는 무슨 관계..?

쿠버네티스 안에서는 pod( a group of containers)이라는 존재가 있다.
즉 쿠버네티스는 pod을 만들어서 container를 관리하는 플랫폼이고, docker의 대표(?) 서비스는 container다


약간의 혼돈의 카오스가 있었지만 결국

- docker -> container를 만드는 서비스
- kubernetes -> container(ex. docker)를 관리 해주는 서비스

<span style="background-color:yellow"><b>kubernetes는 도커가 아닌 다른 컨테이너 서비스 역시 관리가능하다!</b></span>
*내가 어디선가 듣기로는... docker와 비슷한 데 더 좋은 서비스를 구글에서 만들어서 쓰기때문에
내부적으로는 docker는 안쓴다 카더라....*


## 그럼 쿠버네티스와 도커 컴포즈는 무슨 관계..?

<span style="background-color:yellow"><b>docker-compose는 내가 시작할 때 container를 선언해주는 것이다.</b></span>
node나, cluster개념은 없다.

그런데 <span style="background-color:yellow"><b> 둘다 configuration files (Yaml)을 만들수 있다.</b></span>
아마 이 이유 때문에 둘의 관계에 혼란이 오게 만들어 주는 것 같다.


- Docker Compose는 오케스트레이션없이 다중 컨테이너 Docker 응용 프로그램을 정의하고 실행하기위한 도구입니다.
- Kubernetes에는 pod이란 개념이 있는데 그것은 여러 컨테이너들을 가지고 있고, 사용 가능한 노드 사이의 분배 개념(클러스트링) 해준다.



## 여기서 잠깐 짚고 넘어가는 쿠버네티스의 장점은

- 스케쥴링을 잘해줌
- 죽어도 스스로 잘 살려줌
- 확장성
- 로드 밸런싱
- 롤아웃/롤백이 자동으로 진행
- 설정을 관리




작은 서비스에서는 의미가 없을 가능성이 높다고 해서 쓰지 않고 있는데 써보고 싶긴 하다.
  



---
참고자료:
쿠버네티스 장점
https://zzsza.github.io/development/2018/04/17/docker-kubernetes/

쿠버네티스란?
https://www.youtube.com/watch?v=R-3dfURb2hA  
https://conservative-vector.tistory.com/entry/쿠버네티스와-도커의-차이 [에움길]
