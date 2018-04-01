---
title: '[Leetcode 162] Find Peak Element'
categories:
  - leetcode
date: 2018-03-30 01:48:48
tags: [Google, Microsoft, Array, Binary Search]
author: 大猩猩

---
#### 原题说明
A peak element is an element that is greater than its neighbors.

Given an input array where `num[i]` ≠ `num[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that `num[-1]` = `num[n]` = `-∞`.

For example, in array `[1, 2, 3, 1]`, `3`is a peak element and your function should return the index number `2`.

Note:

Your solution should be in logarithmic complexity.


#### 解题思路
题目要求给出一个数列中峰值的位置。注意的是数列中可能存在若干个峰值，我们只要给出其中任意一个的位置即可。举个例子：数列 `[0,0,0,4,0,0,5,0,0]`， 它的峰值分别是`4`,`5`，因此答案应该是`3`或者`6`。

最直接的想法用暴力搜索，直接遍历一遍数组，给出最大值得位置即可。这样时间复杂度是 `O(n)`。

如果我们想要降低时间复杂度到`O(log n)`，直觉上可以用二分搜索（`Binary Search`）。若是只有一个峰值，设最左边位置为`low`，最右边位置为high，这样中间位置为 `mid = (high + low) / 2`。判断准则为，若是 `num[mid] < num[mid+1]`, 我们就让`low = mid`，反之`high = mid`， 直到 `low + 1`等于`high`,终止二分。

有趣的是，如果存在若干个峰值，我们也不需要对以上算法进行改动。因为进过若干次的二分，在位置`low`和`high`之间终归会存在一个且仅有一个峰值。

#### 示例代码 (PYTHON)

```python
class Solution:
    def findPeakElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        low, high = 0, len(nums) - 1
        while low < high:
            mid = int(low + (high - low) / 2)
            if nums[mid] > nums[mid + 1]:
                high = mid
            else:
                low = mid + 1
        return low
```

#### 示例代码 (CPP)

```cpp
class Solution {
public:
    int findPeakElement(const vector<int>& nums) {
        int low = 0; 
        int high = nums.size() - 1;
        while (low + 1 < high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] < nums[mid + 1]) 
                low = mid;
            else
                high = mid;
        }
        return nums[low] > nums[high] ? low : high;
    }
};
```

#### 复杂度分析
典型的二分法算法，并且只需要 `low`, `high`, `mid` 3个变量，所以时间和空间复杂度分别为：

- 时间复杂度：O(log n)
- 空间复杂度：O(1)
 
#### 总结归纳：
这是一道经典的二分算法题（`Binary Search`），一般如果要求在对数时间复杂度下完成，我们可以考虑使用二分搜索。今天的解题就到这里了，种香蕉树去了：）


