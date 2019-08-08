---
layout: post
section-type: post
title: "[leet_code] 395. Longest Substring with At Least K Repeating Characters with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---


문제 : https://leetcode.com/problems/repeated-dna-sequences/

# 목표:
- 길이가 10인 sub_string 중 개수가 2 이상인 sub_string을 구하라
# 조건:
- 없다
# solution 설명 :
- O(N)
- brute force로 모든 sub_string을 다 구한다.
- 그것을 defaultdict에 넣고 개수를 센다.


``` python
from collections import defaultdict

class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        counts = defaultdict(lambda: 0) # Default 값을 0으로 설정합니다.
        ans = set()
        for i in range(len(s)-9):
            sub_string = s[i:i+10]
            counts[sub_string] += 1
            if counts[sub_string] > 1: ans.add(sub_string)
        return ans
```
