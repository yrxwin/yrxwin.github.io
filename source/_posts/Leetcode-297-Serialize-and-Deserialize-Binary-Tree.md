---
title: '[Leetcode 297] Serialize and Deserialize Binary Tree'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-11 14:00:35
tags: [Tree, Design, Google, Facebook, Microsoft, Amazon, Bloomberg, Uber, LinkedIn, Yahoo]
keywords: [Tree, Design]
description:
---

#### 原题说明
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

For example, you may serialize the following tree

        1
       / \
      2   3
         / \
        4   5
as `"[1,2,3,null,null,4,5]"`, just the same as [how LeetCode OJ serializes a binary tree](https://leetcode.com/faq/#binary-tree). You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

 

**Note**: Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.


#### 解题思路
本题要求设计两个函数，系列化和反序列化（重构）二叉树。

序列化函数：我们可以用层序遍历的方法将二叉树储存，可以参考[[LeetCode 102] Binary Tree Level Order Traversal 二叉树层序遍历](/Leetcode-102-Binary-Tree-Level-Order-Traversal)， 需要注意的一点，遍历过程中，若是当前节点的子节点是空的，我们依然需要储存，这样才能在反序列函数中重构二叉树。

反序列化函数：用队列的数据结构，按层序读取序列，每次读取两个元素，对应当前节点的左右子节点。当序列元素非空时，将其设为当前节点对应的左节点或右节点，并加入队列内。直到读取完所有序列内元素，完成二叉树的重构。

另一种思路是用前序遍历。因为递归的实现比较trivial，这里用递推实现。同样，为了正确重构，我们仍然需要储存空节点。这里我们加入`writeAndReturnNode`这个辅助函数，让我们可以最大程度的复用原始的递推代码。需要额外注意不要使同一个节点被写一次以上。在解码时，由于在原代码push时不知道右子节点的情况，因此改为push本节点，并在pop时获取正确右子节点状态后，将`curr`改为右子节点。

#### 示例代码 思路一 (python)
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        if not root:
            return "None"
        queue, ans = collections.deque(), collections.deque()
        queue.append(root)
        while queue:
            tmpNode = queue.popleft()
            if tmpNode == None:
                ans.append(tmpNode)
            else:
                ans.append(tmpNode.val)
                queue.extend([tmpNode.left,tmpNode.right])
        return str(list(ans)) #序列返回的结构和题目例子中给出的是一致的
            
    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        data = data[1:-1].split(",")
        if not self.represents_int(data[0]) or not data:
            return None
        else:
            root = TreeNode(int(data[0]))
        idx = 1
        queue = collections.deque()
        queue.append(root)
        while idx != len(data):
            tmpNode = queue.popleft()
            if self.represents_int(data[idx]):
                tmpNode.left = TreeNode(int(data[idx]))
                queue.append(tmpNode.left)
            if self.represents_int(data[idx+1]):
                tmpNode.right = TreeNode(int(data[idx+1]))
                queue.append(tmpNode.right)
            idx += 2
        return root

    def represents_int(self, num):
        try: 
            int(num)
            return True
        except ValueError:
            return False
            
        

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```

#### 示例代码 思路二 (cpp)
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
class Codec {
public:
    TreeNode* writeAndReturnNode(TreeNode* node, ostringstream& ret) {
        if (node) {
            ret << node->val << " ";
        } else {
            ret << "X ";
        }
        return node;
    }
    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        ostringstream ret;
        stack<TreeNode*> nodeStack;
        while (writeAndReturnNode(root, ret) || !nodeStack.empty()) {
            while(root) {
                nodeStack.push(root->right);
                root = writeAndReturnNode(root->left, ret);
            }
            if (!nodeStack.empty()) {
                root = nodeStack.top();
                nodeStack.pop();
            }
        }
        return ret.str();
    }

    TreeNode* readAndReturnNode(istringstream& inStream) {
        string nextVal;
        inStream >> nextVal;
        if (nextVal == "X") {
            return NULL;
        } else {
            return new TreeNode(stoi(nextVal));
        }
    }
    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        TreeNode *root, *curr, *next;
        stack<TreeNode*> nodeStack;
        istringstream inStream(data);
        root = readAndReturnNode(inStream);
        curr = root;
        while (curr || !nodeStack.empty()) {
            while(curr) {
                curr->left = readAndReturnNode(inStream);
                nodeStack.push(curr);
                curr = curr->left;
            }
            
            if (!nodeStack.empty()) {
                curr = nodeStack.top();
                nodeStack.pop();
                curr->right = readAndReturnNode(inStream);
                curr = curr->right;
            }
        }
        return root;
    }
};
```
#### 复杂度分析
每个节点被访问一次，同时我们用额外空间（队列/栈）来储存中间过程或答案，所以复杂度分析为
时间复杂度: `O(n)`
空间复杂度: `O(n)`

#### 归纳总结
这是一道设计题，对二叉树的序列化和反序列还可以有其它灵活的处理方法。有兴趣的朋友可以再多做一些尝试。
