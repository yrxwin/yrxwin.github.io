---
title: '[Leetcode 1] Two Sum'
categories:
  - leetcode
author: '猩猩管理员'
date: 2018-06-15 17:16:54
tags: [Facebook, Microsoft, Amazon, Bloomberg, Uber, Linkedin, Apple,
Airbnb, Yelp, Yahoo, Adobe, Dropbox, Array, Hash Table]
keywords: [Two Sum, Array, Hash Table]
description:
---
#### 原题说明
Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the same element twice.

**Example**:
{% blockquote %}
Given `nums = [2, 7, 11, 15]`, `target = 9`,

Because `nums[0] + nums[1] = 2 + 7 = 9`,
return `[0, 1]`.
{% endblockquote %}

#### 解题思路
这是一道非常经典的面试题. 由于被面的太多, 现在一般会考察这道题的变种, 但是原题也还是经常出现在电话面试中, 或者被当做热身题.

这道题的`O(n)`解法是利用`hash table`来存储遍历过的元素, 对于当前的元素`nums[i]`, 我们只需要判断`target - nums[i]`是否在哈希表中即可.

这道题可能会有follow up问能否不用额外空间, 那么就需要牺牲时间复杂度: 可以先排序, 然后用双指针两头扫遍历一遍即可, 这个方法此处不做赘述, 在`Three Sum`中会详细介绍.

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> mapping;
        for (int i = 0; i < nums.size(); ++i) {
            if (mapping.count(target - nums[i])) {
                return {mapping[target - nums[i]], i};
            }
            mapping[nums[i]] = i;
        }
        return {-1, -1};
    }
};
```

#### 复杂度分析
时间复杂度: `O(n)` `n`为`nums`数组长度
空间复杂度: `O(n)`

#### 归纳总结
面试中如果遇到这道题, 也不要太高兴直接开始写答案, 还是要好好分析思路, 问清楚要求, 比如是不是一定有解, 可能有多少解, 能不能用额外空间等等.