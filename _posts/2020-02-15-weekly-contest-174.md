---
layout: post
section-type: post
title: "[ leet_code ] [weekly-contest-174 solution] The K Weakest Rows in a Matrix, Reduce Array Size to The Half, Maximum Product of Splitted Binary Tree, Jump Game V"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---

# 1. The K Weakest Rows in a Matrix

``` python
import heapq
def kWeakestRows(mat, k: int):
    return [j[1] for j in heapq.nsmallest(k, ((sum(v), i) for i, v in enumerate(mat)))]
```

# 2. Reduce Array Size to The Half

``` python
from collections import Counter
import itertools
def minSetSize(arr):
    return [x[0]+1 for x in enumerate(itertools.accumulate(sorted(collections.Counter(arr).values(), reverse = True))) if (x[1] >= len(arr)//2)]
```

# 3. Maximum Product of Splitted Binary Tree
그래프 탐색하면서 자식 노드들이 가진 합과 자신의 값의 합을 저장한다.
``` python
class Solution:
    def maxProduct(self, root: TreeNode) -> int:
        def dfs(node) :
            ret = node.val
            if node.left :
                ret += dfs(node.left)
            if node.right :
                ret += dfs(node.right)
            post_ordered_sums.append(ret)
            return ret

        post_ordered_sums = []
        dfs(root)

        ret = 0
        for a in post_ordered_sums :
            ret = max(ret, a * (post_ordered_sums[-1] - a))

        return ret % (10 ** 9 + 7)
```

# 4.  Jump Game V
``` python
from functools import lru_cache

def maxJumps(arr, d: int) -> int:
    n = len(arr)

    # 특정 edge에서 갈 수 있는 노드들의 집합을 찾는다.
    edges = [[] for i in range(n)]
    for i in range(n) :
        for j in range(i+1, i + d + 1) :
            if j >= n or arr[j] >= arr[i] :
                break
            edges[i].append(j)
        for j in range(i-1, i - d - 1, -1) :
            if j < 0 or arr[j] >= arr[i] :
                break
            edges[i].append(j)
    # edge는 해당 노드에서 갈 수 있는 node들의 리스트
    @lru_cache(None)
    def dfs(cur) :
        # (자동 memoization)cur의 값이 들어왔을 때의 return값을 lru_cache에 저장해 놓는다.
        ret = 1
        for nxt in edges[cur] :
            ret = max(ret, dfs(nxt) + 1)
            # 갈 수 있는 루트 중 가장 긴 루트를 return한다.
        return ret

    ret = 0
    for i in range(n):
        ret = max(ret, dfs(i))
    return ret
```
