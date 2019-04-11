---
title: '[Leetcode 1014] Best Sightseeing Pair'
categories:
  - leetcode
author: '大猩猩'
date: 2019-04-10 21:37:40
tags:
keywords:
description:
---

#### 原题说明

Given an array `A` of positive integers, `A[i]` represents the value of the `i` - th sightseeing spot, and two sightseeing spots `i` and `j` have distance `j - i` between them.

The score of a pair (`i < j`) of sightseeing spots is (`A[i] + A[j] + i - j`) : the sum of the values of the sightseeing spots, minus the distance between them.

Return the maximum score of a pair of sightseeing spots.

**Example 1:**
{% blockquote %}
**Input:** `[8, 1, 5, 2, 6]`
**Output:** `11`
**Explanation:** `i = 0, j = 2, A[i] + A[j] + i - j = 8 + 5 + 0 - 2 = 11`.
{% endblockquote %}
 
**Note:**
1. `2 <= A.length <= 50000`
2. `1 <= A[i] <= 1000`

#### 解题思路
这道题的题意概括，就是对于数组中的两个下标i, j，求A[i] + A[j] + i - j最大值.
最直接的思路就是暴力解法，但是时间复杂度是O(n^2), 显然不可取。
    
为了给出更优的解法，我们首先变换目标公式从 `A[i] + A[j] + i - j` 变为 `A[i] + i + A[j] - j`。这样，我们可以在每个位置j，记录下其对应的比 `i < j` 时， `A[i] + i`的最大值。这样遍历 `A`，求出每个位置`j`对应的 `A[i] + A[j] + i - j`的最大值。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int maxScoreSightseeingPair(vector<int>& A) {
        int pre = 0; // 比j小的index
        int res = -INT_MAX;
        for (auto i = 1; i < A.size(); i++) {
            res = max(A[i] - i + A[pre] + pre, res);
            if (A[i] + i > A[pre] + pre) {
                pre = i;
            }
        }
        return res;
    }
};
```

#### 复杂度分析
时间复杂度: O(n)
空间复杂度: O(1)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/GSc-F_jlYWk)，欢迎关注！