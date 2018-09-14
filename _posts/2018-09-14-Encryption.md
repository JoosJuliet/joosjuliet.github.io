---
layout: post
section-type: post
title: "[hacker_rank] Encryption with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank' ]
comments: true
---

문제 :
https://www.hackerrank.com/challenges/encryption/problem


``` python

def encryption(s):
    for j in range(len(s),0,-1):
        if (j-1)*(j-1) <= len(s) <= j*j:
            n, m = j-1, j
            if n * m < len(s):
                n += 1
            if (j-1)*(j-1) == len(s):
                n, m = j-1,j-1
            break
        else:
            continue

    tmp_s = []
    for i in range(n):
        tmp = s[:m]
        if len(tmp) < m:
            tmp = tmp + ' '*(m -len(tmp))
        tmp_s.append(tmp)
        s = s[m:]
    ans = ''
    for j in range(0,m):
        tmp = ''
        for i in range(0,n):
            if tmp_s[i][j] == ' ':
                tmp += ''
            else:
                tmp += tmp_s[i][j]
        ans += (tmp + ' ')
    return ans
```
