---
layout: post
section-type: post
title: "[hacker_rank] Sherlock and Anagrams with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank' ]
comments: true
---

문제:
https://www.hackerrank.com/challenges/sherlock-and-anagrams/problem


일단 아나그램은 같은 글자로 다양한 글자를 만든 것이다.
ex) abc, acb는 아나그램이다.

``` python

import sys
from collections import defaultdict
from math import factorial

read = lambda : sys.stdin.readline().strip()

def ncr(n, r):
    if n < 2 : return 0
    return factorial(n) // (factorial(n-r) * factorial(r))

for _ in range(int(read())):
    word=read()
    multiset = defaultdict(lambda: 0) # Default 값을 0으로 설정합니다.

    for i in range(len(word)+1):
        for j in range(i+1,len(word)+1):
            tmp = word[i:j]
            if len(tmp)<len(word):
                multiset[''.join(sorted(tmp))] += 1
                # 일단 각 경우의 수를 다 subs에 넣는다.
    ans=0
    for i in multiset.values():
        ans += ncr(i, 2)
        # i개의 개수를 두개씩 정렬할 때의 경우의 수
        # 그 경우의 수가 두개이상이면 그건 아나그램이 될 수 있다...
    print(ans)

```
