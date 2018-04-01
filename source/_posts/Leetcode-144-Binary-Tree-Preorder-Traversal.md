---
title: '[Leetcode 144] Binary Tree Preorder Traversal '
categories:
  - leetcode
date: 2018-03-30 02:12:36
tags: [Stack, Tree]
author: 大猩猩

---
#### 原题说明
Given a binary tree, return the preorder traversal of its nodes' values.

For example:

Given binary tree [1,null,2,3],
   
    1   
     \
	  2
	 /
    3
   
return [1,2,3].

#### 解题思路
深度遍历二叉树（`DFS`），可以分为

 - 前序遍历（`preorder`）
 - 中序遍历（`inorder`）
 - 后序遍历（`postorder`）

这题要求使用前序遍历。前序遍历简单是说总是按照根节点（`root`），左子节点（`left`），右子节点（`right`）的顺序深度遍历二叉树。

我们可以使用递归与非递归两种方法来实现前序遍历。递归的方便比较简单，参看相关代码就能明白。这里主要讲一下非递归的方法：

使用栈（`stack`），每次visit当前节点`node`，同时如果当前节点的右子节点非空，将此右子节点存入栈中，再将当前节点`node`更新为当前节点的左子节点。直到遍历完整棵二叉树。具体步骤为：

1. 建立一个空栈`stack`
2. 如果当前节点`node`非空或者栈`stack`非空：
  - 2.1 如果当前节点`node`非空：
    - 访问当前节点`node`
	- 如果当前节点的右子节点非空，压入栈
	- 更新当前节点`node`为它的左子节点，回到步骤2.1 
  - 2.2 如果栈非空，将当前节点更新为栈顶元素，并且退栈，回到步骤2



#### 示例代码 （递归 python版）

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class Solution:
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        ans = []
        self.preorderHelper(root, ans)
        return ans
    
    def preorderHelper(self, root, ans):
        if root:
            ans.append(root.val)
            self.preorderHelper(root.left, ans)
            self.preorderHelper(root.right, ans)
```

#### 示例代码 （非递归 python版）

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class Solution:
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if not root:
            return []
        ans = []
        stack = collections.deque()
        while stack or root:
            while root :
                ans.append(root.val)
                if root.right:
                    stack.append(root.right)
                root = root.left
            if stack:
                root = stack.pop()
        return ans
```
#### 复杂度分析
无论递归还是非递归，它们的时间复杂度与空间复杂度都是一样的。每个节点都被访问一次，同时栈的深度为O(log n)。所以复杂度分析为：

- 时间复杂度：`O(n)`
- 空间复杂度：`O(log n)`

#### 总结归纳：
树的遍历是对树的基本操作之一。今天我们讲了前序遍历。
相关的练习还有：

[[LeetCode 94] Binary Tree Inorder Traversal 二叉树中序遍历](/Leetcode-94-Binary-Tree-Inorder-Traversal)

[[LeetCode 145] Binary Tree Postorder Traversal 二叉树后序遍历](/leetcode-145-Binary-Tree-Postorder-Traversal)

[[LeetCode 102] Binary Tree Level Order Traversal 二叉树层序遍历](/Leetcode-102-Binary-Tree-Level-Order-Traversal)


之后我们会继续讨论更多Tree相关的内容,并更新在 [Tree Tag](/tags/Tree)，尽请期待，种香蕉树去了：）