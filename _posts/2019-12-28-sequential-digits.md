---
layout: post
section-type: post
title: "[leet_code] 1291. Sequential Digits with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/contest/weekly-contest-167/problems/sequential-digits/


``` python
def sequentialDigits(low: int, hight: int) -> List[int]:
  low = 100
  high = 300
  digit = '123456789'

  low_length, high_length = len(str(low)), len(str(high))

  ans = []
  for d in range(low_length, high_length+1):
    for i in range(10-d): #길이를 여기랑 N[i:i+d] 여기서 측정한다.
      if low <= int(digit[i:i+d]) <= high: #하나씩 위치를 옮긴다.
        ans.append(int(digit[i:i+d]))
  return ans

```
