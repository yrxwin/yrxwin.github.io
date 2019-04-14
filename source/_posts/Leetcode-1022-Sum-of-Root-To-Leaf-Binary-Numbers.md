---
title: '[Leetcode 1022] Sum of Root To Leaf Binary Numbers'
categories:
  - leetcode
author: '大猩猩'
date: 2019-04-12 23:16:53
tags: ['Tree','Amazon']
keywords:
description:
---

#### 原题说明
Given a binary tree, each node has value `0` or `1`.  Each root-to-leaf path represents a binary number starting with the most significant bit.  For example, if the path is `0 -> 1 -> 1 -> 0 -> 1`, then this could represent `01101` in binary, which is `13`.

For all leaves in the tree, consider the numbers represented by the path from the root to that leaf.

Return the sum of these numbers.


**Example 1:**
{% asset_img lc1022.png 400 "" %}
{% blockquote %}
**Input:** `[1,0,1,0,1,0,1]`
**Output:** `22`
**Explanation:** (100) + (101) + (110) + (111) = 4 + 5 + 6 + 7 = 22
{% endblockquote %}
 
**Note:**
1. The number of nodes in the tree is between `1` and `1000`.
2. node.val is `0` or `1`.
3. The answer will not exceed `2^31 - 1`.


#### 解题思路
这题比较简单，通过dfs先序遍历二叉树，分别计算每一条从root到leaf的二进制数，累加即可。

#### 示例代码 (cpp)
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
    int sumRootToLeaf(TreeNode* root) {
        int ans = 0;
        helperFunc(root, ans);
        return ans;
    }
    void helperFunc(TreeNode* Node, int& ans, int tmpSum = 0) {
        tmpSum = tmpSum * 2 + Node->val;
        if (Node->right) {
            helperFunc(Node->right, ans, tmpSum);
        }
        if (Node->left) {
            helperFunc(Node->left, ans, tmpSum);
        }
        if (!Node->right && !Node->left) {
            ans += tmpSum;
        }
    }
};
```

#### 复杂度分析
时间复杂度: O(n)
空间复杂度: O(1)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/bnvE2hfjbdo)，欢迎关注！