---
layout: post
section-type: post
title: "[hacker_rank] The Power Sum with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank' ]
comments: true
---

문제:
https://www.hackerrank.com/challenges/the-power-sum/problem

``` python

import sys
import math
read = lambda : sys.stdin.readline().strip()

x = int(read())
# 목표값
n = int(read())
# 몇제곱인지 나오는 값
d = [0]*(x+1)


def power_sum(x, n):
    return calc(x, n, 1)


def calc(x, n, num):
    num_to_n = int(num ** n)
    if num_to_n > x:
        return 0
    elif num_to_n == x:
        return 1
    else:
        return calc(x, n, num+1) + calc(x-num_to_n, n, num+1)

print(power_sum(x, n))


```



# 어찌 만들어지는 지 보여주는 것
```
                  (10,2,1)                   ->1^2
                 /        \
                /          \
          (10,2,2)        (9,2,2)            ->2^2
          /     \         /     \
         /       \       /       \
     (10,2,3) (6,2,3)  (9,2,3) (5,2,3)       ->3^2
     /     \      |       |       |
    /       \     0       1       0
 (10,2,4) (1,2,4)                            ->4^2
     |       |
     0       0
```
1뺀것은 오른쪽으로 그대로는 왼족으로
tree만들어서 구한다.
https://www.hackerrank.com/challenges/the-power-sum/forum
의 `hacetin` 설명 참고
