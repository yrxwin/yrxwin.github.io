---
title: '[Leetcode 116] Populating Next Right Pointers in Each Node'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-05 14:36:07
tags: [Tree, Breadth-first Search, Microsoft]
keywords: [Tree, Breadth-first Search, Microsoft]
description:
---


#### 原题说明
Given a binary tree

    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }
    
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

*Note*:

You may only use constant extra space.

You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).

For example,

Given the following perfect binary tree,

         1
       /  \
      2    3
     / \  / \
    4  5  6  7
After calling your function, the tree should look like:

         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL

#### 解题思路
本题要去给一个完美二叉树加上next节点，如果没有类似节点则标记为`NULL`。结合给出的例子，还是题意还是比较清晰的。

最简单的思路，可以结合我们之前层序遍历二叉树的一题 [[LeetCode 102] Binary Tree Level Order Traversal 二叉树层序遍历](/Leetcode-102-Binary-Tree-Level-Order-Traversal)，把每一层的节点按顺序加上next节点即可。然而，这样的空间复杂度会是O(n),并不符合要求。

为了优化空间复杂度，我们需要记录每层的信息，保存前一个节点，遍历到下一个节点之后，让前一个结点的next到当前节点（如果前面没有节点或者当前节点是最后一个，就另行处理）

具体而言，我们用`cur`记录当前层第一个节点。在每个层间，用`pre`记录当前节点的前一个节点。如果`pre`非空，那么把`pre.next`连接到当前节点`root.left`,再更新`pre`。当一层遍历完，就更新到下一层。 具体参看代码实例。结合题中给的树的例子和给出的示例代码，能更清晰的理解其中逻辑。

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
        if not root:
            return
        while root.left:
            cur = root.left
            prev = None
            while root:
                if prev:
                    prev.next = root.left
                root.left.next = root.right
                prev = root.right
                root = root.next
            root = cur
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
            leftMost = root;
            while(root) {
                if (root->left) {
                    if (prev) {
                        prev->next = root->left;
                    }
                    root->left->next = root->right;
                    prev = root->right;
                }
                root = root->next;
            }
            prev = NULL;
            root = leftMost->left;
        }
    }
};
```

#### 复杂度分析
广度搜索`BFS`遍历二叉树，每个节点被遍历一次，时间复杂度为O(n）。同时我们使用了`cur`，`pre`两个变量，空间复杂度为O(1)。因此复杂度分析为：

- 时间复杂度： `O(n)`
- 空间复杂度：`O(1）`

#### 总结归纳：
这题题意清晰。为了优化空间复杂度，需要我们对层序遍历做更细致的操作。

以后我们会再介绍本题的进阶版，对非完美二叉树改如何实现同样的操作。基本思路与这题相同，只是需要做更进一步的判断实现next的链接。有兴趣的朋友可以参看

[[LeetCode 117] Populating Next Right Pointers in Each Node II](/Leetcode-117-Populating-Next-Right-Pointers-in-Each-Node-II)

种香蕉树去了^_^
