---
title: '[Leetcode 1031] Maximum Sum of Two Non-Overlapping Subarrays'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-04-28 18:41:41
tags: ['Array']
keywords: ['Array']
description:
---
#### 原题说明
Given an array `A` of non-negative integers, return the maximum sum of elements in two non-overlapping (contiguous) subarrays, which have lengths `L` and `M`.  (For clarification, the L-length subarray could occur before or after the M-length subarray.)

Formally, return the largest `V` for which `V = (A[i] + A[i+1] + ... + A[i+L-1]) + (A[j] + A[j+1] + ... + A[j+M-1])` and either:
`0 <= i < i + L - 1 < j < j + M - 1 < A.length`, or
`0 <= j < j + M - 1 < i < i + L - 1 < A.length`.
 
**Example 1:**
{% blockquote %}
**Input:** `A = [0,6,5,2,2,5,1,9,4], L = 1, M = 2`
**Output:** `20`
**Explanation:** One choice of subarrays is `[9]` with length `1`, and `[6,5]` with length `2`.
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** `A = [3,8,1,3,2,1,8,9,0], L = 3, M = 2`
**Output:** `29`
**Explanation:** One choice of subarrays is `[3,8,1]` with length `3`, and `[8,9]` with length `2`.
{% endblockquote %}

**Example 3:**
{% blockquote %}
**Input:** `A = [2,1,5,6,0,9,5,0,3,8], L = 4, M = 3`
**Output:** `31`
**Explanation:** One choice of subarrays is `[5,6,0,9]` with length `4`, and `[3,8]` with length `3`.
{% endblockquote %}
 
**Note:**
1. `L >= 1`
2. `M >= 1`
3. `L + M <= A.length <= 1000`
4. `0 <= A[i] <= 1000`

<!--more-->

#### 解题思路
动态规划
凡是要求数组某一段的和，要想到用`pre_sum`，`pre_sum[i]`表示指数`i`之前左右数的和。
这样我们要求`A[i]`到`A[j]`之间所有数的和，就可以用`pre_sum[j] - pre_sum[i - 1]`
回到这道题，我们第一遍遍历数组A求pre_sum。

第二遍遍历，指数为`i`，用`max_L`记录指数`i - M`之前的最大连续`L`个数之和，
每次更新`max_L`为`max(max_L, pre_sum[i - M] - pre_sum[i - L - M])`
`max_L + pre_sum[i] - pre_sum[i - M]`表示以`i`结尾最后连续`M`个数，与之前最大的连续`L`个数的和。
同理`max_M + pre_sum[i] - pre_sum[i - L]`就表示以i结尾最后连续`L`个数，与之前最大的连续`M`个数的和。
取其中较大的与最终要返回的值`res`比较，并更新即可。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int maxSumTwoNoOverlap(vector<int>& A, int L, int M) {
        if (A.size() < L + M) {
            return 0;
        }
        vector<int> pre_sum = A;
        for (int i = 1; i < A.size(); ++i) {
            pre_sum[i] += pre_sum[i - 1];
        }
        int res = pre_sum[L + M - 1], max_L = pre_sum[L - 1], max_M = pre_sum[M - 1];
        for (int i = L + M; i < A.size(); ++i) {
            max_L = max(max_L, pre_sum[i - M] - pre_sum[i - L - M]);
            max_M = max(max_M, pre_sum[i - L] - pre_sum[i - L - M]);
            res = max(res, max(max_L + pre_sum[i] - pre_sum[i - M], max_M + pre_sum[i] - pre_sum[i - L]));
        }
        return res;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int maxSumTwoNoOverlap(int[] A, int L, int M) {
        for (int i = 1; i < A.length; ++i)
            A[i] += A[i - 1];
        int res = A[L + M - 1], Lmax = A[L - 1], Mmax = A[M - 1];
        for (int i = L + M; i < A.length; ++i) {
            Lmax = Math.max(Lmax, A[i - M] - A[i - L - M]);
            Mmax = Math.max(Mmax, A[i - L] - A[i - L - M]);
            res = Math.max(res, Math.max(Lmax + A[i] - A[i - M], Mmax + A[i] - A[i - L]));
        }
        return res;
    }
}
```

#### 示例代码 (python)
```python
class Solution(object):
    def maxSumTwoNoOverlap(self, A, L, M):
        """
        :type A: List[int]
        :type L: int
        :type M: int
        :rtype: int
        """
        for i in xrange(1, len(A)):
            A[i] += A[i - 1]
        res, Lmax, Mmax = A[L + M - 1], A[L - 1], A[M - 1]
        for i in xrange(L + M, len(A)):
            Lmax = max(Lmax, A[i - M] - A[i - L - M])
            Mmax = max(Mmax, A[i - L] - A[i - L - M])
            res = max(res, Lmax + A[i] - A[i - M], Mmax + A[i] - A[i - L])
        return res
```

#### 复杂度分析
时间复杂度: `O(N)`
空间复杂度: `O(N)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/XTGEbhZmqCY)，欢迎关注！