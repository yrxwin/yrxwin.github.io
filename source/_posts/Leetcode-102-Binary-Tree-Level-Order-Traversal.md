---
title: '[Leetcode 102] Binary Tree Level Order Traversal'
categories:
  - leetcode
author: '大猩猩'
date: 2018-03-31 15:24:33
tags: [Stack, Tree]
keywords:
description:
---

#### 原题说明
Given a binary tree, return the *level order* of its nodes' values. (ie, from left to right, level by level).

For example:

Given binary tree `[3,9,20,null,null,15,7]`,
   
      3   
     / \
    9  20
	   / \
      15  7
   
return its level order traversal as:

    [
     [3],
     [9,20],
     [15,7]
    ]

#### 解题思路
本题要求层序遍历一个二叉树，与普通的广度遍历（`Breadth First Search`）稍有不同的是，需要按层分开。所以我们需要判断当前层的遍历是否结束。我们使用队`queue`来实现遍历，具体思路为：

1. 	建立一个队`q`,并将当前节点`cur`存入队中：
2.	当前层的长度由变量`count`记录 
3.	如果队`q`非空：
	- 2.1 建立一个空列`tmplevel`存放下一层的节点
	- 2.2 如果`count`非零：
	    - 当前节点`cur`更新为退队节点
	    - 将当前节点`cur`的值存入列`tmplevel`中
	    - count减1
	    - 如果当前节点`cur`的左子节点非空，存入队`q`
	    - 如果当前节点`cur`的右子节点非空，存入队`q`
	    - 回到步骤2.2
	- 2.3 将列`tmplevel`存入答案列`ans`
	- 2.4 更新count为当前队列`q`长度
4. 返回`ans`

算法过程中，我们用变量`count`追踪当前层剩余的未访问节点的个数，从而判断何时按层分开。思路还是比较简单的。

#### 示例代码 （python版）

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class Solution:
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root:
            return []
        ans = []
        cur = root
        q = collections.deque([cur])
        count = len(q)
        while q:
            tmplevel = []
            while count:
                cur = q.popleft()
                tmplevel.append(cur.val)
                count -= 1
                if cur.left:
                    q.append(cur.left)
                if cur.right:
                    q.append(cur.right)
            ans.append(tmplevel)
            count = len(q)
        return ans
```

#### 复杂度分析
每个节点被访问一次，因此时间复杂度为`O(n)`。另一方面，队的最大长度为其中最宽的层的节点数，因此空间复杂度仍然为`O(n)`.

- 时间复杂度： `O(n)`
- 空间复杂度： `O(n)`

#### 总结归纳：
层序遍历`level order`也是树遍历的一种方法，结合我们之前讨论过的前序`preorder`、中序`inorder`、后序`postorder`遍历，希望大家能体会它们实现过程中的区别。

层序遍历使用队列`queue`这一数据结构实现，这点和前序`preorder`、中序`inorder`、后序`postorder`遍历是不同的。同时，层序遍历的空间复杂度大于另外三种深度遍历的复杂度，这点也值得我们注意。

好了，今天就和大家讨论到这里，种香蕉树去了
