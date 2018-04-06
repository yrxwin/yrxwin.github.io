---
title: '[Leetcode 106] Construct Binary Tree from Inorder and Postorder Traversal'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-03 21:25:56
tags: [Array, Tree, Depth-first Search]
keywords: [Array, Tree, Depth-first Search, Inorder Traversal, Postorder Traversal]
description:
---

#### 原题说明
Given inorder and postorder traversal of a tree, construct the binary tree.

*Note*:
You may assume that duplicates do not exist in the tree.

For example, given

    inorder = [9,3,15,20,7]
    postorder = [9,15,7,20,3]

Return the following binary tree:

	    3
       / \
      9   20
     /     \
    15      7

#### 解题思路
题目给出二叉树的中序遍历与后序遍历，要求重新构建原二叉树，返回根节点。

首先我们需要明确：

- 中序遍历的顺序：左、中、右
- 后序遍历的顺序：左、右、中

因此，我们知道后序遍历的最后一个元素是原二叉树的根节点，而此根节点将中序遍历分为了左子树的中序遍历与右子树的中序遍历。

根据以上思路，我们可以继续对左右子树的分别进行递归，直到序列为空，重构整个二叉树。

#### 示例代码 (python)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    def buildTree(self, inorder, postorder):
        """
        :type inorder: List[int]
        :type postorder: List[int]
        :rtype: TreeNode
        """
        dicinorder = {}
        for i, val in enumerate(inorder):
            dicinorder[val] = i
        start, end = 0, len(inorder)
        return self.helper(start, end, postorder, dicinorder)
    
    def helper(self, start, end, postorder, dicinorder):
        if start == end:
            return None
        root = TreeNode(postorder.pop())
        inorderIndex = dicinorder[root.val]
        root.right = self.helper(inorderIndex+1, end, postorder, dicinorder)
        root.left = self.helper(start, inorderIndex, postorder, dicinorder)
        return root
```

#### 复杂度分析
我们使用一个字典记录`inorder`数组中value与对应index的关系，这样能快速查找每个value的index，每次查找时间复杂度为O(1)。
每个节点重构会被访问一次，一共n个节点。同时字典需要空间`O(n)`。所以复杂度分析为

- 时间复杂度: `O(n)`
- 空间复杂度: `O(n)`

#### 归纳总结
此题要求重构二叉树，因此需要理解清楚中序遍历与后序遍历的定义。合理使用递归方法即可完成解题。

大家可以结合利用中序遍历与前序遍历构建二叉树这题，更好的理解问题：

[[LeetCode 105] Construct Binary Tree from Preorder and Inorder Traversal](/Leetcode-105-Construct-Binary-Tree-from-Preorder-and-Inorder-Traversal)

大家可以在 [Tree Tag](/tags/Tree) 中找到更多和树有关的内容。种香蕉树去了^_^
