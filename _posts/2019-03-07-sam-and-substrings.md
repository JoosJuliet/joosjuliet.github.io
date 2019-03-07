---
layout: post
section-type: post
title: "[hacker_rank] Sam and substrings with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---

제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)


문제 : https://www.hackerrank.com/challenges/sam-and-substrings/problem

``` python

n = input()

ans = 0
mod = 10**9+7

multiply = 1
for i in range(0,len(n))[::-1]:
    ans +=  int(n[i]) * multiply *(i+1)
    ans %= mod
    multiply = (10*multiply+1)%mod    # # 각자리수 하나를 뺀다.
print(ans)

```
