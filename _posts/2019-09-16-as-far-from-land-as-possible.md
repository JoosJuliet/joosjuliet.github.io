---
layout: post
section-type: post
title: "[leet_code] 1162. As Far from Land as Possible with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/as-far-from-land-as-possible/

# 목표:
- 0에서 1까지의 거리가 최대가 되도록 한다.

# 조건
- 1 <= grid.length == grid[0].length <= 100
- grid[i][j] is 0 or 1


# solution:
- ![solution](/images/2019-09-16-as-far-from-land-as-possible/photo.png)
- 이 방법으로 풀었다. bfs를 활용한 풀이다.
- 일단 1인 것을 전부 q에 넣고 그 곳 근처에 있는 값들을 하나씩 표식을 한다.
- 그렇게 서서히 퍼질 때 마다 그 길이를 ans에 저장을 한다.

```python


class Solution:
    def maxDistance(self, grid: List[List[int]]) -> int:
        n = len(grid)
        q = [[i, j] for i in range(n) for j in range(n) if grid[i][j]] #1인 것 다 뽑아낸다.
        if n **2 == len(q) : return -1
        ans = -1
        while len(q) != 0 :
            deque = []
            for i, j in q:
                for x, y in (i - 1, j), (i + 1, j), (i, j - 1), (i, j + 1):
                    if 0 <= x < n and 0 <= y < n and not grid[x][y]:
                        grid[x][y] = 1 # 갔다 온 것 표시
                        deque.append([x, y]) #1의 근처인 것 다시 deque에 집어넣는다.
            q = deque
            ans += 1 # 긴 것은 이걸로 또 체크를 하고 있지
        return ans

```

---
사진 출처 : https://leetcode.com/problems/as-far-from-land-as-possible/discuss/364722/BFS-python-two-different-approaches-explained-commented-and-visualized
