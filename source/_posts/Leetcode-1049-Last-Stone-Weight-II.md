---
title: '[Leetcode 1049] Last Stone Weight II'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-06-07 23:28:16
tags: ['Amazon', 'Dynamic Programming']
keywords: ['Amazon', 'Dynamic Programming']
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">We have a collection of rocks, each rock has a positive integer weight.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Each turn, we choose&nbsp;<span style="font-weight: bolder;">any two rocks</span>&nbsp;and smash them together.&nbsp; Suppose the stones have weights&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">x</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">y</code>&nbsp;with&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">x &lt;= y</code>.&nbsp; The result of this smash is:</p><ul style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li>If&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">x == y</code>, both stones are totally destroyed;</li><li>If&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">x != y</code>, the stone of weight&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">x</code>&nbsp;is totally destroyed, and the stone of weight&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">y</code>&nbsp;has new weight&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">y-x</code>.</li></ul><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">At the end, there is at most 1 stone left.&nbsp; Return the&nbsp;<span style="font-weight: bolder;">smallest possible</span>&nbsp;weight of this stone (the weight is&nbsp;0 if there are no stones left.)</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;<span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>[2,7,4,1,8,1]
<span style="font-weight: bolder;">Output: </span>1
<span style="font-weight: bolder;">Explanation: </span>
We can combine 2 and 4 to get 2 so the array converts to [2,7,1,8,1] then,
we can combine 7 and 8 to get 1 so the array converts to [2,1,1,1] then,
we can combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we can combine 1 and 1 to get 0 so the array converts to [1] then that's the optimal value.&nbsp;</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= stones.length &lt;= 30</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= stones[i] &lt;= 100</code></li></ol>
<!--more-->

#### 解题思路
假设有三个石头`x1，x2, x3`, 无论如何组合，最终都会成为三个数之间的加减法
比如如果先合并`x1`，`x2`,再与`x3`合并，则最终的重量为`x3 - x1 + x2` (假设`x1 > x2, x3 > (x1 - x2)`)
所以这道题相当于将数组分为两组，两组分别求和为`S1`和`S2`，并希望其差值(`S2 - S1 if S2 >= S1`)最小:
`S1 + S2 = total_weight`
`if S1 <= S2 => S2 - S1 = total_weight - S1 - S1 = total_weight - 2 * S1`
所以相当于我们希望较小的一半石头的重量和尽可能接近 `total_weight / 2`
 
我们通过动态规划来求解这道题，建立一个数组`dp`来记录石头重量之和的所有可能值:
`dp[i]`为`true`如果我们可以使得一组`stones`的重量之和`S1`等于`i`，反之则为`false`
我们遍历`stones`数组，用`sum_weight`来记录当前遍历到的所有重量之和，
我们判断加入当前的石头重量`stone_weight`后，从`sum_weight`到`stone_weight`之间的每一个值`weight`是否可能成为`S1`的值：
如果`dp[weight - stone_weight]`为`true`，则对应的`dp[weight]`也设为`true`。
遍历`stones`完成后，从`weight = sum_weight / 2`开始逐渐减小，如果`dp[weight] = true`,
则当前`weight`即我们希望寻找的`S1`的值，所以返回对应的`total_weight - 2 * weight`即可。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int lastStoneWeightII(vector<int>& stones) {
        // 由于限制条件：
        // 1 <= stones.length <= 30
        // 1 <= stones[i] <= 100
        // 所以石头重量总和最多为 30 * 100 = 3000
        vector<bool> dp(1501, false);
        dp[0] = true;
        int sum_weight = 0;
        for (const auto stone_weight : stones) {
            sum_weight += stone_weight;
            // 一定要用--，而不是++，不然同一块石头的重量会被视作可以反复利用
            // 比如如果stone_weight = 1, 用++的话，会使得dp的所有小于sum_weight的值都为true
            for (int weight = sum_weight; weight >= stone_weight; --weight) {
                if (dp[weight - stone_weight]) {
                    dp[weight] = true;
                }
            }
        }
        for (int weight = sum_weight / 2; weight >= 0; --weight) {
            if (dp[weight]) {
                return sum_weight - 2 * weight;
            }
        }
        return 0;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int lastStoneWeightII(int[] A) {
        boolean[] dp = new boolean[1501];
        dp[0] = true;
        int sumA = 0;
        for (int a : A) {
            sumA += a;
            for (int i = Math.min(1500, sumA); i >= a; --i)
                dp[i] |= dp[i - a];
        }
        for (int i = sumA / 2; i >= 0; --i)
            if (dp[i]) return sumA - i - i;
        return 0;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        dp = {0}
        sumA = sum(stones)
        for stone in stones:
            dp |= {stone + i for i in dp}
        return min(abs(sumA - i - i) for i in dp)
```

#### 复杂度分析
时间复杂度: `O(N)`
空间复杂度: `O(total_weight)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/oPgLkIwq9l0)，欢迎关注！