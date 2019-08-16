---
layout: post
section-type: post
title: "[leet_code] 179. Largest Number with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/largest-number/

# 목표:
- array의 값으로 값을 만드는데 그 값의 최대수를 구하여라
# solution 설명 :
- 비교를 할 때 두값을 이어 붙였을 때 가장 큰 값인 것을 기준으로 sort를 할 수 있게 만들면 된다.


``` python
from functools import cmp_to_key
# 자기가 원하는 대로 비교해서 sort를 할 수 있게 만들어주는 function
# 자신이 임의로 그 비교방법을 def로 정하고, 그걸 cmp_to_key로 그 def를 쌓으면 된다.
def compareTo(a, b):
    # string 으로 크기비교 하는것
    # "2"+"30"=230 과 "30"+"2"=302 비교
    return 1 if a+b >= b+a else -1

def largestNumber(nums):
    nums = sorted(map(str, nums), key = cmp_to_key(compareTo), reverse = True)
    res = ''.join(nums).lstrip('0')
    return res if res else "0"

print(largestNumber([3,30,34,5,9]))
print(largestNumber([0,0]))

```
