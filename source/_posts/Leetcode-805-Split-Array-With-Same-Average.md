---
title: '[Leetcode 805] Split Array With Same Average'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-12 12:14:25
tags: [Array]
keywords: [Array]
description:
---

#### 原题说明
In a given integer array A, we must move every element of A to either list B or list C. (B and C initially start empty.)

Return true if and only if after such a move, it is possible that the average value of B is equal to the average value of C, and B and C are both non-empty.

	Example :
	Input: 
	[1,2,3,4,5,6,7,8]
	Output: true	
	Explanation: We can split the array into [1,4,5,8] and [2,3,6,7], and both of them have the average of 4.5.

**Note**:

 - The length of A will be in the range [1, 30].
 - A[i] will be in the range of [0, 10000].

#### 解题思路
给定一个数组，题目要求判断能否把数组分成两个数组，是它们的平均值相同。

我们说明以下三点事实：

 - 如果存在这样的分组，它们各自的平均值一定等于原数组的平均值，反之则不存在
 - 我们只要找到任意一个分组，使得它的平均值等于原数组的平均值，就可以判定剩余数组成的数组的平均值也与其相等，从在给出存在的判断
 - 如果存在这样的分组，平均值（原数组以及分类后的两个数组的平均值都相等）乘以任意数组的长度，都一定是一个整数。这点会简化我们的计算。

因此，我们可以用上述三点事实，来给出我们的算法。因为是分成两个数组，所以必定有一个数组的长度不超过原数组长度的一般。枚举从1到原数组长度的一半`k`，对其中乘以平均值为整数的那些值`sum`，我们用递归的方法找出是否能从原数组中挑选出给`k`个元素，使得它们的和等于`sum`。如果能找出其中任意一个，存在这种分类，反之则不存在。

为了防止`TLE`,我们用一个`map`来记录遍历过情况。`map`的键是一个元组（target，k），表示需要寻找的目标和元素个数，`map`的值是`i`,表示从第`i`个元组之后找。这样如果新的`i`比`map`中对应键的值来的大，说明这种情况已经遍历过，则无需重复遍历。否则需要更新map，并继续搜索。

#### 示例代码 (python)
```python
class Solution:
    def splitArraySameAverage(self, A):
        """
        :type A: List[int]
        :rtype: bool
        """
        visit = {} # map 记录搜索过得信息
        n, s = len(A), sum(A)
        return any(self.find(A, s * k / n, k, 0, visit) for k in range(1, int(n /2) + 1) if s * k % n == 0)
    
    def find(self, A, target, k, i, visit):
        if (target,k) in visit and visit[(target,k)] <= i:
            return False
        if k == 0:
            return target == 0
        if k + i > len(A):
            return False
        ans = self.find(A, target - A[i], k - 1, i + 1, visit) or self.find(A, target, k, i+ 1, visit)
        if not ans:
            visit[(target, k)] = min(visit.get((target,k), len(A)), i)
        return ans
```

#### 复杂度分析
我们用了一个`map`来记录一些中间过程，理论上它的空间复杂度会是组合树的全排列，约定于`O(2^n)`。但实际情况会远远小于这个估计。对于时间复杂度，也是同样的情况，由于对整数性的要求和`map`的存在，会省去很多不必要的计算。
时间复杂度: `O(2^n)`
空间复杂度: `O(2^n)`

#### 归纳总结
这题如果使用暴力搜索，一定会超时。利用两个数组平均值相等的性质，可以做的剪枝`dfs`。同时我们用一个`map`来记录已经搜索的信息，进一步避免了不必要的计算。