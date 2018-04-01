---
title: '[Leetcode 145] Binary Tree Postorder Traversal'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-03-30 18:53:08
tags: [Stack, Tree]
---

#### 原题说明
Given a binary tree, return the *postorder* traversal of its nodes' values.

For example:

Given binary tree [1,null,2,3],
   
    1   
     \
	  2
	 /
    3
   
return [3,2,1]. 

**Note**: Recursive solution is trivial, could you do it iteratively?

#### 解题思路
深度遍历二叉树（`DFS`），可以分为

 - 前序遍历（`preorder`）
 - 中序遍历（`inorder`）
 - 后序遍历（`postorder`）

这题要求使用后序遍历。后序遍历按照左子节点（`left`），右子节点（`right`），根节点（`root`）的顺序深度遍历二叉树。

同样，我们可以使用递归与非递归两种方法来实现前序遍历。递归的方法还是比较简单，参看相关代码就能明白。后序遍历的非递归的方法相比前序遍历与中序遍历而言，相对比较复杂，每个根节点我们都要visit两次，逻辑上需要大家仔细思考。

我们依然可以通过栈（`stack`）实现，总体思想为方位左子节点，直到其为空，同时将访问过得节点和其右子节点存入栈中。当退回是需要判断节点的右子节点是否为空， 从而可以确定是否访问该节点还是访问该节点的右子节点：

使用栈（`stack`），每次visit当前节点`node`，同时如果当前节点的右子节点非空，将此右子节点存入栈中。然后将当前节点`node`压入栈中，并将当前节点更新为其左子节点，知道当前节点`node`为空。

之后当栈非空，如果栈顶元素的右子节点不等于该元素退栈后的栈顶元素，则将栈顶元素存入答案数组，退栈，并将当前节点`node`设为空。反之，交换栈顶的两个节点，并将当前节点设为栈顶元素，并退栈。

重复上述两个步骤，直到遍历完整棵二叉树。具体流程为：

1. 建立一个空栈`stack`

2. 如果当前节点`node`非空或者栈`stack`非空：
	
	- 2.1 如果当前节点`node`非空：
	    - 如果当前节点的右子节点非空：将右子节点存入栈中
	    - 将当前节点`node`压入栈
	    - 更新当前节点`node`为它的左子节点，回到步骤2.1
	
	- 2.2 如果栈非空:
        - 将当前节点`node`设为栈顶元素并退栈
	    - 如果栈非空并且栈顶元素等于当前节点的右子节点：
	  交换当前节点和栈顶元素。 反之访问并将当前节点`node`存入答案数组`ans`, 并将当前节点设为空
	    - 回到步骤2



#### 示例代码 （递归 python版）

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class Solution:
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        def postorderhelper(root, ans):
            if root:
                postorderhelper(root.left, ans)
            else:
                return
            postorderhelper(root.right, ans)
            ans.append(root.val)
        ans = []
        postorderhelper(root, ans)
        return ans
```

#### 示例代码 （非递归 python版）

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class Solution:
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        cur = root
        stack = collections.deque()
        ans = []
        while(cur or stack):
            while cur:
                if cur.right:
                    stack.append(cur.right)
                stack.append(cur)
                cur = cur.left
            if stack:
                cur = stack.pop()
                if stack and cur.right == stack[-1]:
                    tmp = stack.pop()
                    stack.append(cur)
                    cur = tmp
                else:
                    ans.append(cur.val)
                    cur = None
        return ans
```
#### 复杂度分析
无论递归还是非递归，它们的时间复杂度与空间复杂度都是一样的。每个节点都被访问一次或者两次，同时栈的深度为O(log n)。所以复杂度分析为：

- 时间复杂度：O(n)
- 空间复杂度：O(log n)

#### 总结归纳：
今天我们讲了二叉树的后序遍历，结合之前我们介绍的前序遍历、中序遍历，希望能对感兴趣的朋友有所帮助。

后序遍历的非递归实现相对前序遍历、中序遍历而言复杂一点，但只要逻辑上清晰，严格按照后序遍历的定义去做，也不难实现。

相关的练习还有：

[[LeetCode 144] Binary Tree Preorder Traversal 二叉树前序遍历](/Leetcode-144-Binary-Tree-Preorder-Traversal)

[[LeetCode 94] Binary Tree Inorder Traversal 二叉树中序遍历](/Leetcode-94-Binary-Tree-Inorder-Traversal)

[[LeetCode 102] Binary Tree Level Order Traversal 二叉树层序遍历](/Leetcode-102-Binary-Tree-Level-Order-Traversal)


之后我们会继续讨论更多Tree相关的内容,并更新在 [Tree Tag](/tags/Tree)，尽请期待，种香蕉树去了：）