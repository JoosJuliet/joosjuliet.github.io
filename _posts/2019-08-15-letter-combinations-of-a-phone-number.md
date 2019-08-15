---
layout: post
section-type: post
title: "[leet_code] 17. Letter Combinations of a Phone Number with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/letter-combinations-of-a-phone-number/

# 목표:
- 각 숫자에는 한글이 연결되어 있다.
- 주어진 폰 숫자로 만들 수 있는 모든 글자를 구하여라.

# 조건:

# solution 설명 :
- 모든 경우의 수를 다하는 것이다.
- 각 for문의 경우의 수 별로 다 하는 것이다.

``` python
class Solution:
    def dfs(self, ans, tmp, mapping_dict, digits):
        if len(digits) == len(tmp):
            return tmp
        for i in mapping_dict[digits[len(tmp)]]:
            tmp_s = self.dfs(ans, tmp + i, mapping_dict, digits)
            if tmp_s != '': ans.append(tmp_s)
        return ''

    def letterCombinations(self, digits: str) -> List[str]:
        mapping_dict = {'2':['a','b','c'],'3':['d','e','f'],'4':['g','h','i'],'5':['j','k','l'],'6':['m','n','o'],'7':['p','q','r','s'],'8':['t','u','v'],'9':['w','x','y','z']}
        ans = []
        self.dfs(ans, "", mapping_dict, digits)
        return ans
```
