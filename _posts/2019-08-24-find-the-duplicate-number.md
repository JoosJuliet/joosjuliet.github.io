---
layout: post
section-type: post
title: "[leet_code] 287. Find the Duplicate Number with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/find-the-duplicate-number/

# Aim:
- 중복된 숫자 있으면 보여줘라

# solution :
- python 카운터를 이용해서 풀었다.

``` python
from collections import Counter # 콜렉션에서 불러옵니다.

class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        nums = Counter(nums)
        return list(filter(lambda x: nums[x] >= 2, nums))[0]

```
