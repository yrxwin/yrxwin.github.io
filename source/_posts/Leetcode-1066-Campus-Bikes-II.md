---
title: '[Leetcode 1066] Campus Bikes II'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-07-02 16:10:19
tags: ['Google','Amazon','Backingtracking','Dynamic Programming']
keywords:
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">On a campus represented as a 2D grid, there are&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">N</code>&nbsp;workers and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">M</code>&nbsp;bikes, with&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">N &lt;= M</code>. Each worker and bike is a 2D coordinate on this grid.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">We assign one unique bike to each worker so that the sum of the Manhattan distances between each worker and their assigned bike is minimized.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">The Manhattan distance between two points&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">p1</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">p2</code>&nbsp;is&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">Manhattan(p1, p2) = |p1.x - p2.x| + |p1.y - p2.y|</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Return the minimum possible sum of Manhattan distances between each worker and their assigned bike.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/06/1261_example_1_v2.png" style="border-style: none; max-width: 100%; height: 264px; width: 264px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>workers = <span id="example-input-1-1">[[0,0],[2,1]]</span>, bikes = <span id="example-input-1-2">[[1,2],[3,3]]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">6</span>
<span style="font-weight: bolder;">Explanation: </span>
We assign bike 0 to worker 0, bike 1 to worker 1. The Manhattan distance of both assignments is 3, so the output is 6.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/06/1261_example_2_v2.png" style="border-style: none; max-width: 100%; height: 264px; width: 264px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>workers = <span id="example-input-2-1">[[0,0],[1,1],[2,0]]</span>, bikes = <span id="example-input-2-2">[[1,0],[2,2],[2,1]]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">4</span>
<span style="font-weight: bolder;">Explanation: </span>
We first assign bike 0 to worker 0, then assign bike 1 to worker 1 or worker 2, bike 2 to worker 2 or worker 1. Both assignments lead to sum of the Manhattan distances as 4.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0 &lt;= workers[i][0], workers[i][1], bikes[i][0], bikes[i][1] &lt; 1000</code></li><li>All worker and bike locations are distinct.</li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= workers.length &lt;= bikes.length &lt;= 10</code></li></ol>
<!--more-->

#### 解题思路
我们先用一个二维矩阵记录每个工人到每辆车的距离，`dp[i][j] = distance`就表示工人`i`和车`j`的距离为`distance`。

这样我们把问题就转化为：在二维矩阵里每一行取一个数，同时每个数不能有相同的列，要求让所有取出的数之和最小。

如果用简单的暴力破解，用`dfs`把所有取法都遍历一遍，时间复杂度是`O(N!)`。这里是不能通过测试的。

因此我们需要用`backtracking + memoization`的方法做优化。用一个数`state`表示已经选取了的`bike`的组合。这样`memo[state]`就表示在当前选取的自行车组合下，之后能得到的最小和。

这样我们就能从后往前递归，减少重复计算的，大大降低时间复杂度。
这是一种`bottom up`的思想。

这里有一个技巧，我们用二进制的思想构造`state`。因为自行车的数量不超过`10`个,那么在第`i`位上，如果等于`1`，则说明第`i`辆自行车被选择了，否则就是没被选择。

#### 示例代码 (cpp)
```cpp
class Solution {
private:
    int dict(const vector<int>& worker, const vector<int>& bike) {
        return abs(worker[0] - bike[0]) + abs(worker[1] - bike[1]);
    }
    public:
    int assignBikes(vector<vector<int>>& workers, vector<vector<int>>& bikes) {
        vector<vector<int>> dp(workers.size(), vector<int>(bikes.size(), 0));
        for (auto i = 0; i < workers.size(); ++i) {
            for (auto j = 0; j < bikes.size(); ++j) {
                dp[i][j] = dict(workers[i], bikes[j]);
            }
        }
        int res = INT_MAX;
        vector<int> memo(1 << bikes.size(), 0);
        return permRes(dp, memo, 0, 0);
    }
    int permRes(const vector<vector<int>>& dp, 
                vector<int>& memo, 
                int state, 
                int idx) 
    {
        if (idx == dp.size()) {
            return 0;
        }
        if (memo[state] != 0) {
            return memo[state];
        }
        int tmp = INT_MAX;
        for (auto j = 0; j < dp[0].size(); j++) {
            if ((state & (1 << j)) == 0) {
                tmp = min(tmp, dp[idx][j] + permRes(dp, memo, state | (1<<j), idx + 1));
            }
        }
        memo[state] = tmp;
        return memo[state];
    }
};
```

#### 示例代码 (java)
```java

```

#### 示例代码 (python)
```python
    def assignBikes(self, workers: List[List[int]], bikes: List[List[int]]) -> int:
        dic = {}
        
        def helper(a,b):
            return abs(a[0] - b[0]) + abs(a[1] - b[1])
        
        def dfs(p, arr):
            if p == len(workers):
                return 0
            if (p, tuple(arr)) in dic:
                return dic[(p, tuple(arr))]
            temp = float('inf')
            for i in range(len(arr)):
                if arr[i] == 0:
                    temp = min(temp,  helper(bikes[i], workers[p]) + dfs(p + 1, arr[:i] + [1] + arr[i + 1:]))
            dic[(p, tuple(arr))] = temp
            return temp
        
        ans = dfs(0, [0 for _ in range(len(bikes))])
        return ans
```

#### 复杂度分析
`M`为`workers`数量，`N`为`bikes`数量
时间复杂度: `state`一共有`2^N`,每个`state`至多被计算一遍，因此这里是O(2^N)
空间复杂度: 距离的`cache`可以忽略不计，主要开销在`memo`上，因此这里是O(2^N)

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/GSc-F_jlYWk)，欢迎关注！