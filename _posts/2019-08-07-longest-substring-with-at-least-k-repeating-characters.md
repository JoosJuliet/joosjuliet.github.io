---
layout: post
section-type: post
title: "[leet_code] 395. Longest Substring with At Least K Repeating Characters with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---


문제 : https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/

# 목표:
- k개 이상의 연속된 알파벳들로 이루어진 가장 긴 substring의 길이구하기
# 조건:
- 그딴거 없어'-'
# solution 설명 :
1. k보다 적은 수의 알파벳을 기준으로 string을 자른다.  
2. 그 substring이 k개 이상의 연속된 알파벳들로 이루어진 substring이면 ans에 넣는다.  
3. 그 substring이 적합한 애인지 확인하고 ans에 넣는다.
4. ans에 가장 큰 애가 답이다.


``` python
from collections import Counter # 콜렉션에서 불러옵니다.
from functools import reduce


class Solution:

    def confirmSubstring(self, countOfS, k):
        return list(filter(lambda x: countOfS[x] < k, countOfS))


    def longestSubstring(self, s: str, k: int) -> int:
        ans = [0]
        countOfS = Counter(s)
        confirmed_substrings = self.confirmSubstring(countOfS, k)
        if len(confirmed_substrings) == 0: return sum(countOfS.values())
        else:
            for i in confirmed_substrings:
                s = s.replace(i,',')
            sp = s.split(',')
            for j in sp:
                if j == '': continue
                ans.append(self.longestSubstring(j, k))
        return max(ans)
```
