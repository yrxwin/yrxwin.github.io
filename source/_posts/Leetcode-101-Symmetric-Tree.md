---
title: '[Leetcode 101] Symmetric Tree'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-02 11:20:06
tags: [Tree, Depth-first Search, Microsoft, Bloomberg, LinkedIn]
keywords: [Tree, Depth-first Search]
description:
---

#### 原题说明
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

   
        1   
       / \
      2   2
     / \ / \
    3  4 4  3
   
But the following

        1   
       / \
      2   2
       \   \
       3    3
Note:
Bonus points if you could solve it both recursively and iteratively.

#### 解题思路
本题要求判断二叉树是否对称。简单来说，对一颗二叉树做镜像翻转，如果翻转后的二叉树与原树相同，即可判断为对称，反之则不对称。

我们可以用递归与非递归两种解法来完成这题，但总体思路上就是之前所说的。

在递归方法总是相对简单，我们使用深度搜索`DFS`来实现。用一个辅助函数`helpcheck`来完成对两棵树的同时遍历。这里我们只要对原本该遍历`left`的地方换成`right`,`right`的地方换成`left`,就完成了对镜像树的遍历。

在非递归方法中，我们使用广度搜索`BFS`来实现。使用双端队列来实现。每次从队列头部pop出两棵树的对应节点做判断，节点值不同，则返回*False*；如果满足条件，在把它们对应的左右子节点存入队尾。直到队列为空时，返回*True*



#### 示例代码 （递归 python）

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        return self.helpcheck(root, root)
    def helpcheck(self, left, right):
        if not left and not right:
            return True
        if not left or not right:
            return False
        if left.val != right.val:
            return False
        return self.helpcheck(left.left, right.right) and self.helpcheck(left.right, right.left)  

```
#### 示例代码 （非递归 python）

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

import collections
class Solution:
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root:
            return True
        q = collections.deque()
        q.extend([root,root])
        while q:
            tmpNode1 = q.popleft()
            tmpNode2 = q.popleft()
            if tmpNode1.val != tmpNode2.val:
                return False
            if tmpNode1.left and tmpNode2.right:
                q.extend([tmpNode1.left, tmpNode2.right])
            elif (tmpNode1.left and not tmpNode2.right) or (not tmpNode1.left and tmpNode2.right):
                return False
            if tmpNode1.right and tmpNode2.left:
                q.extend([tmpNode1.right, tmpNode2.left])
            elif (tmpNode1.right and not tmpNode2.left) or (not tmpNode1.right and tmpNode2.left):
                return False
        return True
```

#### 复杂度分析
对递归深度搜索，每个节点被访问一次，因此时间复杂度为`O(n)`。栈最大深度为`O(log n)`。因此其复杂度为：

- 时间复杂度： `O(n)`
- 空间复杂度： `O(1)` 
- 栈的深度：`O(log n)`

对非递归广度搜索，每个节点被访问一次，时间复杂度为`O(n)`。队的最大长度为其中最宽的层的节点数，因此空间复杂度仍然为`O(n)`.

- 时间复杂度： `O(n)`
- 空间复杂度： `O(n)`

#### 总结归纳：
本题想清楚树的对称的定义，便能利用深度搜索`DFS`和广度搜索`BFS`两种树的遍历的方法解题。类似的题目在实现的过程中一般都是利用这两种遍历方法，所以需要大家对树的遍历能够比较熟悉，以便加以利用。

之后我们还会添加一些相关的练习。同时大家可以在[Tree Tag](/tags/Tree) 中找到更多和树有关的内容。种香蕉树去了：）

[[LeetCode 144] Binary Tree Preorder Traversal 二叉树前序遍历](/Leetcode-144-Binary-Tree-Preorder-Traversal)

[[LeetCode 94] Binary Tree Inorder Traversal 二叉树中序遍历](/Leetcode-94-Binary-Tree-Inorder-Traversal)

[[LeetCode 145] Binary Tree Postorder Traversal 二叉树后序遍历](/leetcode-145-Binary-Tree-Postorder-Traversal)
