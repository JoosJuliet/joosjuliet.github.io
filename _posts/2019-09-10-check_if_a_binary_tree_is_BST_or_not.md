---
layout: post
section-type: post
title: "BST(binary search tree)란? 이진 트리가 BST인지 확인하는 법은?"
category: Spring
tags: [ 'binary_search_tree', 'BST' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

# BST란?
![bst](/images/2019-09-10-check_if_a_binary_tree_is_BST_or_not/binary-search-tree.png)




A binary search tree (BST) is a node based binary tree data structure which has the following properties.
• The left subtree of a node contains only nodes with keys less than the node’s key.
• The right subtree of a node contains only nodes with keys greater than the node’s key.
• Both the left and right subtrees must also be binary search trees.

From the above properties it naturally follows that:
• Each node (item in the tree) has a distinct key.


이진 검색 트리 (BST)는 다음과 같은 속성을 갖는 노드 기반 이진 트리 데이터 구조입니다.
• 노드의 왼쪽 하위 트리에는 키가 노드 키보다 작은 노드 만 포함됩니다.
• 노드의 오른쪽 하위 트리에는 키가 노드 키보다 큰 노드 만 포함됩니다.
• 왼쪽 및 오른쪽 하위 트리는 모두 이진 검색 트리 여야합니다.

위의 속성에서 자연스럽게 다음을 따릅니다.
• 각 노드 (트리의 항목)에는 고유 키가 있습니다.


# 비효율적 방법
각 노드에 대해 왼쪽 하위 트리의 최대 값이 노드보다 작고 오른쪽 하위 트리의 최소값이 노드보다 큰지 확인하십시오.


``` java
/* Returns true if a binary tree is a binary search tree */
int isBST(struct node* node){
  if (node == NULL)
  	return(true);

  /* false if the max of the left is > than us */
  if (node->left!=NULL && maxValue(node->left) > node->data)
  	return(false);

  /* false if the min of the right is <= than us */
  if (node->right!=NULL && minValue(node->right) < node->data)
  	return(false);

  /* false if, recursively, the left or right is not a BST */
  if (!isBST(node->left) || !isBST(node->right))
  	return(false);

  /* passing all that, it's a BST */
  return(true);
}

```

# 효과적인 METHOD :
위의 방법 2는 트리의 일부를 여러 번 통과하기 때문에 느리게 실행됩니다.
더 나은 솔루션은 각 노드를 한 번만 봅니다.
트릭은 유틸리티 도우미 함수 isBSTUtil (struct node * node, int min, int max)을 작성하여 각 노드를 한 번만 보면서
축소되는 최소값과 최대 허용 값을 추적하는 트리를 따라 이동합니다.

min 및 max의 초기 값은 INT_MIN 및 INT_MAX 여야합니다.

아래는 위의 접근 방식의 구현입니다.


---
출처:  
https://www.geeksforgeeks.org/a-program-to-check-if-a-binary-tree-is-bst-or-not/  

bst의 사진출처:

https://muckycode.blogspot.com/2015/01/binary-search-treebst.html  
