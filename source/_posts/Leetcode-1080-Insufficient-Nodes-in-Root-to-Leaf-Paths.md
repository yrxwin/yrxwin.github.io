---
title: '[Leetcode 1080] Insufficient Nodes in Root to Leaf Paths'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-08-12 17:58:40
tags: ['Depth-first Search', 'Amazon']
keywords:
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given the&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">root</code>&nbsp;of a binary tree, consider all&nbsp;<em>root to leaf paths</em>: paths from the root&nbsp;to any leaf.&nbsp; (A leaf is a node with no children.)</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">A&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">node</code>&nbsp;is&nbsp;<em>insufficient</em>&nbsp;if&nbsp;<span style="font-weight: bolder;">every</span>&nbsp;such root to leaf path intersecting this&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">node</code>&nbsp;has sum strictly less than&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">limit</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Delete all insufficient nodes simultaneously, and return the root of the resulting&nbsp;binary tree.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;"><img alt="" src="https://assets.leetcode.com/uploads/2019/06/05/insufficient-11.png" style="border-style: none; max-width: 100%; height: 200px; width: 482px;">
Input: </span>root = <span id="example-input-1-1">[1,2,3,4,-99,-99,7,8,9,-99,-99,12,13,-99,14]</span>, limit = <span id="example-input-1-2">1</span>
<span style="font-weight: bolder;"><img alt="" src="https://assets.leetcode.com/uploads/2019/06/05/insufficient-2.png" style="border-style: none; max-width: 100%; height: 200px; width: 258px;">
Output: </span><span id="example-output-1">[1,2,3,4,null,null,7,8,9,null,14]</span>
</pre><div style="color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;"><img alt="" src="https://assets.leetcode.com/uploads/2019/06/05/insufficient-3.png" style="border-style: none; max-width: 100%; height: 200px; width: 292px;">
Input: </span>root = <span id="example-input-2-1">[5,4,8,11,null,17,4,7,1,null,null,5,3]</span>, limit = <span id="example-input-2-2">22</span>
<span style="font-weight: bolder;"><img alt="" src="https://assets.leetcode.com/uploads/2019/06/05/insufficient-4.png" style="border-style: none; max-width: 100%; height: 200px; width: 264px;">
Output: </span><span id="example-output-2">[5,4,8,11,null,17,4,7,null,null,null,5]</span></pre><p style="font-size: inherit; margin-bottom: 1em;">&nbsp;</p><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example 3:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;"><img alt="" src="https://assets.leetcode.com/uploads/2019/06/11/screen-shot-2019-06-11-at-83301-pm.png" style="border-style: none; max-width: 100%; height: 150px; width: 188px;">
Input: </span>root = [1,2,-3,-5,null,4,null], limit = -1
<img alt="" src="https://assets.leetcode.com/uploads/2019/06/11/screen-shot-2019-06-11-at-83517-pm.png" style="border-style: none; max-width: 100%; height: 150px; width: 122px;"><span style="font-weight: bolder;">
Output: </span>[1,null,-3,4]</pre></div><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li>The given tree will have between&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">5000</code>&nbsp;nodes.</li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">-10^5&nbsp;&lt;= node.val &lt;= 10^5</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">-10^9 &lt;= limit&nbsp;&lt;= 10^9</code></li></ol>
<!--more-->

#### 解题思路

题目要去除所有不充分的点。这里对一个点是否充分的定义是：每一条从根节点开始，通过该点到达任意叶子节点的路径的和，都严格小于题目给出的值`Limit`。把所有不充分的点同时删除后，返回剩下的二叉树的根。
用`dfs`的方法解题，
1. 当一个节点是叶子节点时，直接判断它是否是充分的，如果不是，返回`nullptr`，否则返回该节点的指针。
2. 当一个节点不是叶子节点时，判断它的子节点是不是都是不充分的。如果都是不充分的，那么返回`nullptr`，也就是说它也是不充分的。否则返回该节点的指针。

工程上，`C++`可以选用`smart pointer`,从而不用考虑内存泄露的问题。

#### 示例代码 (cpp)
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* sufficientSubset(TreeNode* root, int limit) {
        return helper(root, limit);
    }
    
private:
    TreeNode* helper(TreeNode* node, int limit, int cur = 0) {
        if (node == nullptr) {
            return nullptr;
        }
        cur += node->val;
        if (node->left == nullptr && node->right == nullptr) {
            if (cur < limit) {
                delete node;
                return nullptr;
            }
            return node;
        }
        node->left = helper(node->left, limit, cur);
        node->right = helper(node->right, limit, cur);
        if (node->left == nullptr && node->right == nullptr) {
            return nullptr;
        }
        return node;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public TreeNode sufficientSubset(TreeNode root, int limit) {
        if (root == null)
            return null;
        if (root.left == null && root.right == null)
            return root.val < limit ? null : root;
        root.left = sufficientSubset(root.left, limit - root.val);
        root.right = sufficientSubset(root.right, limit - root.val);
        return root.left == root.right ? null : root;
    }
}
```

#### 示例代码 (python)
```python
class Solution(object):
    def sufficientSubset(self, root, limit):
        """
        :type root: TreeNode
        :type limit: int
        :rtype: TreeNode
        """
        if root.left == root.right:
            return None if root.val < limit else root
        if root.left:
            root.left = self.sufficientSubset(root.left, limit - root.val)
        if root.right:
            root.right = self.sufficientSubset(root.right, limit - root.val)
        return root if root.left or root.right else None
```

#### 复杂度分析
时间复杂度: O(n)
空间复杂度: O(1)

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/tm6atdrcmkI)，欢迎关注！