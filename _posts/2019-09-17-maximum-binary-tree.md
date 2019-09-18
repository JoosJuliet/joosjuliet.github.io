---
layout: post
section-type: post
title: "[leet_code] 654. Maximum Binary Tree with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/maximum-binary-tree/


# 목표:
- array에서 가장 큰 수는 root로 만든다.
- 왼쪽 subtree에서 가장 큰 수로 또 왼쪽 tree 만든다.(오른쪽도)
- 문제에 나와있지는 않지만 inorder traversal로 array가 되있다.
- 알고보니 cartesian-tree를 만들라는 것이었다.

# 조건:
- array는 1000개 이하이다.

# solution 설명 :
- nums에서 큰 수를 찾은 후 그 idx기준으로 nums를 다시 쪼갠다.
- 그 쪼개진 것으로 노드에 이어 붙인다.

알고리즘 출처: https://leetcode.com/problems/maximum-binary-tree/solution/ inctrl덧글



``` python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
class Solution:
    def constructMaximumBinaryTree(self, nums: List[int]) -> TreeNode:
        def maxTree(nums):
            idx = nums.index(max(nums))
            node = TreeNode(nums[idx]) # 이 과정에서 node가 계속 달라진다.
            if len(nums[idx+1:]) > 0:
                node.right = maxTree(nums[idx+1:])
            if len(nums[:idx]) > 0:
                node.left = maxTree(nums[:idx])
            return node
        return maxTree(nums)
```
