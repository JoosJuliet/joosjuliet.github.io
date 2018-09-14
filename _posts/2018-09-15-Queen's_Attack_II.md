---
layout: post
section-type: post
title: "[hacker_rank] Queen's Attack II with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank' ]
comments: true
---

문제:
https://www.hackerrank.com/challenges/queens-attack-2/problem

``` python

n, k = map(int, input().strip().split())
rQueen,cQueen = map(int, input().strip().split())
ObList = []
for _ in range(k):
    rObstacle,cObstacle = map(int, input().strip().split())
    ObList.append((rObstacle,cObstacle))
ObSet = set(ObList)
# print(ObSet)
Delta = [(0,1),(1,1),(1,0),(0,-1),(-1,-1),(-1,0),(1,-1),(-1,1)]
Count = 0
for shift in Delta:
    # print(shift[0], shift[1])
    Pos = (rQueen,cQueen)
    #
    while Pos[0] + shift[0] >=1 and Pos[0] + shift[0] <= n and Pos[1] + shift[1] >=1 and Pos[1] + shift[1] <= n:
        Pos = (Pos[0]+shift[0],Pos[1]+shift[1])
        if Pos in ObSet:
            break
        Count += 1
print(Count)
```
