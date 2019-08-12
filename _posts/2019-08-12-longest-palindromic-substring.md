---
layout: post
section-type: post
title: "[leet_code] 5. Longest Palindromic Substring with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/longest-palindromic-substring/

# 목표:
- 가장 긴 팰린드롭 문자열을 구하여라

# 조건:
- s의 길이는 1000이니 O(N**3)이 최선이다.

# solution 설명 :
- O(N**3)
- 이것 역시 brute force로 다해보는 것이다 ㅇ<-<


``` python
class Solution:
    def judgePalindrom(self,s):
        return s == s[::-1]
    def longestPalindrome(self, s: str) -> str:
        if len(s) == 1: return s
        len_ans = 0
        ans = ""
        for i in range(len(s)-1):
            for j in range(1, len(s)-i+1):
                sliteds = s[i:i+j]
                if self.judgePalindrom(sliteds) and len_ans < len(sliteds):
                    ans = sliteds
                    len_ans = len(ans)

        return ans
```
