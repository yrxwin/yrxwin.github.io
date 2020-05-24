---
title: '[Leetcode 1043] Partition Array for Maximum Sum'
categories:
  - leetcode
author: '猩猩管理员'
date: 2020-05-24 19:10:29
tags: ['Facebook', 'Graph']
keywords: ['Facebook', 'Graph']
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given an integer array&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A</code>, you partition the array into (contiguous) subarrays of length at most&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">K</code>.&nbsp; After partitioning, each subarray has their values changed to become the maximum value of that subarray.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Return the largest sum of the given array after partitioning.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>A = <span id="example-input-1-1">[1,15,7,9,2,5,10]</span>, K = <span id="example-input-1-2">3</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">84
</span><span style="font-weight: bolder;">Explanation</span>: A becomes [15,15,15,9,10,10,10]</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= K &lt;= A.length&nbsp;&lt;= 500</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0 &lt;= A[i] &lt;= 10^6</code></li></ol>
<!--more-->

#### 解题思路
动态规划，用`p[i]`来表示`A`中前`i`个元素能够得到的最大值。
对于下一位`dp[i + 1]`(即新加入元素`A[i]`)来说，我们将以`A[i]`结尾的切分(partition)的长度从`len = 1`开始向前遍历，直到达到长度上限`K`：`len = K`
或者达到最左边：`i - len + 1 = 0`

对于每一个以`A[i]`结尾的切分长度`len`，我们首先计算该切分中的最大值（即从`i`到`i - len + 1`之间`A`的最大值），用`max_value`表示：
`max_value = max(max_value, A[i - len + 1]);`
然后将`dp[i + 1]`的值更新为：
`max(dp[i + 1], max_value * len + dp[i - len + 1])`

返回dp数组最后一个值：`dp[A.size()]`

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int maxSumAfterPartitioning(vector<int>& A, int K) {
        // 最左边dp[0]始终为0，可以不用判断最左边的边界条件
        vector<int> dp(A.size() + 1, 0);
        // i为A的index
        for (int i = 0; i < A.size(); ++i) {
            int max_value = 0;
            for (int len = 1; len <= K && i - len + 1 >= 0; ++len) {
                max_value = max(max_value, A[i - len + 1]);
                // dp的index相比A的index右移一格
                dp[i + 1] = max(dp[i + 1], max_value * len + dp[i - len + 1]);
            }
        }
        return dp[A.size()];
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int maxSumAfterPartitioning(int[] A, int K) {
        int N = A.length, dp[] = new int[N];
        for (int i = 0; i < N; ++i) {
            int curMax = 0;
            for (int k = 1; k <= K && i - k + 1 >= 0; ++k) {
                curMax = Math.max(curMax, A[i - k + 1]);
                dp[i] = Math.max(dp[i], (i >= k ? dp[i - k] : 0) + curMax * k);
            }
        }
        return dp[N - 1];
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def maxSumAfterPartitioning(self, A: List[int], K: int) -> int:
        N = len(A)
        dp = [0] * (N + 1)
        for i in range(N):
            curMax = 0
            for k in range(1, min(K, i + 1) + 1):
                curMax = max(curMax, A[i - k + 1])
                dp[i] = max(dp[i], dp[i - k] + curMax * k)
        return dp[N - 1]
```

#### 复杂度分析
时间复杂度: `O(N * K)`, `N`为数组`A`的长度
空间复杂度: `O(N)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/OKNR9xE-Luo)，欢迎关注！