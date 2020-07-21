---
layout: post
section-type: post
title: "[ leet_code ] [weekly-contest-197 solution] Number of Good Pairs, Number of Substrings With Only 1s, Path with Maximum Probability"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
문제 : https://leetcode.com/contest/weekly-contest-197/

# 1512. Number of Good Pairs
TimeComplexity: O(N)  
1. 각 nums의 값들을 센다.
2. 그 값들을 nCr로 계산을 하는데 어차피 r은 2가 되니까 n*(n-1)//2로 봐도 된다.
3. nCr한 값들을 다 더한다.

``` python
class Solution:
    def numIdenticalPairs(self, nums: List[int]) -> int:
        return sum(k * (k - 1) // 2 for k in collections.Counter(A).values())
```




# 1513. Number of Substrings With Only 1s
TimeComplexity: O(N)  
1. 각 s의 글자들이 포함되는 집합의 개수를 구한다.
2. 그 개수를 다 더한다.  
참고 만약에 0이 되면 그 포함되는 집합이 다시 초기화된다.  

The writer did not make use of the above formulae directly. Instead, accumulatively plus the number of '1' to achieve the same intention. For example:
'1': 1
'11': 1 + 2
'111': 1 + 2 + 3
``` python
class Solution:
    def numSub(self, s: str) -> int:
        # cnt = 0
        # ans = 0
        # for i in s:
        #     cnt = 0 if i == '0' else cnt+1
        #     ans += cnt
        # return ans %(10**9 + 7)
        return sum(len(a) * (len(a) + 1) / 2 for a in s.split('0')) % (10**9 + 7)

```




# 1514. Path with Maximum Probability
``` python
def maxProbability(self, n: int, edges: List[List[int]], succProb: List[float], start: int, end: int) -> float:
    p, g = [0.0] * n, defaultdict(list)
    for index, (a, b) in enumerate(edges):
        g[a].append((b, index))
        g[b].append((a, index))
    p[start] = 1.0
    heap = [(-p[start], start)]    
    while heap:
        prob, cur = heapq.heappop(heap)
        if cur == end:
            return -prob
        for neighbor, index in g.get(cur, []):
            if -prob * succProb[index] > p[neighbor]:
                p[neighbor] = -prob * succProb[index]
                heapq.heappush(heap, (-p[neighbor], neighbor))
    return 0.0
```
