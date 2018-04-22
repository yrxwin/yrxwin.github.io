---
title: '[Leetcode 719] Find K-th Smallest Pair Distance'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-17 13:01:07
tags: [Array, Binary Search, Heap, Google]
keywords: [Array]
description:
---

#### 原题说明
Given an integer array, return the k-th smallest distance among all the pairs. The distance of a pair (A, B) is defined as the absolute difference between A and B.

	**Example 1**:
	Input:
	nums = [1,3,1]
	k = 1
	Output: 0 
	Explanation:
	Here are all the pairs:
	(1,3) -> 2
	(1,1) -> 0
	(3,1) -> 2
	Then the 1st smallest distance pair is (1,1), and its distance is 0.

**Note**:

 1. `2 <= len(nums) <= 10000.`
 2. `0 <= nums[i] < 1000000.`
 3. `1 <= k <= len(nums) * (len(nums) - 1) / 2.`


#### 解题思路
题目要求求出第 k 个最小 pair 的距离。对于长度为n的数组，一共有 `n*(n-1)`个pair。如果我们求出所有 pair 的距离，然后排序找出第k个最小的pair的距离，时间复杂度会是 `O(n^2log(n))`，同时空间复杂度会是 `O(n^2)`， 这显然不是最优解。

可以对以上解法稍作优化，使用优先队列进行排序，这样时间复杂度会是`O(n^2log(k))`，空间复杂度会降低到 `O(k)`。

这题更好的一个解法是使用 [Binary Search](\tags\Binary-Search)。对数组先进行排序，我们可以得到 pair 的最大距离`end`。因为题目讨论的都是整数，所以答案一定是在`0`到`end`的范围内的整数。我们在这个范围内使用 `Binary Search`，对于每一个搜索的值 `mid`，我们用一个函数`count`判断比`mid`小的 pair 的距离的个数。如果小于k，则让 start == mid ；反之，则让 end == mid。

因为我们对数组事先进行了排序，所以每一次调用count函数，用`window sliding`的方法，只需要遍历一边数组就可以。

#### 示例代码 (python)
```python
class Solution:
    def smallestDistancePair(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        nums.sort()
        start, end = 0, nums[-1] - nums[0]
        while start + 1 < end:
            mid = int(start + (end - start)/2)
            if self.count(nums, mid) < k:
                start = mid
            else:
                end = mid
        return start if self.count(nums,start) >= k else end
    
    def count(self, nums, mid): #比mid小的pair数
        left, right, ans = 0, 0, 0
        while right != len(nums):
            while nums[right] - nums[left] > mid:
                left += 1
            ans += right - left
            right += 1
        return ans
```
#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int countPairs(vector<int>& nums, int mid) {
        int low = 0, high = 0, res = 0;
        while(high < nums.size()) {
            while(nums[high] - nums[low] > mid) {
                low++;
            }
            res += high - low;
            high++;
        }
        return res;
    }
    
    int smallestDistancePair(vector<int>& nums, int k) {
        sort(nums.begin(),nums.end());
        int low = nums[1] - nums[0], high = nums[nums.size()-1] - nums[0], mid;
        for(int i = 0; i < nums.size() - 1; i++) {
            if (nums[i + 1] - nums[i] < low) {
                low  = nums[i + 1] - nums[i];
            }
        }
        
        while(low < high) {
            mid = (low + high) / 2;
            if (countPairs(nums, mid) < k) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }
        return low;
    }
};
```

#### 复杂度分析
排序数组的时间复杂度为`O(n log(n))`， `Binary Search`的遍历次数为`O(log(n))`，每次遍历调用 count 函数，需要遍历一边数组，时间复杂度为`O(n)`， 所以总的时间复杂度是`O(n log(n))`。用 in-place 的方法排序，不需要额外的空间，总的空间复杂度为 `O(1)`

- 时间复杂度: `O(n log(n))` 
- 空间复杂度: `O(1)`

#### 归纳总结
在有有效精度或者整数等条件给出的前提下，用 [Binary Search](\tags\Binary-Search) 往往能有效的优化一些算法。之后我们会再多讨论这类题型。
