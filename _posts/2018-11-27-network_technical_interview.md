---
layout: post
section-type: post
title: "[tech interview 3 편] Network"
categories: Tech_Interview
tags: [ 'interview', 'technology', 'it', 'network' ]
comments: true
---


# 글 요약
## 5-Layer TCP/IP Internet Model
￼
계층 별 communication
계층별 data-type

이 중
Layer3 - Network
에 대한 글을 써보겠습니다!



## Internetworking이란?
컴퓨터의 경우 사용하는 OS도 다양하고, program의 경우 아예 구현된 언어도 다르기 때문에 각 네트워크에서 이들을 통신할 수 있도록 하려면 공통된 protocol이 필요하다. 
즉 네트워크는 1.주소 체계가 다르고 2. 주고 받는 패킷의 형태가 다르다.
그런데 각각의 네트워크는 호환이 안됨으로 각각의 네트워크에 따른 specific한 기술을 적용해야한다. 이 비호환을 극복하고 통신을 제공하는 것이 internetworking이다.

## Internet
전세계의 컴퓨터가 서로 연결되어 TCP/IP 규약을 이용해 정보를 주고받는 공개된 컴퓨터 통신망

## Internet Infrastructure가 목표로 하는 디자인
- 서비스가 확장 되더라도 이를 수용할 수 있는 디자인
- 어떤 네트워크도 수용할 수 있도록 디자인

## Internet Infrastructure 철학
Internet
- 패킷 통신 서비스를 제공
- 패킷 형태에 제약 없고, 네트워크 기술에도 제약이 없다.
- endpoint는 모두 동일하게 취급한다.
- 어떤 endpoint든 모든 endpoint에 보낼 수 있다.
endpoint
- 모든 contents들을 제어하고 모든 서비스를 제공

철학의 이점
- 서로 다른 네트워크도 수용해 모든 서비스를 수용한다.
- 서비스와 통신을 따로 분리를 시켜 놓아야 해서, 서비스를 제공하는 사람은 통신 쪽을 몰라도 된다.

## Router
위의 인터넷 철학들을 구현하기 위해 생긴 것은 Router이다.

Router는 크게 두가지 일을 한다.
1. 패킷 포워딩
2. 형식 변환

패킷 포워딩은
 패킷을 받아서 도착지로 가는 최단경로로 가기 위해 다음 router로 가게 해주는 것이다.
형식 변환은
 서로 다른 네트워크는 주소/패킷의 형태가 다를 수 있음으로 이를 변환해 주는 것이다. 이 형식변환은 프로토콜 소프트웨어가 해결한다. ** 이 건 Layer3에 있는 IP라는 프로토콜** 로 해결한다.

> protocol이란 논리적으로 프레임 안에 있는 각 항목의 뜻과 기능, 자료 전송의 절차들을 구성할 수 있게 세운 규칙이다.
> 인터넷은 하나의 네트워크라고 말했지만, 실제로는 라우터와 작은 네트워크들로 구성되어 있음으로 존재하지는 않는다. 그래서 virtual network라고도 부른다.

## 계층 3 IP 프로토콜에서 일어나는 일
전체의 네트워크에서 동일한 주소를 사용해야 하기 때문에, IP주소를 만들어 모든 네트워크가 주소를 이해할 수 있게 한다.




forwarding table은  update는 목적과 의도에 따라 지속적으로 바꾼다.
(forwarding table과 routing table은 single network connection을 가진 system에서는 거의 비슷하게 행동하나 완전히 다른 일을 하는 것이다.)
[https://serverfault.com/questions/499760/difference-between-routing-and-forwarding-table]

흔히는 이 프로토콜에서 각 장치를 나타내는 IP 주소를 가리키는 말로 쓰인다.




———————


참고자료
https://www.slideshare.net/zephinzer/slideshare-5-layer-tcp-ip-model-for-the-layman
[TCP/IP 각각의 layer들에 대해서 정리가 잘되있습니다.]
http://datamining.dongguk.ac.kr/lectures/2009-1/info/internet-1.pdf




라우팅

2. mac adress [l2가지고 하는 것]
[이 것에 해당되는 포스팅도 분할 하겠습니다]
각자 할일만 하게 한다. 캡슐화를 잘 해놨기 때문에
layer가 바뀌어도 상관이 없다.


#CDN이란?
####CDN
* akamai : 이미지 caching


###akamai
전세계 각각의 통신사와 계약을 맺어 엣지포인트가 있다. 즉 다른 국가로 위치를 바꾸면 새로운 국가의 통신사와 연락을 주고 받아 바뀐 통신사 쪽에 캐싱을 해준다. 즉 물리적 거리가 줄어들어 빨라진다.
[ ex) 페이스북, 인스타그램 ]

# LoadBalance란?

loadbalance는  L4(IP),L7(APPLICATION)  두가지 버젼이 있다.

![server]({{ site.post_img}} /studyServer/server.png)

라우팅을 하는 방법은 여러가지가 있는데 그 중 하나가 바로 url을 통해서 입니다.
도메인 [ip -> L4 dns로] + path [L7이 처리하는 것 -> nginx]




 CDN system serves your content from the server which is closest to your visitor. They help to get around issues of network latency by serving your content as close to the visitor as possible.





loadbalance가 해주는 게
트래핑으로 위해 gzip으로 압축을 하고, ssl 패킹, 서버를 묶어주는 것 , logging

### 정리하면

 | L4 | L7 |
 | :--- | :---  |
 | IP를 LOADBALACE |  loadbalacing하는데 데이터 흐름에 대해서 분배를 해준다. |
 | roundrobin으로 routing한다. |  정해진 url로 보낸다.  |

참고 ) round robin이란?
프로세스들 사이에 우선순위를 두지 않고, 순서대로 시간단위(Time Quantum)로 CPU를 할당하는 방식의 CPU 스케줄링 알고리즘

#Nginx란?


h/w -> sw세계
	nginx,haproxy,appache  -> gcp,aws
-->  h/w에서 부분.png




이제는 초반에는 server 역할을 하던 nginx,haproxy,appache가 routing 역할을 중점으로 하게 되었습니다.  
nginx
 - xml같은 것 할 때 더 가볍게 해야하는 것
 - blob데이터들은 압축을 해서 보내주는데 미리 압축 해논 것을 보내는 기능
 - (참고) express에도 미리 압축한 것을 저장 해 놓아 주는 것도 있다.




애니캐스트와 spanner

http://tech.kakao.com/2014/05/29/anycast/
https://www.psychz.net/client/kb/ko/learn-about-anycast-and-some-of-its-advantages-and-disadvantages.html


gclb는 내가 ssl을 직접 올려야 한다. cloudfront는 알아서 자기가 해준다.


라우팅
1. url 입력
도메인[ip -> l4  dns로] + path [l7이 처리해주는 것]
2. mac adress [l2가지고 하는 것]
[이 것에 해당되는 포스팅도 분할 하겠습니다]
각자 할일만 하게 한다. 캡슐화를 잘 해놨기 때문에
layer가 바뀌어도 상관이 없다.


비트나미 는 여러가지 어플리케이션 솔루션들을 다양한 환경에 쉽게 설치할 수 있게 패키지를 만들어 배포해주는 회사



https://www.lifewire.com/layers-of-the-osi-model-illustrated-818017





	#nginx appache의 가장 큰 차이
	#nginx 는  event-loop방식[비동기] 작은 작업 많이 할 때 노드가 그런 일에 강한 것
	#appache 멀티 프로세스 + 멀티 쓰레드 돌아가는- 적당수 process만들 고 각각의 하나하나 프로세스들이] = 부모와 자식관계 = 다들 계속 자식들을 만든다. 대신에 overhead가 크다. 그래서 nginx방식인 이벤트루프 방식
	#tensorflow같은 경우 멀티 프로세스 쓰레드 를 하기에는.... event loop 하기에도 그러고 그냥 돌려랏
	#iptable  ,
	# loopback 을 막는다.
	#fastcgi_pass  ->  submodule들과 통신하는 방법들

gzip_proxied any;
	#앞단에 lb있는데 any를 안하면 압축을 안한다. lb가 하겠찌 하고 근데 그렇다고 해도 뭐 둘다 안한다.
# LoadBalance란?

loadbalance는  L4(IP),L7(APPLICATION)  두가지 버젼이 있다.

![server]({{ site.post_img}} /studyServer/server.png)


instance group


라우팅
1. url 입력
도메인[ip -> l4  dns로] + path [l7이 처리해주는 것]
2. mac adress [l2가지고 하는 것]

애니캐스트?
dns에게 알려줘서 그 근처 dns인 kt에게
같은 아이피인데 통신사마다 다른 곳으로 알려주는 것 [dns를 통해]

리전 balancing
가까운 곳에 가면 자동으로 해당 지역에 접속할 수 있도록

https://www.digitalocean.com/community/tutorials/how-to-configure-dns-round-robin-load-balancing-for-high-availability





L5는 왜?!
L4는 L7과 다르게 5,6,7 layer가 없습니다.
즉 L4는 broad cast를 하는데 [보통 이런 것을 hub기능이라고 합니다.]application은 정해진 사람한테만 전해주는 switching 기능이 잇습니다.

* L5 Session Layer
The Session Layer manages the sequence and flow of events that initiate and tear down network connections. At Layer 5, it is built to support multiple types of connections that can be created dynamically and run over individual networks.

*

gcp GCLB
As cloudfront

### 어떤 layer덕분에 그게 되는지는 찾아보기

loadbalance가 해주는 게
트래핑으로 위해 gzip으로 압축을 하고, ssl 패킹, 서버를 묶어주는 것 , logging




# 정리하면

 | L4 | L7 |
 | :--- | :---  |
 | IP를 LOADBALACE |  loadbalacing하는데 데이터 흐름에 대해서 분배를 해준다. |
 | roundrobin으로 routing한다. |  정해진 url로 보낸다.  |

참고 ) round robin이란?
프로세스들 사이에 우선순위를 두지 않고, 순서대로 시간단위(Time Quantum)로 CPU를 할당하는 방식의 CPU 스케줄링 알고리즘

##


#Nginx란?


h/w -> sw세계
	nginx,haproxy,appache  -> gcp,aws
-->  h/w에서 부분.png




이제는 초반에는 server 역할을 하던 nginx,haproxy,appache가 routing 역할을 중점으로 하게 되었습니다.  



xml같은 것 할 때 더 가볍게 해야하는 것
nginx

nginx 압축을 해서 보내주는데
미리 압축 해논 것을 보내는 기능

express에도 미리 압축한 것을 저장 해 놓아 주는 것도 있따.
근데 이기능은 nginx에도 있다.




dns 는 따로 노는 것

akamai ->
전세계에 엣지포인트가 있다.[전세계 통신사와 계약]
다른 곳으로 위치를 바꾸면 해당 국가의 통신사에게 연락을 해서 캐싱을 시켜준다.
즉 빨라진다. //근데 비싸
[ 페이스북, 인스타그램이 쓴다]



storage를 쓰면 land balance에서 캐싱을 해준다.


storage->blob데이터를 저장
sql -> text data

그렇지만 조아라 같은 경우 sql보다는 storage에다가 하는 게 좋다.


이런 것을 아는 경우 deadlock을 생각할 수 있다.




gclb는 내가 ssl을 직접 올려야 한다.
cloudfront는 알아서 자기가 해준다.



애니캐스트와 spanner

http://tech.kakao.com/2014/05/29/anycast/
https://www.psychz.net/client/kb/ko/learn-about-anycast-and-some-of-its-advantages-and-disadvantages.html







udp
user datagram protocol
안정적이지 않고 순서도 보장되지 않는다. 데이터를 잃을 수도, 중복될 수도 있다. 대신 빠르다
전화 같은 경우 되겠네

tcp
transmission control protocol
안정성과 순서를 보장



우리는 3이상부터 중요하다.
우리는 L4부터 한다.
L3 switch ( 정해진 사람한테만 준다)
L2 hub (broadcast)
L1    -> MACaddress

loadbalance는 L4(IP),L7(APPLICATION)

L4 :는 IP를 LOADBALACE
L7 는 application은 loadbalacing하는데
데이터 흐름에 대해서 분배를 해준다.




roundrobin으로 순서대로 돈다. [무조건 순서대로 가야한다. 누구한테 가는지를 못정한다.]-> L4

L7은 roundrobin보다 더 똑똑히 누가 누구한테 가는지를 정해줄 수 있다.
ex)
a.com/b/c ->1번서버
b.com/d/e ->2번서버

a.com/b/c ->3번서버

이건 L7만 가능




line정도는 haproxy쓴다.

h/w -> sw세계
	nginx,haproxy,appache  -> gcp,aws


gcp GCLB
aws cloudfront

loadbalance가 해주는 게
트래핑으로 위해 gzip으로 압축을 하고, ssl 패킹, 서버를 묶어주는 것 , logging

xml같은 것 할 때 더 가볍게 해야하는 것
nginx


nginx 압축을 해서 보내주는데
미리 압축 해논 것을 보내는 기능

express에도 미리 압축한 것을 저장 해 놓아 주는 것도 있따.
근데 이기능은 nginx에도 있다.

client          firewall             lb                                    was
								 의 포함관계가 webserver


우리는 서버앞에 nginx를 둘 수 있는데 그 앞에 하나 더 둘 수 있다.

client     -         !!!!!!!!      								-					-		-
		cloud flare[anti didos, ssl 관리]			load balance			web server		
		aKamai[이미지 caching (cdn역할)]


		 cdn , fw															was


dns 는 따로 노는 것

akamai ->
전세계에 엣지포인트가 있다.[전세계 통신사와 계약]
다른 곳으로 위치를 바꾸면 해당 국가의 통신사에게 연락을 해서 캐싱을 시켜준다.
즉 빨라진다. //근데 비싸
[ 페이스북, 인스타그램이 쓴다]


cert-bot은 서버에 깔 때만 된다.
load balancing에 붙이면 안된다.


storage를 쓰면 land balance에서 캐싱을 해준다.


storage->blob데이터를 저장
sql -> text data

그렇지만 조아라 같은 경우 sql보다는 storage에다가 하는 게 좋다.


이런 것을 아는 경우 deadlock을 생각할 수 있다.




gclb는 내가 ssl을 직접 올려야 한다.
cloudfront는 알아서 자기가 해준다.


greenbar는 진짜 안전한 업체다 이렇게 나온 것




사진을 가지고 resizing을 때에 따라 다르게 해야한다.
그러므로 올린 사진들은 storage에 다 잘 저장을 해야한다.
glacier : 저장을 해놓음


프록시 서버(영어: proxy server 프락시 서버)는 클라이언트가 자신을 통해서 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해 주는 컴퓨터나 응용 프로그램



# WAN과 LAN
LAN은 Local Area Network의 약자로 사용자가 포함된 지역 네트워크
쉽게 말씀드리면 학교, 회사, 집에서 컴퓨터, IP 전화기등의 장비를 서로 연결한 거에요.​
이 때 컴퓨터끼리 1대1로 직접 연결하는게 아니라 공유기나 스위치등을 이용해서

아래 사진과 같이 연결하게 됩니다.​
LAN은 이더넷이라는 프로토콜
​​

WAN은 Wide Area Network 의 준말로써 LAN과 LAN 사이를
광범위한 지역 단위로 구성하는 네트워크

WAN은 LAN과 LAN사이를 이어


















upstream drf {
        server unix:///home/linku/LinkU/linku_backend/linku.sock;
}

server {
        listen 443 ssl;

        root /usr/share/nginx/;
        # index index.html index.htm;

        server_name linkuniversity.me www.linkuniversity.me;

        ssl on;
        ssl_certificate /etc/letsencrypt/live/linkuniversity.me/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/linkuniversity.me/privkey.pem;

        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;
        ssl_dhparam /etc/ssl/certs/dhparam.pem;
        ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
        ssl_session_timeout 1d;
        ssl_session_cache shared:SSL:50m;
        ssl_stapling on;
        ssl_stapling_verify on;
        add_header Strict-Transport-Security max-age=15768000;


        location / {
                try_files $uri $uri/ /index.html;
        }

        location /static {
                alias /home/linku/LinkU/linku_backend/static;
        }

        location /media {
                alias /home/linku/LinkU/linku_backend/media;
	}


	location /admin {
                uwsgi_pass drf;
                include /home/linku/LinkU/linku_backend/uwsgi_params;
        }

        location /api {
                rewrite /api/(.+) /$1 break;
                uwsgi_pass dry;
                include /home/linku/LinkU/linku_backend/uwsgi_params;
        }

        location ~ /.well-known{
                allow all;
        }

}

server {
    listen 80;
    server_name linkuniversity.me www.linkuniversity.me;
    return 301 https://$host$request_uri;
}


Explain about DNS?
DNS - Domain Name System. DNS is the Naming System for the resources over Internet; includes Physical nodes and Applications. DNS –It is the easy way to locate to a resource easily over a network and serves to be an essential component necessary for the working of Internet.

What is a Network?
A network means a set of devices that connected by physical media links. A network is recursively a connection of more than two nodes by a physical link or two or more networks connected by one or more nodes.

What is Bandwidth?
Each and Every Signal often has a limit of an upper range and lower range of frequency of signal it can carry. So this range of limit of network between its upper frequency and lower frequency is termed as Bandwidth.

What is the DNS forwarder?
DNS servers usually communicate with outside DNS servers of the local network. A forwarder is an entry that is used when a DNS server receives DNS queries that it cant resolve locally. And then it forwards those requests to external DNS servers for resolution


What is a gateway or Router?
A router or gateway is a node that is connected to two or more networks. In general it forwards message from one network to another.

What is MAC address? Does it have some link or something in common to Mac OS of Apple?
MAC - Media Access Control. MAC is the address of the device identified at Media Access Control Layer of Network Architecture. Similar to IP address MAC address is unique address, i.e., no two device can have same MAC address. MAC address is stored at the ROM Read Only Memory of the device.

MAC Address and Mac OS are two different things and it should not be confused with each other. Mac OS is a POSIX standard Operating System Developed upon FreeBSD used by Apple devices.

What is IP?
IP is a unique 32 bits software address of a node in a network.

What is private IP?
Three ranges of IP addresses have been reserved for private address and they are not valid for use on the Internet. If you want to access internet with these address you must have to use proxy server or NAT server (on normal cases the role of proxy server is played by your ISP.).If you do decide to implement a private IP address range, you can use IP addresses from any of the following classes:

Class A: 10.0.0.0 10.255.255.255
Class B: 172.16.0.0 172.31.255.255
Class C: 192.168.0.0 192.168.255.255

What is public IP address?
A public IP address is an address leased from an ISP that allows or enables direct Internet communication.


List the different layers under TCP/IP?
There are four layers:

Network Layer
Internet Layer
Transport Layer
Application Layer.

Describe VPN?
VPN - Virtual Private Network. It is a technology that allows a secure tunnel to be created across a network such as the Internet.
