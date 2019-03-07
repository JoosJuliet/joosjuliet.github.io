---
layout: post
section-type: post
title: "[hacker_rank] Fibonacci Modified with python3"
category: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

문제 : https://www.hackerrank.com/challenges/fibonacci-modified/problem  

``` python
t1, t2, n = map(int, input().split())
ts = [t1, t2]+[0]*18

for i in range(2,n):
    ts[i] = ts[i-2] + ts[i-1]**2
    if i == n-1: print(ts[i])
print(ts)
```
