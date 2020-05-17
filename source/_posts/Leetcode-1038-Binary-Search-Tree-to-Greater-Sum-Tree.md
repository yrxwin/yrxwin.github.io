---
title: Leetcode 1038 Binary Search Tree to Greater Sum Tree
categories:
  - leetcode
author: '大猩猩'
date: 2020-05-17 12:54:39
tags: ['Amazon','Amazon','Binary Search Tree']
keywords: ['Binary Search Tree', 'Inorder traversals']
description:
---
#### 原题说明
Given the root of a binary search tree with distinct values, modify it so that every `node` has a new value equal to the sum of the values of the original tree that are greater than or equal to `node.val`.

As a reminder, a *binary search tree* is a tree that satisfies these constraints:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.




**Example 1:**
{% blockquote %}
{% asset_img lc1038.png 400 "" %}
**Input:**
[4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
**Output:** 
[30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]
{% endblockquote %}


**Constraints:**

The number of nodes in the tree is between `1` and `100`.
Each node will have value between `0` and `100`.
The given tree is a binary search tree.
**Note**: This question is the same as 538: https://leetcode.com/problems/convert-bst-to-greater-tree/


<!--more-->

#### 解题思路
题目要求将`binary search tree`中每个节点的值替换成不小于当前节点的所有元素的和。我们可以利用中序遍历的思想，进行发”反向“的中序遍历。也就是说将元素从大到小的进行搜索。遍历过程中，用一个变量记录到当前节点位置为止，所遍历过的元素的和。将其与当前节点的值进行替换。

代码可以用`recursion`和`iteration`两种方法实现。这里使用`iteration`的方法.优点在于，一是加深对中序遍历的理解， 二是避免`stack overflow`。

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
    TreeNode* bstToGst(TreeNode* root) {
        int curSum = 0;
        TreeNode* tmp = root;
        stack<TreeNode*> sk;
        while (!sk.empty() || tmp) {
            if (tmp) {
                sk.push(tmp);
                tmp = tmp->right;
            }
            else {
                tmp = sk.top();
                curSum += tmp->val;
                tmp->val = curSum;
                sk.pop();
                tmp = tmp->left;
            }
        }
        return root;
    }
};
```

#### 示例代码 (java)
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    int pre = 0;
    public TreeNode bstToGst(TreeNode root) {
        if (root.right != null) bstToGst(root.right);
        pre = root.val = pre + root.val;
        if (root.left != null) bstToGst(root.left);
        return root;
    }     
}
```

#### 示例代码 (python)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    val = 0
    def bstToGst(self, root: TreeNode) -> TreeNode:
        if root.right: self.bstToGst(root.right)
        root.val = self.val = self.val + root.val
        if root.left: self.bstToGst(root.left)
        return root
```

#### 复杂度分析
时间复杂度: O(n)
空间复杂度: O(1)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://www.youtube.com/watch?v=Y17ZpASccdA&t=65s)，欢迎关注！