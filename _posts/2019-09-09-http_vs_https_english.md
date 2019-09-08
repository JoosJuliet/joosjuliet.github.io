---
layout: post
section-type: post
title: "how to created https?, http vs https"
category: Computer_science
tags: [ 'computer_science', 'network', '글또3기' ]
comments: true
---


# What is HTTPS?
## What is the security weakness of HTTP??
Since HTTP is based on plain text data, sensitive information such as user information is exposed on the Internet.
Also, since it is connectless which is a big feature of http, it is impossible to accurately determine the client.
This allows for a man-in-the-middle attack.
One way to prevent this is https.


## What is man-in-the-middle attack?  
While data is being transferred between the server and the client, an attacker can place itself between the two and intercept the data.
You may believe that both sides are talking to each other, but you are actually communicating with the abuser.

## So what is the role of HTTPS?
Information can be assessed to ensure that the access site is trusted, using SSL certificates, with HTTPS communication to prevent man-in-the-middle attacks that can be collected or tampered with.


## What is HTTPS?

![https](/images/2019-09-08-http_vs_https/https.png)

SSL is a communication layer developed for data security.
HTTPS is a method of passing HTTP over the SSL layer. In other words, the plaintext HTTP document is encrypted by passing through the SSL layer and arrives at the destination. In addition, SSL is an expression layer protocol that lies below the application layer, so that any application layer data can be encrypted and sent.


Sometimes HTTPS is recognized as a protocol, and HTTP and SSL are combinations of protocols at completely different layers. This is more accurate with HTTPS over SSL.



---
참고자료

http에 대한 설명  
https://ko.wikipedia.org/wiki/HTTP  
https://www.joinc.co.kr/w/Site/Network_Programing/AdvancedComm/HTTP +https설명까지  

중간자 공격 설명  
https://blog.naver.com/PostView.nhn?blogId=ucert&logNo=221201640816&categoryNo=37&parentCategoryNo=0  
