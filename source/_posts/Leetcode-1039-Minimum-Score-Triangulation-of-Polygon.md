---
title: '[Leetcode 1039] Minimum Score Triangulation of Polygon'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-05-17 19:42:49
tags: ['Uber', 'Dynamic Programming']
keywords: ['Uber', 'Dynamic Programming']
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">N</code>, consider a convex&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">N</code>-sided polygon with vertices labelled&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A[0], A[i], ..., A[N-1]</code>&nbsp;in clockwise order.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Suppose you triangulate the polygon into&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">N-2</code>&nbsp;triangles.&nbsp; For each triangle, the value of that triangle is the&nbsp;<span style="font-weight: bolder;">product</span>&nbsp;of the labels of the vertices, and the&nbsp;<em>total score</em>&nbsp;of the triangulation is the sum of these values over all&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">N-2</code>&nbsp;triangles in the triangulation.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Return the smallest possible total score that you can achieve with some triangulation of the polygon.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"></ol><div style="color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-1-1">[1,2,3]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">6</span>
<span style="font-weight: bolder;">Explanation: </span>The polygon is already triangulated, and the score of the only triangle is 6.
</pre><div><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example 2:</span></p><p style="font-size: inherit; margin-bottom: 1em;"><img alt="" src="https://assets.leetcode.com/uploads/2019/05/01/minimum-score-triangulation-of-polygon-1.png" style="border-style: none; max-width: 100%; height: 150px; width: 253px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-2-1">[3,7,4,5]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">144</span>
<span style="font-weight: bolder;">Explanation: </span>There are two triangulations, with possible scores: 3*7*5 + 4*5*7 = 245, or 3*4*5 + 3*4*7 = 144.  The minimum score is 144.
</pre><div><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example 3:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-3-1">[1,3,1,4,1,5]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-3">13</span>
<span style="font-weight: bolder;">Explanation: </span>The minimum score triangulation has score 1*1*3 + 1*1*4 + 1*1*5 + 1*1*1 = 13.
</pre><p style="font-size: inherit; margin-bottom: 1em;">&nbsp;</p><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">3 &lt;= A.length &lt;= 50</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= A[i] &lt;= 100</code></li></ol></div></div></div>
<!--more-->

#### 解题思路
动态规划，递归可以使逻辑简单（本质还是动态规划）
1. 将多边形起始位置设为`start`，`end`, 用一个数组dp来记录任意起始位置的`score`
2. 为了计算`dp[start][end]`, 我们用一个index `k`在`start`到`end`之间遍历
`dp[start][end] = min(dp[start][k] + dp[k][end] + A[start] * A[k] * A[end])`
3. 结果为`dp[0][n - 1]`
**注意**：
1. 相邻的`dp[i][i + 1] = 0`, 因为两条边无法组成三角形
2. 如果用传统动归的方法，必须`i`的位置从`j`开始往前推，不能`i`和`j`都从小往大推，不然`dp[k][j]`是未知的。

#### 示例代码 (cpp)
递归（实际上还是动态规划，因为有memorization）
```cpp
class Solution {
    int getScore(const vector<int>& A, vector<vector<int>>& dp, int start, int end) {
        if (start >= end - 1) {
            return 0;
        }
        if (dp[start][end] > 0) {
            return dp[start][end];
        }
        int score = INT_MAX;
        for (int k = start + 1; k <= end - 1; ++k) {
            score = min(score, getScore(A, dp, start, k) + getScore(A, dp, k, end) + A[start] * A[k] * A[end]);
        }
        dp[start][end] = score;
        return score;
    }
public:
    // 递归（实际上还是动态规划，因为有memorization）
    int minScoreTriangulation(vector<int>& A) {
        int n = A.size();
        vector<vector<int>> dp(n, vector<int>(n, 0));
        return getScore(A, dp, 0, n - 1);
    }
};
```

动态规划
```cpp
class Solution {
public:
    int minScoreTriangulation(vector<int>& A) {
        int n = A.size();
        vector<vector<int>> dp(n, vector<int>(n, 0));
        for (int j = 2; j < n; ++j) {
            for (int i = j - 2; i >= 0; --i) {
                dp[i][j] = INT_MAX;
                for (int k = i + 1; k < j; ++k) {
                    dp[i][j] = min(dp[i][j], dp[i][k] + dp[k][j] + A[i] * A[j] * A[k]);
                }
            }
        }
        return dp[0][n - 1];
    } 
};
```

#### 示例代码 (java)
```java
class Solution {
    public int minScoreTriangulation(int[] A) {
        int n = A.length;
        int[][] dp = new int[n][n];
        for (int j = 2; j < n; ++j) {
            for (int i = j - 2; i >= 0; --i) {
                dp[i][j] = Integer.MAX_VALUE;
                for (int k = i + 1; k < j; ++k)
                    dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k][j] + A[i] * A[j] * A[k]);
            }
        }
        return dp[0][n - 1];
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def minScoreTriangulation(self, A: List[int]) -> int:
        n = len(A)
        dp = [[0] * n for i in range(n)]
        for d in range(2, n):
            for i in range(n - d):
                j = i + d
                dp[i][j] = min(dp[i][k] + dp[k][j] + A[i] * A[j] * A[k] for k in range(i + 1, j))
        return dp[0][n - 1]
```

#### 复杂度分析
时间复杂度:`O(N^3)`, 用传统动归可以很容易看出，用递归的方法可以想到任意`dp[i][j]`都遍历一次`O(N^2)`，而每一次遍历中
都有一个 `for (int k = start + 1; k <= end - 1; ++k)`用到`O(N)`
空间复杂度:`O(N^2)`, 递归会使用额外的`O(N)`stack

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/q1tM-6lXwEU)，欢迎关注！