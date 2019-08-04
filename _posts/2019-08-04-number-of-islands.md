---
layout: post
section-type: post
title: "[leet_code] 200. Number of Islands with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/number-of-islands/


# 목표:
1. 면을 공유하고 있는 "1" 들은 섬이다.
2. 그 섬의 개수를 구하라

# 조건:
릿코드는.. 조건이 없을 때가 많다  

# solution 설명 :
1. dfs로 풀어서 개수를 안다.
2. 메모리를 적게 쓰기 위해 grid에서 왔던 것 체크를 "2"로 한다.


``` python
class Solution:
    def dfs(self, i, j, n, m, grid):
        grid[i][j] = "2" # 왔던 것 체크
        for x, y in zip([0, 0, 1, -1], [1, -1, 0, 0]):
            dx = i + x
            dy = j + y
            if 0 <= dx < n and 0 <= dy < m:
                if grid[dx][dy] == "1":
                    self.dfs(dx, dy, n, m, grid)
        return

    def numIslands(self, grid) -> int:
        if not grid :
            return 0
        n, m = len(grid), len(grid[0])
        count = 0
        for i in range(n):
            for j in range(m):
                if grid[i][j] == "1":
                    self.dfs(i, j, n, m, grid)
                    count += 1
        return count
```
