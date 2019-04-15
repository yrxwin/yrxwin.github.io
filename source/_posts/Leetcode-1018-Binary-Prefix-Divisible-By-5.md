---
title: '[Leetcode 1018] Binary Prefix Divisible By 5'
categories:
  - leetcode
author: '大猩猩'
date: 2019-04-11 21:25:48
tags: ['Array']
keywords:
description:
---

#### 原题说明
Given an array `A` of `0`s and `1`s, consider `N_i`: the `i-th` subarray from `A[0]` to `A[i]` interpreted as a binary number (from most-significant-bit to least-significant-bit.)

Return a list of booleans `answer`, where `answer[i]` is true if and only if `N_i` is divisible by `5`.

**Example 1:**
{% blockquote %}
**Input:** `[0,1,1]`
**Output:** `[true,false,false]`
**Explanation:** The input numbers in binary are 0, 01, 011; which are 0, 1, and 3 in base-10.  Only the first number is divisible by 5, so answer[0] is true.
{% endblockquote %}
**Example 2:**
{% blockquote %}
**Input:** `[1,1,1]`
**Output:** [false, false, false]
{% endblockquote %}
**Example 3:**
{% blockquote %}
**Input:** `[0,1,1,1,1,1]`
**Output:** `[true,false,false,false,true,false]`
{% endblockquote %}
**Example 4:**
{% blockquote %}
**Input:** `[1,1,1,0,1]`
**Output:** `[false,false,false,false,false]`
{% endblockquote %}
 
**Note:**
1. `1 <= A.length <= 30000`
2. `A[i] is 0 or 1`

<!--more-->

#### 解题思路
题目要求检查从`A[0]` 到 `A[i]` `(0 <= i < A.size())`的字符串，对应的二进制数是否能被5整除。

我们按顺序依次检查二进制对应的数是否能被5整除。

这里有一个小技巧：两个数的和对5的余数，等于它们各自对5的余数的和对5的余数。运用这个事实，我们可以防止整数溢出。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    vector<bool> prefixesDivBy5(vector<int>& A) {
        vector<bool> ans;
        int tmp = 0;
        for (auto a : A) {
            tmp = (tmp * 2 + a) % 5;
            if (tmp == 0) {
                ans.push_back(true);
            }
            else {
                ans.push_back(false);
            }
        }
        return ans;
    }
};
```

#### 复杂度分析
时间复杂度: O(N)
空间复杂度: O(N)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/-sPywZWtmK4)，欢迎关注！