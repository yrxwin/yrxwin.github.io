---
title: '[Leetcode 250] Count Univalue Subtrees'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-03 12:34:50
tags: [Tree]
keywords: [Tree]
description:
---

#### 原题说明
Given a binary tree, count the number of uni-value subtrees.

A Uni-value subtree means all nodes of the subtree have the same value.

For example:
Given binary tree,

              5
             / \
            1   5
           / \   \
          5   5   5
return 4.

#### 解题思路
这题要求求出所有二叉树子树中，元素都相同的子树的个数。给出的例子中，以5为值得子树个数是4个，以1为值得子树个数是0，所以答案是4。

如果一个子树是满足条件的元素相同的子树，那以它的子节点为根的子树也一定是满足条件的元素相同的子树。因此，我们可以从叶子节点从下往上（`bottom-up`）判断。

如果两个以叶子节点为根的子树都是元素相同的子树，并且它们的值与父节点的值相同，则以父节点为根的子树也是满足条件的子树。但是节点没有父节点，无法往上判断，所以可以采用递归的方法从上往下调用判断。

在代码的实现过程中，这里我们用计数器`self.count`记录满足条件的子树个数，用一个辅助函数checkUni帮助我们从下往上查找`UnivalSubTree`

#### 示例代码 （python）
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def countUnivalSubtrees(self, root):
        self.count = 0
        self.checkUni(root)
        return self.count

# If both children are "True" and root.val is equal to both children's values that exist, 
# then root node is uniValue subtree node. 
    def checkUni(self, root):
        if not root:
            return True
        l, r = self.checkUni(root.left), self.checkUni(root.right)
        if l and r and (not root.left or root.left.val == root.val) and \
        (not root.right or root.right.val == root.val):
            self.count += 1
            return True
        return False
```

#### 复杂度分析
使用深度搜索`DFS`,每个节点被访问一次。并且递归过程中，栈的最大深度为O(n)。考虑到本题并非平衡二叉树，最差将退化成链表，而大O代表复杂度的上阈值，因此为O(n)。

- 时间复杂度 O(n)
- 空间复杂度 O(n)

#### 归纳总结：
递归方法解决树的问题。关键在于想明白父节点与子节点之间的关系。这里一个小点值得提醒，我们把空的节点判断为`True`, 这样方便于之后的计算。

大家可以在 [Tree Tag](/tags/Tree) 中找到更多和树有关的内容，在 [Depth-first Search Tag](/tags/Depth-first-Search) 中找到更多和深度搜索相关的问题。

要种香蕉树去了：）