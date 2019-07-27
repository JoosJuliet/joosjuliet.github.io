---
layout: post
section-type: post
title: "[leet_code] 19. Remove Nth Node From End of List with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/remove-nth-node-from-end-of-list/
# 목표:
- 주어진 index의 node를 제외하고 잇는다.
# 조건:
- ... 없다.

# solution 설명 :
1. 총개수 구한다.
2. 개수에서 n+1개 뺀다.
3. 목표물 바로전에서 위치가 멈춘다.
4. 현재에서 이어야 하는 것은 다음,다음임으로 현제의 next를 통해 받는다.


>ListNode는 print를 해보면 ListNode{val: 1, next: ListNode{val: 2, next: ListNode{val: 3, next: ListNode{val: 4, next: ListNode{val: 5, next: None}}}}} 이런상황이다.

``` python
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        lengthOfList = 0
        tmp = head
        if not tmp.next: return None

        while tmp :
            lengthOfList += 1
            tmp = tmp.next

        n = lengthOfList - n
        if n == 0 :
            return head.next

        tmp = head
        while tmp :
            if n == 1:
                tmp.next = tmp.next.next
            tmp = tmp.next
            n -= 1

        return head
```
