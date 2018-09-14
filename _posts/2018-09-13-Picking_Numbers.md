---
layout: post
section-type: post
title: "[hacker_rank] Picking Numbers with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank' ]
comments: true
---

문제 :
https://www.hackerrank.com/challenges/picking-numbers/problem

``` python
def pickingNumbers(a):
    d = Counter(a)
    previous_k = -1
    max_value = 0
    for k in sorted(d):
        if previous_k > 0 and ((k - previous_k) == 1):
            max_value = max(max_value, d[k] + d[previous_k])            
        else:
            max_value = max(max_value, d[k])
        previous_k = k
    return max_value

```



``` python

from collections import Counter # 콜렉션에서 불러옵니다.
def pickingNumbers(a):
  d = Counter(a)
  max_key = sorted(d)[len(d)]
  print(max_key)
  for i in a:
    if max_key < i:
      max_key = i
  dya = [[0]*2 for _ in range(max_key+1)]

  previous_k = -1
  max_value = 0
  for k in sorted(d):
    if previous_k > 0 and k - previous_k == 1:
      dya[k][0] = dya[previous_k][1]+ d[k]
      # 0은 과거것 더하기 현재것
      dya[k][1] = d[k]
      # 0은 과거것 더하기 현재것만
    else:
      dya[k][0] = d[k]
      dya[k][1] = d[k]

    if max_value < max(dya[k][0], dya[k][1]):
      max_value = max(dya[k][0], dya[k][1])
    previous_k = k

  return(max_value)

```
