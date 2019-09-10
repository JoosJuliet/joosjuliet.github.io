---
layout: post
section-type: post
title: "[leet_code] 222. Count Complete Tree Nodes with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/count-complete-tree-nodes/

# Aim:
- count the number of nodes

# solution :
- get the all of the direction's height(right, left)
- when they are equal 2^height -1
- when they are not equal, recursively get all of of nodes from left&right sub-trees

![Picture_that_tells_how_to_solve](images/2019-08-17-count-complete-tree-nodes/count_nodes.png)
``` java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }
        if (root.left == null && root.right == null) {
            return 1;
        }

        TreeNode left = root;
        int leftDepth = 0;
        while (left != null) {
            leftDepth++;
            left = left.left;
        }

        TreeNode right = root;
        int rightDepth = 0;
        while (right != null) {
            rightDepth++;
            right = right.right;
        }

        if (leftDepth == rightDepth) {
            return (1 << leftDepth) - 1; //same to Math.pow(2, leftDepth)
        } else {
            return 1 + countNodes(root.left) + countNodes(root.right); // root + count of left nodes+  count of right nodes
        }
    }
}
```


---
Reference and image Source:  
https://www.programcreek.com/2014/06/leetcode-count-complete-tree-nodes-java/
