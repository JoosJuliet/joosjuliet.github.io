---
layout: post
section-type: post
title: "[leet_code] 1130. Minimum Cost Tree From Leaf Values with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/


# 목표:
- 부모노드는 자식 노드 들 중에 가장 큰 수의 곱으로 만들어진다.
- 그 곱들의 합 중에 가장 작은 수를 구하라

# 조건:
- 2 <= arr.length <= 40
- 1 <= arr[i] <= 15
- It is guaranteed that the answer fits into a 32-bit signed integer (ie. it is less than 2^31)
# solution 설명 :
- 다 해보는 것이다.

Input: [5, 2, 3, 4, 6]  
1st step -> get value [5, 2] = 10 / [2, 3] = 6 / [3, 4] = 12 / [4, 6] = 24  
dp[0, 1] = 10 / dp[1, 2] = 6/ dp[2, 3] = 12 / dp[3, 4] = 24  
2nd step -> calculate [5, 2, 3] / [2, 3, 4] / [3, 4, 6]  
dp[0, 2] = Min(dp[0, 1] + Max[0, 1] * arr[2], dp[1, 2] + Max[1, 2] * arr[0]);  
dp[1, 3] = ..  
dp[2, 4] = ..  
3rd -> [5, 2, 3, 4] / [ 2, 3, 4, 6]  
dp[0, 3] = ..  
dp[1, 4] = ..  

알고리즘 출처:https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/discuss/381340/JAVA-DP-solution


``` python
def get_max(arr, i, j):
    max_num = arr[i]
    # i부터 j까지 중에서 가장 큰 수
    while i<=j:
        max_num = max(arr[i], max_num)
        i +=1
    return max_num


def mctFromLeafValues(arr):
    x = len(arr)
    dp = [[0]*x for _ in range(x)]

    for Len in range(1, x):
        for l in range(0, x-Len):
            r = l+Len
            # 길이 별로 지금 만들고 나누는 것이다.
            if Len == 1:
                dp[l][r] = arr[l]*arr[r]
            else:
                for k in range(l, r):
                    if dp[l][r] == 0:
                        # 값 없으면
                        dp[l][r] = dp[l][k] + dp[k+1][r] + get_max(arr, l, k) * get_max(arr, k+1, r)
                        # get_max(arr, l, k) * get_max(arr, k+1, r) 이건 해당 길이의 루트 노드의 값을 알려주는 것이다.
                        # 값 넣기
                    else:
                        dp[l][r] = min(dp[l][r], dp[l][k] + dp[k + 1][r] + get_max(arr, l, k) * get_max(arr, k + 1, r))
                        # 더 작은 값 넣기
    return dp[0][x - 1]
```
