---
layout: post
section-type: post
title: "[ leet_code ] [weekly-contest-208 solution] 1598. Crawler Log Folder, 1599. Maximum Profit of Operating a Centennial Wheel with python3"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---

# 1598. Crawler Log Folder

``` python
def min_operations(logs: List[str]) -> int:
  depth = 0
  for log in logs:
    depth += ((-1 if depth != 0 else 0) if (log == '../') else (0 if log == './' else 1))
  return depth

```

``` python
stack = []

for log in logs:
    if log == '../':
        x = stack.pop() if stack else 0
    elif log == './':
        continue
    elif log[-1] == '/':
        x = log.split('/')
        stack.append(x)

return len(stack)
```

# 1599. Maximum Profit of Operating a Centennial Wheel
문제 : https://leetcode.com/contest/weekly-contest-208/problems/maximum-profit-of-operating-a-centennial-wheel/

``` python
#         O(N) , N is customers.length

class Solution:
    def minOperationsMaxProfit(self, customers: List[int], boarding_cost: int, running_cost: int) -> int:
        remain_member = 0
        result = 0
        ans = 0
        for i in range(0, len(customers)):
            if (customers[i]+remain_member) >= 4:
                remain_member = customers[i]+remain_member - 4
                member = 4
            else:
                member = customers[i]+remain_member
                remain_member = 0

            if result <= member*boarding_cost - running_cost*(i+1):
                result = member*boarding_cost - running_cost*(i+1)
                ans = i


        if result < 0:
            return -1
        return ans
```
