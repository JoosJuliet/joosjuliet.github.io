---
layout: post
section-type: post
title: "왜 public과 private으로 subnet을 나누어야 할까요?"
category: AWS
tags: [ 'AWS' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)
---

# 이 글을 쓰는 이유
VPC 작업을 하려고 AWS문서를 보면 VPC를 설정하는 가장 대표적 4가지 시나리오 중 하나는 바로 private과 public subnet을 설정하는 것이 있습니다.   
그 중 왜 subnet을 private과 public과 나눠야 하는지에 대한 의문을 갖게 되어 이 글을 쓰게 되었습니다.  
public 과 private 으로 subnet을 나눈 이유는 *보안* 을 위해서 입니다.  
public subnet에는 outbound(+ 인터넷 연결)와 inbound call 전부 원하는대로 사용할 수 있습니다.  
즉 어떤 것을 하지 않으면 기본적으로 public subnet 입니다.

그에 반해 private subnet은 좀 다릅니다.
private subnet은 오로지 inbound call만 허용합니다.  

그렇다면 왜 subnet을 나눈다는 행위가 보안이 높아질까요?  
이건 *DMZ trust zone* 에 대해 알게 되면 알 수 있습니다.

# DMZ trust zone이란?
DMZ trust zone을 만드려면 세개의 구간으로 나누어야 한다.

- 내부망
- DMZ 구간
- 외부망

## 내부망
일정크기의 인터넷이 연결되어 있지 않으며 특정 네트워크안에서만 통신을 하는 근거리 통신망이다.  
예시 중 하나는 인트라넷이다.

## 외부망
인터넷도 연결할 수 있고 내가 연결되어 있는 내부망 끼리도 통신을 할 수 있습니다.
즉 외부망은 일반적으로 우리가 사용하는 것입니다.

## DMZ구간
DMZ(Demilitarized Zone)구간이란 외부에 서비스 제공 시, 내부 자원을 보호하기 위해 내부망과 외부망 사이에서 접근제한을 수행하는 gateway입니다.
public Internet으로 가기 전에 gateway를 하나 더 만드는 것이지요.

[DMZ 개념도]
![dmz-zone](/images/2020-04-18-private-public-subnet/dmz-zone.png)

- 내부망 : 물리적 망분리, 접근통제시스템 등에 의해 인터넷 구간에서의 직접적인 접근이 통제 또는 차단되는 구간
- DMZ구간 : 인터넷과 내부망과 인터넷 구간 사이에 위치한 중간지점으로 침입차단시스템 등으로 접근제한 등을 수행하지만 외부망에서 직접 접근이 가능한 영역
- 외부망 : 인터넷이 직접 연결되어 있는 구간

또한 외부망에서의 내부망은 원칙적으로 차단되어야 하는데,
접속이 필요한 경우에는 가상사설망(VPN, Virtual Private Network)등의 안전한 보호대책을 마련하여 접근할 수 있도록 해야 합니다.

# 그래서 aws 에서 dmz존은 어디로 갔고 public과 private subnet만 있을까?

일단 private subnet은 내부망과 거의 엇비슷하게 연결이 된다.  
그리고 public subnet은 다른 aws제품들을 활용해 외부망과 dmz zone을 구현한다.  

1. private subnet과 public subnet 둘 다 생성한 routing table 을 사용해서 연결을 한다.
2. public subnet에 internet gateway를 연결한다.  
  - public subnet에 속한 곳은 local network ip 이외의 대상은 internet gateway로 트래픽을 보낸다.

비록 외부에서 연결 가능한 DMZ이지만 NACL과 Security Group을 통해 접근 제어가 설정이 된다.
3. public subnet 안에 통신 게이트웨이인 NAT gateway를 만든다.
  - private subnet에서도 local network외의 ip는 모두 NAT gateway로 트래픽을 가게 한다.
  - 즉 private subnet에 속한 pc는 로컬 ip이외의 대상이 통신할 경우 무조건 NAT Gateway로 트래픽을 보낸다.
  - 즉 외부에서 private subnet에 직접 접근이 불가능하다.

*물리적 접근이 불가능함으로 망분리라고 한다*
![망분리](/images/2020-04-18-private-public-subnet/divide_network.png)
# 결론
private과 public으로 subnet을 나눈 이유는 보안을 위해 망분리를 위한 과정중 하나였던 것이다.  
원했던 보안은 직접적으로 돌고 있는 instance에 인터넷을 통해 함부로 접근하지 못하게 하기 위해서였다.


---
참고 : https://aws.amazon.com/ko/premiumsupport/knowledge-center/client-vpn-associate-target-network/
https://m.blog.naver.com/xcripts/70122248114
https://stackoverflow.com/questions/22188444/why-do-we-need-private-subnet-in-vpc
https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/VPC_Scenarios.html
https://blog.lael.be/post/9534
