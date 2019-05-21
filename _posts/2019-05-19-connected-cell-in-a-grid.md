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
- 1이 군집된 것들 중 가장 많은 수가 군집 된 것을 찾아서 count 알려주기

# 조건:
- constraints가 넉넉해서 n**2으로도 풀 수 있다.

# solution 설명 :
dfs나 bfs로 풀면 좋을 것 같다.
1.

일단 is_splited_way은 오로지 갈림길인지 확인하고 X를 준다.
그리고 어차피 M의 위치를 아니까 그걸 가지고 한다.
가는길에 갈림길인 곳만 1로 되고 그것이 바로... !
1의 개수가 바로 답이다.


``` python
n = int(input())
m = int(input())

maze = [list(map(int, input().split())) for _ in range(m)]

def count_route(x, y, maze, count):
    if maze[x][y] == 0 :
        return

    if maze[x][y] == 1 :
        count += 1
        maze[x][y] = 'X'

    for i in range(4):
        dx = [0,0,1,-1]
        dy = [1,-1,0,0]
        if x+dx[i] >= 0 and x+dx[i] < n and y+dy[i] >= 0 and y+dy[i] < m:
            if maze[x+dx[i]][y+dy[i]] == 1 or 'X':
                return count_route(x+dx[i], y+dy[i], maze, count)


ans = []
for j in range(m):
    for i in range(n):
        if maze[i][j] == 1 :
            ans.append(count_route(i, j, maze, 0))
print(ans)


```
