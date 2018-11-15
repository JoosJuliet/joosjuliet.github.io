---
layout: post
section-type: post
title: "[hacker_rank] Extra Long Factorials with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---

문제 :
https://www.hackerrank.com/challenges/extra-long-factorials/problem


# solution 1

``` python
def extraLongFactorials(n):
    return reduce(lambda x, y: x*y, range(1, n+1))
```

# solution 2


``` python
import sys
sys.setrecursionlimit(10**6)
read = lambda : sys.stdin.readline().strip()


def get_factorial2(n):
    old = [1]
    current = []
    for i in range(2, n+1):
        carry = 0
        print(old)
        for digit in old:
            prod = digit * i + carry
            current.append(prod % 10)
            carry = prod // 10
            # 몫

        if carry != 0:
            for j in str(carry)[::-1]:
                # carry 거꾸로 뒤집기
                current.append(int(j))  # add j as a str
        old = current
        current = []

    return "".join(map(str,old[::-1])) # convert everything to str before concatenation and returning the results

print(get_factorial2(int(read())))

```
