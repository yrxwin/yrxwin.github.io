---
title: '[Leetcode 105] Construct Binary Tree from Preorder and Inorder Traversal'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-04 19:07:57
tags:
keywords:
description:
---

#### 原题说明
Given preorder and inorder traversal of a tree, construct the binary tree.

*Note*:
You may assume that duplicates do not exist in the tree.

For example, given

	preorder = [3,9,20,15,7]
	inorder = [9,3,15,20,7]


Return the following binary tree:

       3
      / \
     9   20
        /  \
       15   7


#### 解题思路
题目给出二叉树的前序遍历与中序遍历数列，要求重新构建原二叉树，返回根节点。

首先我们需要明确：

- 前序遍历的顺序：中、左、右
- 中序遍历的顺序：左、中、右


因此，我们知道前序遍历序列的第一个元素是原二叉树的根节点，而此根节点将中序遍历序列分为了左子树的中序遍历序列与右子树的中序遍历序列。

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
    # @param preorder, a list of integers
    # @param inorder, a list of integers
    # @return a tree node
    def buildTree(self, inorder, postorder):
        """
        :type inorder: List[int]
        :type postorder: List[int]
        :rtype: TreeNode
        """
        if not preorder or not inorder:
            return None        
        root = TreeNode(preorder.pop(0))
        inorderIndex = inorder.index(root.val)
        #先左后右，和前序遍历方向相同。可以对比使用中序与后序遍历时构建二叉树的不同
        root.left = self.buildTree(preorder, inorder[:index])
        root.right = self.buildTree(preorder, inorder[index+1:])
        return root
```

#### 复杂度分析
每个节点重构会被访问一次，同时查找index需要O(n)。同时这里并不需要额外空间。所以复杂度分析为

- 时间复杂度: `O(n^2)`
- 空间复杂度: `O(1)`

#### 归纳总结
此题要求重构二叉树，因此需要理解清楚中序遍历与后序遍历的定义。合理使用递归方法即可完成解题。

大家可以结合利用中序遍历与后序遍历构建二叉树这题，更好的理解问题：

[[LeetCode 106] Construct Binary Tree from Inorder and Postorder Traversal](/Leetcode-106-Construct-Binary-Tree-from-Inorder-and-Postorder-Traversal)

大家可以在 [Tree Tag](/tags/Tree) 中找到更多和树有关的内容。种香蕉树去了^_^