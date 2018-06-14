---
title: '[Leetcode 239] Sliding Window Maximum'
categories:
  - leetcode
author: '猩猩管理员'
date: 2018-06-14 15:37:45
tags: [Google, Amazon, Zenefits, Heap]
keywords: [Sliding Window Maximum, Google, Amazon, Zenefits, Heap, Stack]
description:
---
#### 原题说明
Given an array `nums`, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

**Example**:
**Input**: `nums = [1,3,-1,-3,5,3,6,7]`, and `k = 3`
**Output**: `[3,3,5,5,6,7]`
**Explanation**: 
```
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```
**Note**: 
You may assume k is always valid, 1 ≤ k ≤ input array's size for non-empty array.

**Follow up**:
Could you solve it in linear time?

#### 解题思路
这是一道比较好的面试题, 因为用priority queue的方法是容易想到的, 但是在实现的过程中也需要考虑一些边界条件, 比如刚开始扫的时候队列中少于`k`个数怎么处理, 什么时候结束等等. 这样方便面试官考察基本的coding能力.

对于followup, 相对来说要难一些, 用了类似`stack`的结构来存储当前sliding window, 类似的问题有[[LeetCode 316] Remove Duplicate Letters 移除重复字母](/Leetcode-316-Remove-Duplicate-Letters)
, [[Leetcode 739] Daily Temperatures](/Leetcode-739-Daily-Temperatures). 如果面试中能够想到的话, 就很接近Strong Hire了.

为了方便更新sliding window以及取出当前最大元素, 我们用的数据结构是`deque`, 不过其功能更像是一个`stack`. `deque`存储的是`nums`中对应元素的`index`. 主要思路是使得`deque`中的元素由老到新, 由大到小排列. 具体的方法是: 每次新扫到的元素与栈顶元素(即`deque`的尾元素)比较, 如果新的元素大, 则`pop`当前栈顶元素, 不然则直接插入新元素. 这样每走一步, 当前的`deque`头元素(栈底元素)即为窗口中的最大值.

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> dq;
        vector<int> rets;
        for (int i = 0; i < nums.size(); ++i) {
            if (i >= k) {
                if (dq.front() == i - k) {
                    dq.pop_front();
                }
            }
            while (!dq.empty() && nums[i] > nums[dq.back()]) {
                dq.pop_back();
            }
            dq.push_back(i);
            if (i >= k - 1) {
                rets.push_back(nums[dq.front()]);
            }
        }
        return rets;
    }
};
```

#### 复杂度分析
时间复杂度: `O(n)` 其中`n`为`nums`长度
空间复杂度: `O(k)`

#### 归纳总结
同学们可以将解题思路中总结的类似题目一起做一遍, 这样对于处理这类问题会有更好的理解.