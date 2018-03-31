---
title: '[Leetcode 94] Binary Tree Inorder Traversal'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-03-30 16:53:07
tags: [Hash Table,Stack,Tree,Microsoft]
---
Given a binary tree, return the *inorder* traversal of its nodes' values.

For example:

Given binary tree [1,null,2,3],
   
    1   
     \
	  2
	 /
    3
   
return [1,3,2].

**Note**: Recursive solution is trivial, could you do it iteratively?

#### 解题思路
深度遍历二叉树（`DFS`），可以分为

 - 前序遍历（`preorder`）
 - 中序遍历（`inorder`）
 - 后序遍历（`postorder`）

这题要求使用中序遍历。中序遍历按照左子节点（`left`），根节点（`root`），右子节点（`right`）的顺序深度遍历二叉树。

同样，我们可以使用递归与非递归两种方法来实现前序遍历。递归的方法比较简单，参看相关代码就能明白。非递归的方法可以通过栈（`stack`）实现：

使用栈（`stack`），每次visit当前节点`node`，同时如果当前节点的右子节点非空，将此右子节点存入栈中，再将当前节点`node`更新为当前节点的左子节点。直到遍历完整棵二叉树。具体步骤为：

1. 建立一个空栈`stack`

2. 如果当前节点`node`非空或者栈`stack`非空：
	- 2.1 如果当前节点`node`非空：	
	    - 将当前节点`node`压入栈
	    - 更新当前节点`node`为它的左子节点，回到步骤2.1	
	- 2.2 如果栈非空，:	
	    - 将当前节点更新为栈顶元素，并且退栈
	    - 访问当前节点
	    - 更新当前节点`node`为它的右子节点，回到步骤2



#### 示例代码 （递归 python版）

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class Solution:
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        def inorderhelper(root,ans):
            if root is None:
	        return
            inorderhelper(root.left,ans)  
            ans.append(root.val)
            inorderhelper(root.right,ans)
        res = []
        inorderhelper(root,res)
        return res
```

#### 示例代码 （递归 cpp版）

```cpp
 struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 };
 
class Solution {
public:
    void inorderHelper(TreeNode* curr, vector<int> &ret) {
        if (!curr) {
	    return;
	}
        if (curr->left != NULL) {
            inorderHelper(curr->left,ret);
        }
        ret.push_back(curr->val);
        if (curr->right) {
            inorderHelper(curr->right,ret);
        }
        return;
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ret;
        inorderHelper(root,ret);
        return ret;
    }
};
```

#### 示例代码 （非递归 python版）

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

class Solution:
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        stack = collections.deque()
        cur, ans = root, []
        while(cur or stack):
            while cur:
                stack.append(cur)
                cur = cur.left
            if stack:
                cur = stack.pop()
                ans.append(cur.val)
                cur = cur.right
        return ans
```
#### 示例代码 （非递归 cpp版）

```cpp
 struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 };
 
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ret;
        TreeNode* curr = root;
        stack<TreeNode*> nodeStack;
        while(curr || !nodeStack.empty()){
            while(curr) {
                nodeStack.push(curr);
                curr = curr->left;
            }
            curr = nodeStack.top();
            nodeStack.pop();
            ret.push_back(curr->val);
            curr = curr->right;
        }
        return ret;
    }
};
```

#### 复杂度分析
无论递归还是非递归，它们的时间复杂度与空间复杂度都是一样的。每个节点都被访问一次，同时栈的深度为O(log n)。所以复杂度分析为：

- 时间复杂度：O(n)
- 空间复杂度：O(log n)

#### 总结归纳：
今天我们讲了二叉树的中序遍历，结合之前我们介绍的前序遍历，希望能对感兴趣的朋友有所帮助。

这里再介绍一个小知识点，当二叉树(`Binary Tree`)为二叉搜索树（`Binary Search Tree`）时，中序遍历会按照节点值从小到大排列。因此这也提供给我们一个判断二叉树(`Binary Tree`)是否是二叉搜索树（`Binary Search Tree`）的方法。

之后我们会继续讨论和树相关的内容，并更新链接，尽请期待，继续种香蕉树去了：）
