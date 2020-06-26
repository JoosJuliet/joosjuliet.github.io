---
layout: post
section-type: post
title: "[leet_code] Weekly Contest 193 (Running Sum of 1d Array, Least Number of Unique Integers after K Removals) with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---


# 1480. Running Sum of 1d Array
문제 : https://leetcode.com/contest/weekly-contest-193/problems/running-sum-of-1d-array/


``` python
class Solution:
    def runningSum(self, nums: List[int]) -> List[int]:
        return [sum(nums[:i+1]) for i in range(0,len(nums))]
```


# 1481. Least Number of Unique Integers after K Removals
문제 : https://leetcode.com/contest/weekly-contest-193/problems/least-number-of-unique-integers-after-k-removals/


``` python
class Solution:
    def findLeastNumOfUniqueInts(self, arr: List[int], k: int) -> int:
        v = sorted(collections.Counter(arr).values(), reverse = True)
        while v and k>=v[-1]: k -= v.pop()
        return len(v)
```
