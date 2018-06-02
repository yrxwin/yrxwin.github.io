---
title: '[Leetcode 410] Split Array Largest Sum'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-22 19:35:29
tags: [Binary Search, Dynamic Programming, Facebook, Baidu]
keywords: [Binary Search]
description:
---

#### 原题说明
Given an array which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays. Write an algorithm to minimize the largest sum among these m subarrays.

**Note**:

If n is the length of array, assume the following constraints are satisfied:

 - 1 ≤ n ≤ 1000
 - 1 ≤ m ≤ min(50, n)
 
**Examples**:

	Input:	
	nums = [7,2,5,10,8]
	m = 2

	Output:
	18

	Explanation:
	There are four ways to split nums into two subarrays. 
	The best way is to split it into [7,2,5] and [10,8], where the largest sum among the two subarrays is only 18.

#### 解题思路
本题给出一个数组`nums`和一个整数`m`,要求把数组`nums`分成连续的`m`份，找到所有分类中，子数组最大和的最小值。

显然，最简单的方法是可以使用`DFS`做暴力搜索，但是这样时间复杂度相当于从`n-1`个元素中抽取`m-1`个元素，为`O(n^m)`，会 TLE。

因为子数组本身是连续的，我们可以想到用动态规划 [Dyanmic Programming](\tags\Dynamic-Programming) 来设计解法。定义`f[i][j]`为把数组 `nums[0,1,..,i]`分成`j`份后最大子数组和的最小值。显然，我们会有以下公式:
`f[i][j] = max(f[k][j-1],nums[k+1]+...+nums[i) for all valid k`
用动态规划，从`f[0][0]`出发，最后返回`f[n][m]` 即可。时间复杂度为`O(n^2*m)`，并且空间复杂度为`O(n*m)`。

这里，介绍一种更好的算法，运用 [Binary Search](\tags\Binary-Search) 。考虑到数组元素都是非负整数，所以答案也一定是整数。同时，答案一定存在于 0 到 数组元素和`sum of array`之间。因此，我们只需能够判断，对于任意一个整数`mid`，是否存在一个分类使得`nums`能分成`m`份，并且最大子数组的和不超过`mid`。如果能，我们下调`Binary Search`，如果不能，我们上调`Binary Search`。

判断的算法也很简单，我们用贪心算法`Greedy`。用`tmpsum`记录当前子数组的和，用`count`记录当前的分类数。如果当前元素`num`加上`tmpsum`不超过`mid`，更新`tmpsum = tmpsum + num`；如果超过`mid`，更新`tmpsum = 0`并更新`count = count + 1`。遍历完数组`nums`， 当`count <= m`，返回 `True`，反之返回`False`。

#### 示例代码 (python)
```python
class Solution:
    def splitArray(self, nums, m):
        """
        :type nums: List[int]
        :type m: int
        :rtype: int
        """
        low, high = 0, sum(nums)
        while low + 1 < high:
            mid = int(low + (high - low) /2)
            if self.determinTrue(mid, nums, m):
                high = mid
            else:
                low = mid
        return i if self.determinTrue(low, nums, m) else high
    
    def determinTrue(self, target, nums, m):
        n = len(nums)
        tmpsum, count = 0, 1
        for num in nums:
            if num > target:
                return False
            if tmpsum + num <= target:
                tmpsum += num
            else:
                tmpsum = num
                count += 1
        return count <= m
```

#### 复杂度分析
每次贪心算法时间复杂度为`O(n)`，同时`Binary Search`需要的时间复杂度是`O(log(sum of array))`。因此总的时间复杂度为`O(n*(log(sum of array)))`。而空间复杂度为`O(n)`。

- 时间复杂度: `O(n*(log(sum of array)))`
- 空间复杂度: `O(n)`

#### 归纳总结
当数组的和不过分大时，一般情况下，[Binary Search](\tags\Binary-Search) 的时间复杂度都会优于[Dyanmic Programming](\tags\Dynamic-Programming)。当然，这里能使用 `Binary Search`的前提是数组元素都是非负整数而`Dynamic Programming`则没有这个限制 。