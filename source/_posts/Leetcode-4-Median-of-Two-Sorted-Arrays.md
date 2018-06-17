---
title: '[Leetcode 4] Median of Two Sorted Arrays'
categories:
  - leetcode
author: '猩猩管理员'
date: 2018-06-17 17:19:04
tags: [Google, Microsoft, Apple, Zenefits, Yahoo, Adobe, Dropbox, Array, Binary Search, Divide and Conquer]
keywords: [Median of Two Sorted Arrays, Array, Binary Search, Divide and Conquer]
description:
---
#### 原题说明
There are two sorted arrays `nums1` and `nums2` of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be `O(log (m+n))`.

**Example 1**:
{% blockquote %}
`nums1 = [1, 3]`
`nums2 = [2]`
The median is `2.0`
{% endblockquote %}**Example 2**:

{% blockquote %}
`nums1 = [1, 2]`
`nums2 = [3, 4]`
The median is `(2 + 3)/2 = 2.5`
{% endblockquote %}
#### 解题思路
这道题的最优解比较难想到. 想到之后, 也要注意处理边界条件.

这里我们使用`Divide and Conquer`的方法: 首先抽象出一个函数, 用于寻找两个数组(由小到大)合并之后的第`k`个元素. 由于两个数组都是排好序的, 只需要比较他们的第`k / 2`个元素, 较小的那个元素至多排在合并后的第`k - 1`个位置, 因此该元素以及其左边的元素不可能为合并后的第`k`个元素, 均可以排除. 由此我们可以反复调用函数得到最终结果. 边界条件的处理请见代码.
 
这道题还可以使用二分搜索的办法, 但实际上掌握一种就足以应付面试了, 这里介绍的方法思路相对比较清晰. 读者如果对另一种方法感兴趣, 可以[参考这里](https://leetcode.com/problems/median-of-two-sorted-arrays/discuss/2471/very-concise-ologminmn-iterative-solution-with-detailed-explanation).

#### 示例代码 (cpp)
```cpp
class Solution {
    int findKth(vector<int> nums1, vector<int> nums2, int k) {
        int m = nums1.size(), n = nums2.size();
        if (m > n) {
            return findKth(nums2, nums1, k);
        }
        if (!m) {  // 较短的数组为空, 则直接返回另一个数组的第k个元素
            return nums2[k - 1];
        }
        if (k == 1) {
            return min(nums1[0], nums2[0]);
        }
        int i = min(m, k / 2), j = min(n, k / 2);
        if (nums1[i - 1] < nums2[i - 1]) {
            return findKth(vector<int>(nums1.begin() + i, nums1.end()), nums2, k - i);
        } else {
            return findKth(nums1, vector<int>(nums2.begin() + j, nums2.end()), k - j);
        }
        return -1;
    }
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int m = nums1.size(), n = nums2.size();
        return (findKth(nums1, nums2, (m + n + 1) / 2) + findKth(nums1, nums2, (m + n + 2) / 2)) / 2.0;
    }
};
```

#### 复杂度分析
时间复杂度: `O(log(m+n))`
空间复杂度: `O(1)`

#### 归纳总结
这道题没有见过的话不太容易一下子想到. 面试中遇到不要太高兴直接写答案, 要分析思路. 如果类似难度的题目没有遇到过也不要紧张, 面试官很可能会给出提示, 比如面试官如果提示目标复杂度是`log`量级的, 那么就应该想到可能是二分搜索或者`Divide and Conquer`的解法.  