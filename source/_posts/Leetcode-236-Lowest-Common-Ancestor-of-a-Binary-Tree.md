---
title: '[Leetcode 236] Lowest Common Ancestor of a Binary Tree'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-09 11:23:12
tags: [Tree]
keywords: [Tree]
description:
---
#### 原题说明

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we **allow a node to be a descendant of itself**).”

          _______3______
         /              \
      ___5__          ___1__
     /      \        /      \
    6       _2       0       8
            /  \
           7   4
         
For example, the lowest common ancestor (LCA) of nodes `5` and `1` is `3`. Another example is LCA of nodes `5` and `4` is `5`, since a node can be a descendant of itself according to the LCA definition.

#### 解题思路
本题要求找出两个节点的最近的共同祖先。

一个简单的思路是我们可以遍历整棵树，然后用一个`map`记录每个节点的父节点。这样可以找出节点`p`和`q`到根节点的`path`,然后就能方便的找出最近的共同祖先。但是这样要求我们用额外的`map`来记录每个节点的信息，空间复杂度为O(n)。

换一个思路，我们发现：假设对于一个节点，如果它的右子树里只找到了其中一个目标节点，而在它的左子树中没有找到另一个目标节点；或者它的左子树里只有一个目标节点，而它的右子树里没有另外一个目标界节点，那么当前节点就不是两个目标节点的最近公共祖先了。除此之外的情况，当前节点就是两个目标节点的公共祖先了。 我们可以从叶子节点向上，标记子树中出现目标节点的情况。若一个节点的左右子树都有标记，则当前节点就是共同祖先。

我们用递归的方法实现代码，会非常简洁。

#### 示例代码 (python)
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        if not root or root == p or root == q:
            return root
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        if left and right:
            return root
        return left if left else right
```

#### 复杂度分析
最坏情况每个节点visit一次，因此时间复杂度为`O(n）`。
时间复杂度: `O(n)`
空间复杂度: `O(1)`

#### 归纳总结
思考清楚共同祖先的定义，我们用递归的方法实现代码。同时我们可以看出，这题本质上还是对 [Tree](/tags/Tree) 遍历的变种。

好了，几天就和大家讨论到这里，种香蕉树去了。