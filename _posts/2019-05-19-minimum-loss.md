---
layout: post
section-type: post
title: "[hacker_rank] Minimum Loss with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

문제 : https://www.hackerrank.com/challenges/minimum-loss/problem

# 목표:
- ordering된 두 수 간의 격차가 최소여야 한다.

# 조건:
- 앞에 있는 수가 더 커야한다.
- 답이 없는 경우는 없다.
- Big O가 logN, N, NlogN 이어야한다.

# solution 설명 :
- O(NlogN)
- price로 sort한 후 index 조건을 맞춘다.




``` python
n = int(input())
difference = []
prices = sorted(enumerate(map(int, input().split())), key=lambda t: t[1])

prev = [0, -1]
# 절대 젤 앞에 것이 문제가 되지 않게 하기 위한 것
for price in prices:
    if prev[0] > price[0] :
        difference.append(price[1] - prev[1])
    prev = price

print(min(difference))
```
