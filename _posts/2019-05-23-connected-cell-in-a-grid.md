---
layout: post
section-type: post
title: "[hacker_rank] Connected Cells in a Grid with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

문제 : https://www.hackerrank.com/challenges/connected-cell-in-a-grid/problem

# 목표:
- 1이 밀집된 곳에서 1의 개수를 다 더한다.

# 조건:
- constraint가 강하지 않아서 시간복잡도에 자유로운 편이다.

# solution 설명 :
1. 돌아다니다가 1을 만나면 dfs로 들어간다.
2. 이미 간 곳은 1을 0으로 바꿔서 또 가지 않는다.
3. 근처에 있는 값들을 모두 판별했을 때 cnt를 return한다.
  - 만약 그 근처값들의 근처에 1이 있으면 recursive로 들어가서 확인후 그 값들을 다 더한다.


``` python
def dfs(r, c, maze):
    if r >= len(maze) or r < 0 or c >= len(maze[0]) or c < 0 or maze[r][c] == 0:
        return 0

    maze[r][c] = 0

    cnt = 1
    ds = [[1, 0], [-1, 0], [0, 1], [0, -1], [-1, 1], [1, -1], [1, 1], [-1, -1]]
    # 사방면으로 다 가야한다.
    for d in ds:
        cnt += dfs(r+d[0], c+d[1], maze)
    return cnt

def start():
    n, m = int(input()), int(input())
    maze = [list(map(int, input().split())) for _ in range(n)]

    ans = []
    for r in range(n):
        for c in range(m):
            if maze[r][c] == 1:
                ans.append(dfs(r, c, maze))

    return max(ans)

print(start())


```
