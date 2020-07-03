---
layout: post
section-type: post
title: "[ leet_code ] [weekly-contest-194 solution] XOR Operation in an Array, Making File Names Unique"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---

문제 : https://leetcode.com/contest/weekly-contest-194  


# 1. XOR Operation in an Array

``` python
from functools import reduce
def xorOperation(n: int, start: int) -> int:
    return reduce(lambda a, b: a^b, [start + i * 2 for i in range(n)])
```

# 2. Making File Names Unique

``` python
from collections import defaultdict

def getFolderNames(names: List[str]) -> List[str]:
    counted = {}
    ans =[]
    for name in names:
        new_name = name
        while new_name in counted:
            new_name = name + f"({counted[name]})"
            counted[name] += 1

        ans.append(new_name)
        counted[new_name] = 1

    return ans
```
