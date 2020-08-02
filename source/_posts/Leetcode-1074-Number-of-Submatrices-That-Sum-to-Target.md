---
title: '[Leetcode 1074] Number of Submatrices That Sum to Target'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-08-01 12:12:29
tags: ['Google','Amazon']
keywords:
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given a&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">matrix</code>, and a&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">target</code>, return the number of non-empty submatrices that sum to&nbsp;<font face="monospace">target</font>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">A submatrix&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">x1, y1, x2, y2</code>&nbsp;is the set of all cells&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">matrix[x][y]</code>&nbsp;with&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">x1 &lt;= x &lt;= x2</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">y1 &lt;= y &lt;= y2</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Two submatrices&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">(x1, y1, x2, y2)</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">(x1', y1', x2', y2')</code>&nbsp;are different if they have some coordinate&nbsp;that is different: for example, if&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">x1 != x1'</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>matrix = <span id="example-input-1-1">[[0,1,0],[1,1,1],[0,1,0]]</span>, target = <span id="example-input-1-2">0</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">4</span>
<span style="font-weight: bolder;">Explanation: </span>The four 1x1 submatrices that only contain 0.
</pre><div style="color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>matrix = <span id="example-input-2-1">[[1,-1],[-1,1]]</span>, target = <span id="example-input-2-2">0</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">5</span>
<span style="font-weight: bolder;">Explanation: </span>The two 1x2 submatrices, plus the two 2x1 submatrices, plus the 2x2 submatrix.
</pre></div><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;"><span style="font-weight: bolder;">Note:</span></span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= matrix.length &lt;= 300</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= matrix[0].length &lt;= 300</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">-1000 &lt;= matrix[i] &lt;= 1000</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">-10^8 &lt;= target &lt;= 10^8</code></li></ol>
<!--more-->

#### 解题思路
这题是`presum`思想的变种二维版本。
首先我们可以把每一行的`presum`都先计算出来，用一个二维的`vector`保存。
之后，对任意两个列`col1`, `col2`, 计算`col1`和`col2`之间的所有数的和， 因为对于每一行，我们已经计算了它们对应的`presum`, 所以，对于`col1`,`col2`之间的数，可以通过`presum[row][col2+1]` - `presum[row][col1]` 迅速得到。（注意我们开`presum`数组时，选择多开一个，这样处理了第一个数的和的问题。详细参考c++代码）
我们可以依次得到在列区间`col1`, `col2`中，第`0`行到第`row`行的所有的数的和。用一个哈希表存下来，边可以查询满足题目要求的`Submatrix`。相当与又一个`presum`的思想。可参考[leetcode 560题](https://leetcode.com/problems/subarray-sum-equals-k/)

综上所述，这题通过二维的presum运用的可以得到解答。相关的题目还有[leetcode 304 Range Sum Query 2D - Immutable](https://leetcode.com/problems/range-sum-query-2d-immutable/)。 大家可以练习下

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int numSubmatrixSumTarget(vector<vector<int>>& A, int target) {
        int res = 0, m = A.size(), n = A[0].size();
        vector<vector<int>> presum(m, vector<int>(n + 1, 0));
        
        for (int i = 0; i < m; i++) {
            for (int j = 1; j < n + 1; j++) {
                presum[i][j] += presum[i][j - 1] + A[i][j - 1];
            }
        }

        unordered_map<int, int> counter;
        for (int col1 = 0; col1 < n + 1; col1++) {
            for (int col2 = col1 + 1; col2 < n + 1; col2++) {
                counter = {{0,1}};
                int cur = 0;
                for (int row = 0; row < m; row++) {
                    cur += presum[row][col2] - presum[row][col1];
                    res += counter.find(cur - target) != counter.end() ? counter[cur - target] : 0;
                    counter[cur]++;
                }
            }
        }
        return res;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int numSubmatrixSumTarget(int[][] A, int target) {
        int res = 0, m = A.length, n = A[0].length;
        for (int i = 0; i < m; i++)
            for (int j = 1; j < n; j++)
                A[i][j] += A[i][j - 1];
        Map<Integer, Integer> counter = new HashMap<>();
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                counter.clear();
                counter.put(0, 1);
                int cur = 0;
                for (int k = 0; k < m; k++) {
                    cur += A[k][j] - (i > 0 ? A[k][i - 1] : 0);
                    res += counter.getOrDefault(cur - target, 0);
                    counter.put(cur, counter.getOrDefault(cur, 0) + 1);
                }
            }
        }
        return res;
    }
}
```

#### 示例代码 (python)
```python
class Solution(object):
    def numSubmatrixSumTarget(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: int
        """
        m, n = len(matrix), len(matrix[0])
        for row in matrix:
            for i in xrange(n - 1):
                row[i + 1] += row[i]
        res = 0
        for i in xrange(n):
            for j in xrange(i, n):
                c = collections.defaultdict(int)
                cur, c[0] = 0, 1
                for k in xrange(m):
                    cur += matrix[k][j] - (matrix[k][i - 1] if i > 0 else 0)
                    res += c[cur - target]
                    c[cur] += 1
        return res   
```

#### 复杂度分析
`m`为行数，`n`为列数。
时间复杂度: O(mn^2)
空间复杂度: O(mn)

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/svOoUutTOdo)，欢迎关注！