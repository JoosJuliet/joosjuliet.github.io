---
layout: post
section-type: post
title: "[hacker_rank] Cut the Tree with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

문제 : https://www.hackerrank.com/challenges/cut-the-tree/problem

# 목표:
- vertex를 중간을 끊어서 나누자.

# 조건:
- constraint가 강하지 않아서 시간복잡도에 자유로운 편이다.

# solution 설명 :
1. vertex를 차례로 하나씩 끊으면서 길을 간다.
2. 어차피 길이 한 붓 그리기가 아니기 때문에 끊고 바로 visited 를 False로 하면 끊긴 곳이 아닌곳을 갈 걱정을 안해도 된다.
3. 그렇게 끊긴 부분부터 쭉 다 더하고 차이를 계산한다.

``` python
import sys

ans = sys.maxsize

sys.setrecursionlimit(int(1e6)+1)

def dfs(current_idx, T, chain, v, visited):
    global ans
    if visited[current_idx]:
        return 0
    visited[current_idx] = True

    lower_end = v[current_idx] # 특정 vertex의 값
    for idx in chain[current_idx]:
        # 지금 idx에 연결된 애를 돈다.
        # 이미 처음 시작한 곳은 visited에서 True로 해놨기 때문에 다른 구간은 갈 수가 없다.
        lower_end += dfs(idx, T, chain, v, visited) # 특정 vertex들의 값을 더한 것
    diff = abs(T - 2*lower_end) # (T-lower_end)-lower_end

    if diff < ans: ans = diff
    return lower_end


def start():
    n = int(input())
    v = list(map(int, input().split()))
    T = sum(v)
    visited = [False]*n

    chain = [set() for _ in range(n)]

    for _ in range(n-1):
        i, j = map(int, input().split())
        chain[i-1].add(j-1)
        chain[j-1].add(i-1)

    dfs(0, T, chain, v, visited)
    print(ans)

start()



```
