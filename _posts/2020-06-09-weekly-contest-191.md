---
layout: post
section-type: post
title: "[leet_code] Weekly Contest 191 in Maximum Product of Two Elements in an Array and Maximum Area of a Piece of Cake After Horizontal and Vertical Cuts with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---


# 1464. Maximum Product of Two Elements in an Array
문제 : https://leetcode.com/contest/weekly-contest-191/problems/maximum-product-of-two-elements-in-an-array/


``` python
def maxProduct(nums: List[int]) -> int:
    nums.sort()
    return (nums[-1]-1) * (nums[-2]-1)
```


# 1465. Maximum Area of a Piece of Cake After Horizontal and Vertical Cuts
문제 : https://leetcode.com/contest/weekly-contest-191/problems/maximum-area-of-a-piece-of-cake-after-horizontal-and-vertical-cuts/


``` python
def maxArea(h: int, w: int, horizontal_cuts: List[int], vertical_cuts: List[int]) -> int:
    horizontal_cuts.sort()
    vertical_cuts.sort()

    prev = 0
    hor = 0
    for i in horizontal_cuts:
        hor = max(hor, i-prev)
        prev = i
    hor = max(hor, h-prev)

    prev = 0
    ver = 0
    for i in vertical_cuts:
        ver = max(ver, i-prev)
        prev = i
    ver = max(ver, w-prev)

    return (hor*ver)% 1000000007
```

# 1466. Reorder Routes to Make All Paths Lead to the City Zero

문제 : https://leetcode.com/contest/weekly-contest-191/problems/reorder-routes-to-make-all-paths-lead-to-the-city-zero/
``` python
def minReorder(n: int, connections: List[List[int]]) -> int:
    connections.sort(key=lambda i: (i[0], i[1]))

    path = {0}
    count = 0

    for start, end in connections:
        if start in path and end not in path:
            path.add(end)
            count += 1
        elif end in path and start not in path:
            path.add(start)

    return count
```
