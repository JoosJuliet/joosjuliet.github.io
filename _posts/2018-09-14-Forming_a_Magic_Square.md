---
layout: post
section-type: post
title: "[hacker_rank] Forming a Magic Square with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank' ]
comments: true
---

문제: https://www.hackerrank.com/challenges/magic-square-forming/problem


``` python
from itertools import permutations

# Complete the formingMagicSquare function below.
def formingMagicSquare(s):
    comb = permutations(range(1,10),9)
    min_ans = sys.maxsize

    for tuple1 in comb:
        if  (tuple1[0] + tuple1[1] + tuple1[2]) == (tuple1[3] + tuple1[4] + tuple1[5]) == (tuple1[6] + tuple1[7] + tuple1[8]) == (tuple1[0] + tuple1[3] + tuple1[6]) == (tuple1[1]+ tuple1[4] + tuple1[7]) == (tuple1[2]+ tuple1[5] + tuple1[8])== (tuple1[0]+ tuple1[4]+tuple1[8])== (tuple1[2]+tuple1[4]+ tuple1[6]) :

            s2 = [[tuple1[0],tuple1[1], tuple1[2]], [tuple1[3],tuple1[4],tuple1[5]],[tuple1[6],tuple1[7],tuple1[8]]]

            ans = 0
            for i in range(0,3):
                for j in range(0,3):
                    if s[i][j] != s2[i][j]:
                        ans +=abs(s[i][j]-s2[i][j])

            if min_ans > ans:
                min_ans = ans

    return min_ans

```
