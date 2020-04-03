---
layout: post
section-type: post
title: "[leet_code] 202. Happy Number with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', '30days' ]
comments: true
---
문제 : https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/528/week-1/3284/
https://leetcode.com/problems/happy-number/


1. 4가 되면 무한루프가 나온다고 한다...
``` python

class Solution:
    def isHappy(self, n: int) -> bool:
        while n != 1:
            n = sum([int(i) ** 2 for i in str(n)])
            if n == 4:
                return False

        return True
```


2. 풀이설명: 이미 나왔던 숫자가 다시 나오면 무한루프가 나오기 때문에 set을 이용해 무한루프 확인
``` python
def isHappy(n: int) -> bool:
    notHappy = set()
    while n != 1:
        notHappy.add(n)
        n = sum([int(i) ** 2 for i in str(n)])
        if n in notHappy:
            return False
    return True
```
