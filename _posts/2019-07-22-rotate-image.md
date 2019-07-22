---
layout: post
section-type: post
title: "[leet_code]  Rotate Image with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/rotate-image/

# 목표:
- matrix를 90 도 돌린다.
# 조건:
- 공간복잡도 최소화한다.
# solution 설명 :
- 일단 기본적으로 어렵다... 너무 어려워서 생각도 못했고 답보고 했따.
- ~~답을 보고도 몰랐다 사실~~

답을 내는 방법은 두가지인데...
- 첫번째 방법은 https://www.youtube.com/watch?v=Jtu6dJ0Cb94&feature=youtu.be 이 알려준다.
  - 한번에 90도를 돌린다.
- 두번째 방법은
  - 참고문헌 : https://leetcode.com/problems/rotate-image/discuss/18872/A-common-method-to-rotate-the-image
  - first reverse up to down, then swap the symmetry


``` python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        matrix.reverse()
        for i in range(len(matrix)):
            for j in range(i):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
```
