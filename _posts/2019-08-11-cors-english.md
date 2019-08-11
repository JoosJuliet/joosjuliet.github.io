---
layout: post
section-type: post
title: "What is CORS?"
category: WEB
tags: [ 'CORS', 'english' ]
comments: true
---
# Goal
- understanding CORS
- How to get permission to CORS's mechanism




# What is CORS?
- Cross-origin resource sharing (CORS) is *a browser security mechanism* that restricts cross-origin HTTP requests.(Between different origin)


## What is cross origin?
- not same-origin is cross-origin
- Same-origin is Same protocol, same port, same host.
![same-origin-and-url-form](/images/2019-08-11-cors-english/same-origin-and-url-form.png)




# How to get permission in CORS policy?
## Simple Request
- GET, HEAD method 
- POST with Content-Type: application/x-www-form-urlencoded, multipart/form-data, or text/plain.   

Add "Access-Control-Allow-Origin:\*" to the response header.


## not Simple Request or add custom header to the request

Using preflight request  
that request checks to see if the CORS protocol is autohrized.

![preflight](/images/2019-08-11-cors-english/preflight.png)

1. client -> server (in preflight request)
using OPTIONS method
- this request that first sends to check whether the actual thing is danger.
- That danger is that the state of the server changes.
2. server -> client (in preflight request)
- give Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers,
- give Access-Control-Max-Age
*Access-Control-Max-Age  
It tells how long you can request.*




# Summary
CORS is restricts cross-origin HTTP requests between different origin.  
If that method is simple method, you just add "Access-Control-Allow-Origin:\*" to the response header. The others, using preflight request And then you can get permission for a certain time.

  -


---
reference :
- https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html
- https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS
