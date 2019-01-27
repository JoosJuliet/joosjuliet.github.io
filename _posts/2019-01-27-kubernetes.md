---
layout: post
section-type: post
title: "쿠버네티즈란? 도커와의 관계는? 도커 와 쿠버네티즈의 차이? 도커와 쿠버네티즈를 비교? 쿠버네티즈 vs 도커 컴포즈?"
category: Algorithm
tags: [ 'kubernetes', 'docker', 'google', 'gcp' ]
comments: true
---


# 1. 글을 쓴 이유
2~3년 전 쿠버네티즈를 gcp에서 서비스를 내놓았을 때 대충 봤었는데,
그 이후에 죽 이직에 퇴직에(그 사이 두번이나 했다.) 알고리즘에 바빠서 까먹고 있었다.
그런데 그 사이 쿠버네티즈가 일명.. 이곳저곳에서 쓰는 서비스가 되버렸다(반응속도 시롸냐)
안쓴다 해도 개발 커뮤니티에서 자꾸 쿠버네티즈 글 올라와서...
지금 상황에서 대충이라도 정리를 일단 해놓고 나중에 퀄리티 있게 글을 써야겠다.


# 2. 글 시작


## 쿠버네티즈란?
일단 도커는 컨테이너를 만드는 것이다.
그런데 문제는 실 사용 서비스에 도입하면서 도커 컨테이너를 많이 만드는 상황이 왔다.(도커 오케스트레이션이 필요한 상황)
그러다 보니 도커를 관리하는 플랫폼이 필요하게 되었다.

그것에는 쿠버네티즈, 도커 스웜 등이 있었다.
대세(?)인 것 같은 착각이 드는 것 보니 쿠버네티즈가 1타 된 것 같다.(구글의 아이니까)

<span style="background-color:yellow"><b>쿠버네티즈는 container를 관리하는 플랫폼</b></span>


## 결국 쿠버네티즈와 도커는 무슨 관계..?

쿠버네티즈 안에서는 pod( a group of containers)이라는 존재가 있다.
즉 쿠버네티즈는 pod을 만들어서 container를 관리하는 플랫폼이고, docker의 대표(?) 서비스는 container다


약간의 혼돈의 카오스가 있었지만 결국

- docker -> container를 만드는 서비스
- kubernetes -> container(ex. docker)를 관리 해주는 서비스

<span style="background-color:yellow"><b>kubernetes는 도커가 아닌 다른 컨테이너 서비스 역시 관리가능하다!</b></span>
*내가 어디선가 듣기로는... docker와 비슷한 데 더 좋은 서비스를 구글에서 만들어서 쓰기때문에
내부적으로는 docker는 안쓴다 카더라....*


## 그럼 쿠버네티즈와 도커 컴포즈는 무슨 관계..?

<span style="background-color:yellow"><b>docker-compose는 내가 시작할 때 container를 선언해주는 것이다.</b></span>
node나, cluster개념은 없다.

그런데 <span style="background-color:yellow"><b> 둘다 configuration files (Yaml)을 만들수 있다.</b></span>
아마 이 이유 때문에 둘의 관계에 혼란이 오게 만들어 주는 것 같다.


- Docker Compose는 오케스트레이션없이 다중 컨테이너 Docker 응용 프로그램을 정의하고 실행하기위한 도구입니다.
- Kubernetes에는 pod이란 개념이 있는데 그것은 여러 컨테이너들을 가지고 있고, 사용 가능한 노드 사이의 분배 개념(클러스트링) 해준다.



## 여기서 잠깐 짚고 넘어가는 쿠버네티즈의 장점은

- 스케쥴링을 잘해줌
- 죽어도 스스로 잘 살려줌
- 확장성
- 로드 밸런싱
- 롤아웃/롤백이 자동으로 진행
- 설정을 관리


# 3. 그래서 내 생각에는

도커가 생길 당시 이곳저곳에서(구글 포함) 좋은 경량 컨테이너를 만들기 위해 노력했었다.
그러다가 도커팀에서 사용하기 쉬운 경량 컨테이너를 만들어서 도커라는 이름을 붙여서 마구 홍보를 했고, 다들 도커의 마력에 심취했다.

그러다가 gcp에 2~3년전 어느새 쿠버네티즈 서비스를 슬쩍 올려놨고 열심히 홍보를 했는데
다들 오... 하면서 새로운 마력에 심취 중인 것 같다.

작은 서비스에서는 딱히 필요없는 서비스 같다.


---
참고자료:
쿠버네티즈 장점
https://zzsza.github.io/development/2018/04/17/docker-kubernetes/

쿠버네티즈란?
https://www.youtube.com/watch?v=R-3dfURb2hA
