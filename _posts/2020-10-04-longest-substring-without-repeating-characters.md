---
layout: post
section-type: post
title: "[leet_code] 3. Longest Substring Without Repeating Characters with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---

문제: https://leetcode.com/problems/longest-substring-without-repeating-characters/  
# brute force

time limit: O(n**3) n -> length of sentence  
1.  일단 n까지 쭉 순회를 한다.  
2. 순회를 하는동안 그 숫자까지 index의 substring을 가지고 set을 확인한다.  

``` python
class Solution:
    def lengthOfLongestSubstring(self, sentence: str) -> int:
        n = len(sentence)
        if n == 1: return 1
        def unique(s, e):
            sets = set()
            for i in range(s, e):
                if sentence[i] in sets:
                    return False
                sets.add(sentence[i])
            return True

        ans = 0
        for i in range(n):
            for j in range(i+1, n+1): # n+1까지 하는 이유는 n까지 다 도착하게 하기 위해서이다?
                if unique(i, j):
                    ans = max(ans, j-i)
        return ans
```


# two pointer 사용  

time limit: O(2n)  
1. 첫번째 포인터 right는 계속 움직이다.  
2. 두번째 포인터는 만약 중복되는 글자가 나왔다면, 그 중복된 수가 나올 때까지 계속 이동한다.  
3. 만약 중복된 글자가 나오지 않는다면 left는 계속 그 자리에 있다.  
4. substring이 완성될때마다 max값을 비교한다.  

``` python

class Solution:
    def lengthOfLongestSubstring(self, sentence: str) -> int:
        n, seen = len(sentence), set()
        result, left = 0, 0
        for right in range(n):
            if sentence[right] not in seen:
                seen.add(sentence[right])
            else:
                while sentence[left] != sentence[right]:
                    seen.discard(sentence[left])
                    left+=1
                left+=1
            result = max(result, right-left+1)

        return result   
```
