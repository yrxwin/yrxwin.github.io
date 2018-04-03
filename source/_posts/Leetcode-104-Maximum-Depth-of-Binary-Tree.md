---
title: '[Leetcode 104] Maximum Depth of Binary Tree'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-01 19:19:23
tags: [Tree, Depth-first Search, Uber, LinkedIn, Apple, Yahoo]
keywords: Tree, Depth-first Search
description:
---
#### 原题说明
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

For example:

Given binary tree [3,9,20,null,null,15,7],
   
      3   
     / \
    9  20
	   / \
      15  7
   
return its depth = 3 


#### 解题思路

这题要求我们给出二叉树的最大深度。最大深度是指的从根节点一直到最远的叶节点中所有的节点数目。

因为二叉树有左右两棵，所以二叉树的最大深度为其根节点左右两棵子树中，最深的那棵子树的深度加一.

`depth(root) = max(depth(root.left), depth(root.right)) + 1`

显然我们可以用深度搜索（`DFS`）来实现这一算法，非常简单。


#### 示例代码 （python）

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        ans = max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
        return ans
```

#### 示例代码 （c++）

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int depthHelper(TreeNode* curr, int depth) {
        int left,right;
        if(!curr) {
            return depth;
        }
        left = depthHelper(curr->left, depth + 1);
        right = depthHelper(curr->right, depth + 1);
        return left>right?left:right;
    }
    int maxDepth(TreeNode* root) {
        return depthHelper(root, 0);
    }
};
```

#### 复杂度分析
使用深度搜索`DFS`,每个节点被访问一次。并且递归过程中，栈的最大深度为O(n)。考虑到本题并非平衡二叉树，最差将退化成链表，而大O代表复杂度的上阈值，因此为O(n)。
所以复杂度分析为：

- 时间复杂度：O(n)
- 空间复杂度：O(1), &#160; 递归栈深度O(n)

#### 总结归纳：
这题比较简单，想清楚树的深度的定义，找出递归的关系，就可以利用递归的方法解题。当然也可以使用非递归的方便遍历树来解决这一问题，有兴趣的朋友可以自己试试。

更多Tree相关的内容将更新在 [Tree Tag](/tags/Tree)，尽请期待，种香蕉树去了：）
