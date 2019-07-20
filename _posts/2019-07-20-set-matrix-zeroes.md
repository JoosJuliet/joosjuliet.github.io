---
layout: post
section-type: post
title: "[leet_code] Set Matrix Zeroes with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---

문제 : https://leetcode.com/problems/set-matrix-zeroes/
# 목표:
matrix의 값에 0이 있으면 그 곳에 해당되는 행,열을 쫙 다 0으로 만든다.

# 조건:
- 공간복잡도를 최소한으로 써라

# solution 설명 :
- 0이 있는 matrix의 행,열을 set에 넣는다.(시간복잡도를 최소화하기 위해서)
- 그 해당 행,열인 곳인 matrix 위치에 0을 넣는다.


``` python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:

    zero_location_x = set()
    zero_location_y = set()

    for i in range(0, len(matrix)):
        for j in range(0, len(matrix[i])):
            if matrix[i][j] == 0:
                zero_location_x.add(i)
                zero_location_y.add(j)

    for i in range(0, len(matrix)):
        for j in range(0, len(matrix[i])):
            if i in zero_location_x or j in zero_location_y :
                matrix[i][j] = 0
```
