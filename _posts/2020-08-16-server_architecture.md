---
layout: post
section-type: post
title: "how to make tolerance server to handle millions of requests per second?"
category: Architect
tags: [ 'Architect' ]
comments: true
---


# 1. Comprehension of requirements  
We should be considered how much traffic is sustained for a long time, how many requests should be processed at a time (throughput), and how much hardware resources should be consumed per request. How high availability is required, etc. Accordingly, the design of the system will be changed for a bit.But according to question, I will focus on the system to create a tolerance system in terms of each layers of system.  




# 2. Web Server  
If there are 1 million users per second, it is impossible to operate with one web server, so we have to use multiple web servers. Since reliability is an important service, a web server that can process requests asynchronously is appropriate.  




# 3. Database
Because reliability is crucial factor, we need a database that supports ACID and performs well at any scale.




# 4. Prevention of propagation of failure  
In the happening of a specific service is dead, a circuit breaker is required to prevent failure propagation to other systems. Also, Need a system that can monitor the network and hardware resource status of the service.  
