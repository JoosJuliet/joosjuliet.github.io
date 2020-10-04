---
layout: post
section-type: post
title: "What is CORS?"
category: WEB
tags: [ 'CORS', 'english' ]
comments: true
---
# Goal
- understanding the principle of CORS
- How to get permission to access the CORS's mechanism




# What is CORS?
- CORS stands for cross-origin resource sharing, which is *a browser security mechanism* that restricts cross-origin HTTP requests.
- CORS is used for HTTP request security purposes.




## What is cross origin?
- Cross-origin refers to a HTTP situation in which one or all of the following is different: protocols, ports, or hosts.
- On the other hand, same-origin is when the HTTP has the same protocol, same port, and same host.
![same-origin-and-url-form](/images/2019-08-11-cors-english/same-origin-and-url-form.png)




# How does one get permission within CORS?
## To execute a simple request:
- Use the GET, HEAD method
- POST with Content-Type: application/x-www-form-urlencoded, multipart/form-data, or text/plain.  
- Add "Access-Control-Allow-Origin:\*" to the response header.
- Note that “Access-Control-Allow-Origin” represents the Key, and * represents a Value


## To execute a not Simple Request or add custom header to the request:

Use a preflight request to determine whether the CORS protocol is authorized.


![preflight](/images/2019-08-11-cors-english/preflight.png)
1. client -> server (in preflight request)
- As seen in the diagram, the preflight request process begins first with the client sending a request to the server, which returns an answer.   

- To use the OPTIONS method  
  - The client first sends a request to check whether the actual request might face a risk of the server’s state changing.
Next, the server then returns a


1. client -> server (in preflight request)
using OPTIONS method
- this request that first sends to check whether the actual thing is danger.
- That danger is that the state of the server changes.
2. server -> client (in preflight request)
- Next, the server then returns a response to the client. (in the preflight request)
- In a preflight request, the server gives the following key-value pair: access-control-allow origin, access-control-allow-methods, …
  - give Access-Control-Allow-Origin, Access-Control-Allow-Methods, Access-Control-Allow-Headers, Access-Control-Max-Age*
*Note: Access-Control-Max-Age indicates how long you can request a HTTP message.*




# Summary
CORS is restricts cross-origin HTTP requests between different origin in a browser security mechanism.  
If that method is simple method, you just add "Access-Control-Allow-Origin:\*" to the response header. The others, using preflight request And then you can get permission for a certain time.




---
reference :
- https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html
- https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS
