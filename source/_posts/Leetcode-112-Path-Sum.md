---
title: '[Leetcode 112] Path Sum'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-03 11:52:28
tags: [Tree, Depth-first Search, Microsoft]
keywords: [Tree, Depth-first Search]
description:
---

#### 原题说明
Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

For example:
Given the below binary tree and sum = 22,

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

#### 解题思路
本题给出一个数`sum`，要求判断二叉树中是否存在一条从根到叶`root-to-leaf`的路径，使得路径上数值的和等于`sum`。

事实上，如果存在这样一条路径，那么对于根节点的两个可能的子节点`left`和`right`, 两个中至少存在一条路径，使得从子节点`left`或者`right`到叶的路径的数值的和等于`sum - root.val`。以此类推，子节点的子节点亦是如此。

因此，我们自然想到利用递归，深度搜索的方法来解决此题。当搜索到叶节点时，如果叶节点的值`val`等于当时的`sum`,则找到了这样一条路径。

#### 示例代码 （python）

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        if not root:
            return False
        if not root.left and not root.right: #当搜索到叶节点时
            return root.val == sum
        return self.hasPathSum(root.left, sum-root.val) or self.hasPathSum(root.right, sum-root.val)
```

#### 复杂度分析
使用深度搜索`DFS`,每个节点被访问一次。并且递归过程中，栈的最大深度为O(n)。考虑到本题并非平衡二叉树，最差将退化成链表，而大O代表复杂度的上阈值，因此为O(n)。
 所以复杂度分析为：

- 时间复杂度： `O(n)`
- 空间复杂度：`O(1)`, &#160; 递归栈深度`O(n)` 

#### 总结归纳：
这是一道典型的用递归方法解决的树的问题，采用深度搜索`DFS`的方法也是比较基础。

大家可以在 [Tree Tag](/tags/Tree) 中找到更多和树有关的内容，也可以在 [Depth-first Search tag](/tags/Depth-first-Search) 中查找与深度搜索有关的题目。

不说了，忙着种香蕉树去了：） 