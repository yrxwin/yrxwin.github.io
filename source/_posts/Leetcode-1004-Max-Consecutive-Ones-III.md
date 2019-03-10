---
title: '[Leetcode 1004] Max Consecutive Ones III'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2019-03-09 23:24:29
tags:
keywords:
description:
---
#### 原题说明
Given an array `A` of 0s and `1`s, we may change up to `K` values from `0` to `1`.

Return the length of the longest (contiguous) subarray that contains only `1`s. 

**Example 1:**
{% blockquote %}
**Input:** A = `[1,1,1,0,0,0,1,1,1,1,0], K = 2`
**Output:** `6`
**Explanation:**
[1, 1, 1, 0, 0, **<u>1</u>**, <u>1</u>, <u>1</u>, <u>1</u>, <u>1</u>, **<u>1</u>**]
Bolded numbers were flipped from `0` to `1`.  The longest subarray is underlined.
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** `A = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], K = 3`
**Output:** `10`
**Explanation:** 
[0, 0, <u>1</u>, <u>1</u>, <u>**1**</u>, <u>**1**</u>, <u>1</u>, <u>1</u>, <u>1</u>, <u>**1**</u>, <u>1</u>, <u>1</u>, 0, 0, 0, 1, 1, 1, 1]
Bolded numbers were flipped from 0 to 1.  The longest subarray is underlined.
{% endblockquote %}

**Note:**
- `1 <= A.length <= 20000`
- `0 <= K <= A.length`
- `A[i] is 0 or 1`

#### 解题思路
使用双指针解题：
- `zeros`用来记录我们考察的子序列中将`0`变为`1`的次数。
- 用`right`指针从左向右遍历数组`A`，`right`指针表示当前我们考察的子序列的最右位置，如果遇到`0`，则`zeros++`，表示增加一次翻转。
- `left`指针用来记录当前子序列最左的位置，如果发现`zeros > K`, 则将`left`向右推进，直到`zeros <= K`。
推进过程中，如果遇到`0`，则`zeros--`，表示当前的`0`不在考察子序列当中。
- `left`指针实际上一直在追赶`right`。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int longestOnes(vector<int>& A, int K) {
        int left = 0;
        int zeros = 0;
        int ans = 0;
        for (auto right = 0; right < A.size(); ++right) {
            if (A[right] == 0)
                zeros++;
            while (zeros > K) {
                if (A[left] == 0) {
                    zeros--;
                }
                left++;
            }
            ans = max(right - left + 1, ans);
        }
        return ans;
    }
};
```

#### 复杂度分析
时间复杂度: `O(n)`
空间复杂度: `O(1)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/g1eMPnclJfU)，欢迎关注！