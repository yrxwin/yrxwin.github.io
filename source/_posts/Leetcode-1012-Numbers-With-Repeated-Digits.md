---
title: '[Leetcode 1012] Numbers With Repeated Digits'
categories:
  - leetcode
author: '大猩猩'
date: 2019-04-07 17:28:35
tags: ['Math', 'Google']
keywords:
description:
---

#### 原题说明
Given a positive integer N, return the number of positive integers less than or equal to N that have at least 1 repeated digit.

**Example 1:**
{% blockquote %}
**Input:** `20`
**Output:** `1`
**Explanation:** The only positive number `(<= 20)` with at least `1` repeated digit is `11`.
{% endblockquote %}
**Example 2:**
{% blockquote %}
**Input:** `100`
**Output:** `10`
**Explanation:** The positive numbers `(<= 100)` with atleast `1` repeated digit are `11, 22, 33, 44, 55, 66, 77, 88, 99`, and `100`.
{% endblockquote %}
**Example 3:**
{% blockquote %}
**Input:** `1000`
**Output:** `262`.
{% endblockquote %}
 
**Note:**
1. `1 <= N <= 10^9`

#### 解题思路
题目要求求出比`N`小，同时至少存在一个重复数字的正整数的个数。运用`brute force`方法直接计算满足题目要求的数会有超时的问题，时间复杂度是`O(N)`，不满足要求。更好的方法是先求出所有不满足要求的数的个数`res`，再用`N`减去`res`，反过来得出答案。

这里，不满足题目要求的数可以分为两类;
1. 第一类是位数比`N`小的数，同时数字各不相同
2. 第二类是位数与`N`相同的，比N小，同时数字各不相同。

这两类数就包含了所有不大于N，同时数字各不相同的数，而剩下的数就是至少包含一个相同数字，且不大于`N`的数。

同时，我们需要一个辅助函数`helper`,它的作用是用来求出`m`个不同数字组成长度是`n`位的数的个数。

第一类数的求解相对简单，最高位的可能是`1~9`一共9中可能，之后可以直接调用`helper`方便求解。

第二类数，需要分别对不同的相同前缀做分类计算。在确定相同前缀之后，再次调用`helper`可以求出对应的数的个数。

#### 示例代码 (cpp)
```cpp
/*
example: 8765

the number with digits < N

XXX
XX
X

number with same prefix

1XXX ~ 7XXX
80XX ~ 86XX
870X ~ 875X
8760 ~ 8765
*/

class Solution {
public:
    int numDupDigitsAtMostN(int N) {
        int N_copy = N + 1;
        int res = 0;
        vector<int> arr;
        while (N_copy > 0) {
            arr.insert(arr.begin(), N_copy % 10);
            N_copy = N_copy / 10;
        }
        int n = arr.size();
        // count the number with digits < N
        for (int i = 1; i < n; ++i) {
            res += 9 * helper(9 , i - 1);
        }
        // cout the number with same prefix
        unordered_set<int> seen;
        for (int i = 0; i < n; ++i) {
            for (int j = i == 0 ? 1 : 0; j < arr[i]; ++j) {
                if (!seen.count(j)) {
                    res += helper(9 - i, n - i - 1);
                }
            }
            if (seen.count(arr[i])) { //相同前缀中有相同的数字，不符合要求，不用继续计算之后的前缀了
                break;
            }
            seen.insert(arr[i]);
        }
        return N - res;
    }
    // helper函数，返回由m个digit，n位数位可以组成的数的个数
    // m--可以用于组合数字的digit个数
    // n--需要组成的位数
    int helper(int m, int n) {
        return n == 0 ? 1 : m * helper(m - 1, n - 1);
    }
};
```
#### 复杂度分析
时间复杂度: O(log N)
空间复杂度: O(log N)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://www.youtube.com/watch?v=Xi-YfchDa5U&feature=youtu.be)，欢迎关注！