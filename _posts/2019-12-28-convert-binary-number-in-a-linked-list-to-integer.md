---
layout: post
section-type: post
title: "[leet_code] 1290. Convert Binary Number in a Linked List to Integer with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/contest/weekly-contest-167/problems/convert-binary-number-in-a-linked-list-to-integer/


``` python
def getDecimalValue(self, head: ListNode) -> int:
    ans = 0
    while head != None:
        ans = 2*ans + head.val
        head = head.next
    return ans
```
