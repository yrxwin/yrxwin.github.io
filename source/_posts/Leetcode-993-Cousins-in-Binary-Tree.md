---
title: '[Leetcode 993] Cousins in Binary Tree'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-02-23 22:25:38
tags: ['Bloomberg', 'Tree']
keywords: ['Bloomberg', 'Tree']
description:
---
#### 原题说明
In a binary tree, the root node is at depth 0, and children of each depth k node are at depth `k+1`.

Two nodes of a binary tree are cousins if they have the same depth, but have different parents.

We are given the root of a binary tree with unique values, and the values x and y of two different nodes in the tree.

Return true if and only if the nodes corresponding to the values x and y are cousins.


**Example 1:**
{% asset_img example1.png 250 %}{% blockquote %}
**Input:** `root = [1,2,3,4], x = 4, y = 3`
**Output:** `false`
{% endblockquote %}

**Example 2:**
{% asset_img example2.png 250 %}{% blockquote %}
**Input:** `root = [1,2,3,null,4,null,5], x = 5, y = 4`
**Output:** `true`
{% endblockquote %}

**Example 3:**
{% asset_img example3.png 250 %}{% blockquote %}
**Input:** `root = [1,2,3,null,4], x = 2, y = 3`
**Output:** `false`
{% endblockquote %}
 
**Note:**
1. The number of nodes in the tree will be between 2 and 100.
2. Each node has a unique integer value from 1 to 100.
<!-- more -->

#### 解题思路
因为要判断两个节点是否同层，想到用BFS逐层扫描.
对于每一层的节点：
    1) 用`has_x`和`has_y`代表`x`和`y`是否出现在本层
    2) 判断该节点的子节点是否同时是`x`和`y`，如果是，说明x和y是兄弟节点，而非cousin节点，直接`return false`
    3) 该层扫描结束后，如果has_x和has_y同时为true，说明x和y同时出现在该层，`return true`
    4) 该层扫描结束后，如果has_x和has_y仅有一个为true，则x和y必然在不同层，`return false`
整棵树扫描结束后，如果还是没有返回，说明之前并未遇到过x或y中任何一个，`return false`

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    bool isCousins(TreeNode* root, int x, int y) {
        queue<TreeNode*> qu;
        if (!root) {
            return false;
        }
        qu.push(root);
        while (!qu.empty()) {
            // has_x and has_y represents whether x and y exist in this level
            bool has_x = false;
            bool has_y = false;
            // level_size means number of nodes at this level, so we don't need two queue to swap 
            int level_size = qu.size();
            for (int i = 0; i < level_size; ++i) {
                TreeNode* cur = qu.front();
                qu.pop();
                if (cur->val == x) {
                    has_x = true;
                }
                if (cur->val == y) {
                    has_y = true;
                }
                // Check if x and y are sibling
                if (cur->left && cur->right) {
                    if (cur->left->val == x && cur->right->val == y) {
                        return false;
                    }
                    if (cur->right->val == x && cur->left->val == y) {
                        return false;
                    }
                }
                if (cur->left) {
                    qu.push(cur->left);
                }
                if (cur->right) {
                    qu.push(cur->right);
                }
            }
            if (has_x && has_y) {
                return true;
            }
            // Good to add this condition since x and y are unique in the tree
            if (has_x || has_y) {
                return false;
            }
        }
        return false;
    }
};
```

#### 复杂度分析
时间复杂度: `O(n)`
空间复杂度: `O(log(n))`

#### 归纳总结
这道题重点要理解题意，cousin节点之间必须在同一层，且父节点不同。官网的解答空间复杂度不高，且整个想法不够直观，不是很推荐。

我们在**Youtube**上更新了[视频讲解](https://www.youtube.com/watch?v=LoBbUrWPH7k)，欢迎关注！