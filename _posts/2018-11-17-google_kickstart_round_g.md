---
layout: post
section-type: post
title: "[google codejam kickstart] 2018 ground g solution with python"
category: Algorithm
tags: [ 'algorithm', 'python', 'kickstart' ]
comments: true
---
새로 만든 tag인 kickstart 첫 글!
계속 꾸준히 kickstart 참여중이다

처음에는 한문제도 못풀었다가 ^^
점점 test case 몇개는 통과시키다가, 첫문제의 small case라도 풀 때도 있게 되고, big case도 풀 때도 있기도 하고...

*(너무)* 천천히 늘어가는 내 알고리즘 실력을 알게 해주는 좋은 대회다


# problem 1 solution
  - O(N^3)
  - small case 통과만 된다.

0과 1처리가 까다롭다.

``` python
import sys
read = lambda : sys.stdin.readline().strip()

def solve(n, l):
    l.sort()
    d = {}
    for i in range(len(l)):
        d[i+1] = l[i]
    ans = 0
    for i in range(1, len(l)+1):
        for j in range(i+1, len(l)+1):
            for k in range(j+1, len(l)+1):
                if d[i]*d[j] == d[k] or d[j]*d[k] == d[i] or d[i]*d[k] == d[j]:
                    ans += 1
    return ans


for t in range(1, int(read()) + 1):
    n = int(read())
    print("Case #{}: {} ".format(t, solve(n, list(map(int, read().split())))))

```
