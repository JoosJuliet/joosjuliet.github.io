---
layout: post
section-type: post
title: "What is the difference between session and cookies(feat. token)"
category: Web
tags: [ 'session', 'cookies' ]
comments: true
---
What we first notice is Why we are using session/cookies.
That's because http is stateless. So we don't know requester and previous user's state.

So We are using Cookies and Sessions.
they are used to store information.

# cookies vs session
![cookie_vs_session](/images/2019-08-25-cookie_session/session_cookie.png)
A session are stored in server memory(or db). So We can use control session's lifecycle. Commonly session's life time is 30 minutes.

Cookies are stored on the client computer and they are kept of use tracking purpose. Server script sends a set of cookies to the browser. For example name, age, or identification number etc. The browser stores this information on a local machine for future use. (that's why some website need to agree cookie's policy.)

When next time browser sends any request to web server then it sends those cookies information to the server and server uses that information to identify the user. That's why session is implemented using cookies.


---
reference:
https://www.tutorialspoint.com/What-is-the-difference-between-session-and-cookies
https://farahbloggingworld.wordpress.com/2013/09/11/cookies-vs-sessions/
