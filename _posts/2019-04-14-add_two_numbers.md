---
layout: post
section-type: post
title: "[hacker_rank]Add Two Numbers with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---

문제 :
https://leetcode.com/problems/add-two-numbers/

# website ver
``` python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        if l1 is None:
            return l2
        if l2 is None:
            return l1
        first_node = ListNode(None)
        previous_node = first_node
        carry_over = 0
        while l1 or l2 or carry_over:
            num = self.get_digit_from_listnode(l1) + self.get_digit_from_listnode(l2) + carry_over
            digit = num % 10
            carry_over = num // 10
            listnode = ListNode(digit)
            previous_node.next = listnode
            previous_node = listnode
            l1 = self.get_next_node(l1)
            l2 = self.get_next_node(l2)
        first_node = first_node.next
        return first_node

    def get_digit_from_listnode(self, listnode):
        return listnode.val if listnode else 0

    def get_next_node(self, listnode):
        return listnode.next if listnode else None
```

# ide ver
``` python
import sys
lst = [list(map(int, input().split())) for _ in range(6)]
high_score = -sys.maxsize -1
for x in range(1, 5):
    for y in range(1, 5):
        high_score = max(high_score, sum(lst[x-1][y-1:y+2]) + lst[x][y] + sum(lst[x+1][y-1:y+2]))
print(high_score)
```
