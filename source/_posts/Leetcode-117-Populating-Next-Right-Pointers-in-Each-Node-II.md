---
title: '[Leetcode 117] Populating Next Right Pointers in Each Node II'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-05 18:55:46
tags: [Tree, Breadth-first Search, Microsoft]
keywords: [Tree, Breadth-first Search, Microsoft]
description:
---

#### 原题说明
Follow up for problem *"Populating Next Right Pointers in Each Node"*.

What if the given tree could be any binary tree? Would your previous solution still work?

Note:

- You may only use constant extra space.

For example,

Given the following binary tree,

         1
       /  \
      2    3
     / \    \
    4   5    7
After calling your function, the tree should look like:

         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL

#### 解题思路
这题是[[LeetCode 116] Populating Next Right Pointers in Each Node](/Leetcode-116-Populating-Next-Right-Pointers-in-Each-Node)的进阶题。从完美二叉树变成任意的二叉树。仍然要求空间复杂度为`O(n)`。

总体的思路不变，需要记录每层的信息，保存前一个节点，遍历到下一个节点之后，让前一个结点的`next`链接到当前节点。由于不能保证上一层的父节点都有子节点，因此我们需要对上一层父节点是否存在子节点做出额外的判断，然后遍历当前层的非空节点。这点与之前完美二叉树是不同的。

在示例代码中，`prev`可以看做一个存放当前遍历节点的前一个节点。而`cur`则指向当前层的第一个节点，遍历完整层后，利用`cur`更新下一层。如果对代码的逻辑理解不够清晰，建议用题目给出的二叉树做简单的验算，能有直观认识。

#### 示例代码 (python)
```python
# Definition for binary tree with next pointer.
# class TreeLinkNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
#         self.next = None

class Solution:
    # @param root, a tree link node
    # @return nothing
    def connect(self, root):
        prev = TreeLinkNode(0)
        cur = prev
        while root:
            prev.next = root.left
            if prev.next:
                prev = prev.next
            prev.next = root.right
            if prev.next:
                prev = prev.next
            root = root.next
            if not root:
                prev = cur
                root = cur.next

```

#### 示例代码 (cpp)
```cpp
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        TreeLinkNode *leftMost = NULL, *prev = NULL;
        while(root) {
            while(!root->left && !root->right) {
                root = root->next;
                if (!root) {
                    return;
                }
            }
            leftMost = root;
            while(root) {
                if(root->left) {
                    if (prev) {
                        prev->next = root->left;
                    }
                    prev = root->left;
                }
                if (root->right) {
                    if (prev) {
                        prev->next = root->right;
                    }
                    prev = root->right;
                }
                root = root->next;
            }
            root = leftMost->left ? leftMost->left : leftMost->right;
            prev = NULL;
        }
    }
};
```

#### 复杂度分析
广度搜索`BFS`遍历二叉树，每个节点被遍历一次，时间复杂度为O(n）。同时我们使用了`cur`，`pre`两个变量，空间复杂度为O(1)。因此复杂度分析为：

- 时间复杂度： `O(n)`
- 空间复杂度： `O(1）`

#### 总结归纳：
这题是对[[LeetCode 116] Populating Next Right Pointers in Each Node](/Leetcode-116-Populating-Next-Right-Pointers-in-Each-Node)的进阶，要求更高。但总体解题的逻辑不变。因此此题的解法也完全适用于`Leetcode 166`。

种香蕉树去了^_^
