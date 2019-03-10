---
layout: post
section-type: post
title: "[hacker_rank] The Maximum Subarray with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---

제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)


문제 : https://www.hackerrank.com/challenges/maxsubarray/problem

``` python

for _ in range(int(input())):
    d = [0] * int(input())
    minus_sum = 0

    for i, v in enumerate(map(int, input().split())):
        d[i] = max(d[i - 1] + v, v)
        if v > 0:
            minus_sum += v

    if minus_sum == 0:
        print(max(d), max(d))
    else:
        print(max(d), minus_sum)

```
