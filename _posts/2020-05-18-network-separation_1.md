---
layout: post
section-type: post
title: "RDS와 EC2의 VPC를 분리해서 네트워크를 구성 하는 이유 (feat. VPC Peering, Client VPN)"
category: AWS
tags: [ 'AWS' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)
---  

# 궁금하게 된 이유
RDS의 사용법에 관련된 AWS의 시나리오가 있었는데 그 중 하나가 RDS와 EC2를 분리해 놓은 것도 있었고 우리 회사도 그런식으로 만들어져 있었다. 이유를 찾기 위해 열심히 구글링을 했으나 제대로된 이유는 찾지 못했었다.  
그러다 모든 망분리는 보안을 위한 것이고, AWS를 사용하기 전에는 어떻게 DB를 다뤘는지에 관한 자료들을 찾아보던 중 힌트를 알게 되었다.  




# 보안이슈
과거에는 금융업쪽에서도 망을 분리하는 것이 필수적이지 않았던 시절도 있었다.  
우리나라에서는 2013년의 큰 쇼핑몰회사가 고객정보를 해커에게 털렸고,  
주요원인은 "논리적 망분리 허술과 DB서버에 대한 접근통제실패"로 지목되었었다.  

망분리에 관련된 금융업쪽의 법규와 ISMS 같은 보안인증을 받기 위한 사항들이 차곡차곡 생겼는데 그 중 하나가 고객의 개인정보가 든 DB서버의 경우 망을 분리 해야한다는 것이었습니다.  

![서버구조](/images/2020-04-18-database-network-separation/server-architect.png)

이런식으로 되어있었다.  
그래서 database 서버는 인터넷을 사용할 수 없는 업무망 속에 넣어놨었다.  




# 사용법
그것을 사용하는 방법은 여러가지가 있는데 지금 우리나라에서 가장 많이 들어 본(?) 것은    

## 컴퓨터를 분리해서 망 접속
![컴퓨터 분리](/images/2020-04-18-database-network-separation/divide-computer.png)

~정말 화끈하지 않은가~
## 컴퓨터에 vdi를 깔아 vdi를 통해서만 인터넷을 이용
![vdi](/images/2020-04-18-database-network-separation/vdi.png)

~근데 vdi가 너무 느리고 무겁다~




# aws에서는 어떻게 저 개념을 가져올 수 있을까?
![망분리](/images/2020-04-18-database-network-separation/ec2-rds.png)

데이베이스는 기본적으로 Web 애플리케이션 서버를 경유하여 접속을 하게 되는데,  
Web 애플리케이션에는 데이터베이스 서버에 대한 접속 정보가 저장되어 있다.  
즉 Web 애플리케이션 서버가 외부의 침입으로 해킹되면 데이터베이스에도 피해가 간다.  

그래서 db를 연결하는 ec2와 db를 각각 private 에 넣어 인터넷 연결을 끊어버리는 것이다.




# 근데 그렇게 다 망분리해 놓고 인터넷까지 끊어버리면... db는 어떻게 가져올까?
과거에는 무려 usb로 이동을 시켰다고 한다...  
그러다가 차츰 업무망과 인터넷망 구간의 자료이동을 위한 파일 전송 방법을 지원해 안정성과 보안성이 강화된 망간 자료전송 체계를 구축하는 스트리머 기계등을 사용하게 된다.




# 그러면 aws에서는...
1. VPC Peering
private IP 주소를 사용하여 두개의 VPC간에 트래픽을 라우팅할 수 있도록 하기 위한 VPC 네트워킹 연결하는 서비스 이다.


*번외*
# VPC peering vs client vpn
이란 검색어도 있는데  

AWS Client VPN은  
AWS 리소스와 온프레미스 네트워크 리소스를 안전하게 액세스할 수 있게 해주는 관리형 클라이언트 기반 VPN 서비스입니다. 클라이언트 VPN에서는 OpenVPN 기반 VPN 클라이언트를 사용하여 어떤 위치에서든 리소스에 액세스할 수 있습니다.


open vpn은  
라우팅 구성이나 브리지 구성, 원격 접근 기능을 통해 안전한 점대점 또는 사이트 대 사이트 연결  
가상 사설망 기술을 구현하는 응용 소프트웨어  

![client-vpn](/images/2020-04-18-database-network-separation/vpn.png)

즉 이렇게 생긴 vpc에 연결을 하기 위한
node를  만들고 해당 node에 접속하는 것이다.


---



망분리url:
https://www.boannews.com/media/view.asp?idx=31388  

http://www.igloosec.co.kr/BLOG_%EC%9D%B8%ED%84%B0%ED%8C%8C%ED%81%AC%20%EA%B0%9C%EC%9D%B8%EC%A0%95%EB%B3%B4%20%EC%9C%A0%EC%B6%9C%EC%82%AC%EA%B3%A0%EB%A1%9C%20%EC%82%B4%ED%8E%B4%EB%B3%B8%20%EB%A7%9D%EB%B6%84%EB%A6%AC%20%EA%B4%80%EB%A6%AC%EC%9D%98%20%EC%A4%91%EC%9A%94%EC%84%B1?searchItem=&searchWord=&bbsCateId=0&gotoPage=14  

http://blog.naver.com/PostView.nhn?blogId=ntower&logNo=221634711808&parentCategoryNo=&categoryNo=62&viewDate=&isShowPopularPosts=true&from=search  

https://m.blog.naver.com/PostView.nhn?blogId=zewang0505&logNo=110166368114&proxyReferer=https:%2F%2Fwww.google.com%2F  

책 :  
Amazon web services로 시작하는 클라우드 입문
