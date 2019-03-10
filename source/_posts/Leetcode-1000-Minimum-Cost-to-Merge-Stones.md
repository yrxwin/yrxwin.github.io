---
title: '[Leetcode 1000] Minimum Cost to Merge Stones'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-03-09 22:01:14
tags: ['Google', 'Dynamic Programming']
keywords: ['Google', 'Dynamic Programming']
description:
---
#### 原题说明
There are `N` piles of stones arranged in a row.  The i-th pile has `stones[i]` stones.

A move consists of merging **exactly K consecutive** piles into one pile, and the cost of this move is equal to the total number of stones in these K piles.

Find the minimum cost to merge all piles of stones into one pile.  If it is impossible, return `-1`.


**Example 1:**
{% blockquote %}
**Input:** `stones = [3,2,4,1], K = 2`
**Output:** `20`
**Explanation:**
We start with `[3, 2, 4, 1]`.
We merge `[3, 2]` for a cost of 5, and we are left with `[5, 4, 1]`.
We merge `[4, 1]` for a cost of 5, and we are left with `[5, 5]`.
We merge `[5, 5]` for a cost of 10, and we are left with `[10]`.
The total cost was `20`, and this is the minimum possible.
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** `stones = [3,2,4,1], K = 3`
**Output:** `-1`
**Explanation:** After any merge operation, there are `2` piles left, and we can't merge anymore.  So the task is impossible.
{% endblockquote %}

**Example 3:**
{% blockquote %}
**Input:** `stones = [3,5,1,2,6], K = 3`
**Output:** `25`
**Explanation:** 
We start with `[3, 5, 1, 2, 6]`.
We merge `[5, 1, 2]` for a cost of 8, and we are left with `[3, 8, 6]`.
We merge `[3, 8, 6]` for a cost of 17, and we are left with `[17]`.
The total cost was 25, and this is the minimum possible.
{% endblockquote %}
 
**Note:**
- `1 <= stones.length <= 30`
- `2 <= K <= 30`
- `1 <= stones[i] <= 100`

#### 解题思路
**动态规划：**
`dp[i][j][k]` := 将`i`到`j`合并成`k`堆的最小cost
**初始状态：**
`dp[i][j][k] = 0 if i==j and k == 1 else inf`
**最终返回：** 
`dp[0][n-1][1]`
**状态转移方程:**
1. `k >= 2`
   `dp[i][j][k] = min{dp[i][m][1] + dp[m+1][j][k-1]}` for all `i <= m < j`
2. `k == 1`
   `dp[i][j][1] = dp[i][j][K] + sum of (stones[i] to stones[j])`

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int mergeStones(vector<int>& stones, int K) {
        const int n = stones.size();
        if ((n - K) % (K - 1))
            return -1;
        // calculate the sum from 0 to i        
        vector<int> sumStones(n + 1, 0);
        for (auto i = 0; i < n; ++i) {
            sumStones[i + 1] = sumStones[i] + stones[i]; 
        }
        // initialize the 3d vector dp
        vector<vector<vector<int>>> dp(n, vector<vector<int>>(n, vector<int>(K + 1, 1e9)));
        for (int i = 0; i < n; ++i) {
            dp[i][i][1] = 0;
        }
        // compute the transition functions
        for (auto stepLen = 2; stepLen <= n; ++stepLen) {
            for (auto i = 0; i <= n - stepLen; ++i) {
                int j = i + stepLen - 1;
                for (auto k = 2; k <= K; k++) {
                    for ( auto m = i; m < j; m += K - 1) {
                        dp[i][j][k] = min(dp[i][j][k], dp[i][m][1] + dp[m + 1][j][k - 1]);
                    }
                }
                dp[i][j][1] = dp[i][j][K] + sumStones[j + 1] - sumStones[i];
            }
        }
        return dp[0][n - 1][1];
    }
};
```

#### 复杂度分析
时间复杂度: `O(n^3)`
空间复杂度: `O(n^2 * K)`

#### 归纳总结
这道题还有更加优化的动态规划解法，但是思路不是非常直接，面试时也不太会要求掌握，同学们如果希望看到讲解，可以留言告诉我们。
我们在**Youtube**上更新了[视频讲解](https://youtu.be/F9FJEOXNn9M)，欢迎关注！