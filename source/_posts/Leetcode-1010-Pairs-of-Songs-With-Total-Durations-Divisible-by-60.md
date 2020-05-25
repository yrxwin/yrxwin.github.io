---
title: '[Leetcode 1010] Pairs of Songs With Total Durations Divisible by 60'
categories:
  - leetcode
author: '大猩猩'
date: 2019-04-07 16:03:16
tags: ['Array','Goldman Sachs','Amazon']
keywords:
description:
---

#### 原题说明
In a list of songs, the `i`-th song has a duration of `time[i]` seconds. 

Return the number of pairs of songs for which their total duration in seconds is divisible by 60.  Formally, we want the number of indices `i < j` with `(time[i] + time[j]) % 60 == 0`.

**Example 1:**
{% blockquote %}
**Input:** `[30,20,150,100,40]`
**Output:** `3`
**Explanation:** Three pairs have a total duration divisible by 60:
(time[0] = 30, time[2] = 150): total duration 180
(time[1] = 20, time[3] = 100): total duration 120
(time[1] = 20, time[4] = 40): total duration 60
{% endblockquote %}
**Example 2:**
{% blockquote %}
**Input:** `[60,60,60]`
**Output:** 3
**Explanation:** All three pairs have a total duration of 120, which is divisible by 60.
{% endblockquote %}

**Note:**
1. `1 <= time.length <= 60000`
2. `1 <= time[i] <= 500`


#### 解题思路
一个pair能被60整除，意味着两个数的余数的和也能被`60`整除。因此，一个数可以按照对`60`的余数进行分类。这样，按题目给出的要求，一共有`0，1，2，...，59`一共`60`个分类。当两个分类的和被`60`整除时，从每个分类中任意选取1个数，都能组成满足题目要求的一个pair。


因此，我们可以用一个哈希表`mapping`记录上述的分类，哈希表的`key`是余数，`value`是有着对应余数的数的个数。

这里，最简单的做法是先遍历一边`time`，将`mapping`更新好。然后再遍历一边`mapping`,按照余数计算pair的数量。但是这个方法的缺点在于：
1. 需要遍历一遍`time`，再遍历一遍`mapping`
2. 需要对`0`和`30`两类余数的情况做特殊处理。因为他们对应的满足题目条件的余数就是他们自身。

所以我们提供一种只遍历一遍`time`的方法，并且不需要特别处理余数是`0`和`30`的情况

算法：遍历`time`，在每个 iteration 中，当前元素对`60`的余数是`remainder`，在pair中对应的余数是`c_remainder`。这样，pair增加的数量就是`mapping`中`c_remainder`的`value`。同时，需要再更新`mapping`，使得`mapping[remainder]++`。


#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int numPairsDivisibleBy60(vector<int>& time) {        
        unordered_map<int,int> mapping;
        int res = 0;
        for (auto ele : time) {
            int remainder = ele % 60;
            int c_remainder = (60 - remainder) % 60;
            if (mapping.count(c_remainder)) {
                res += mapping[c_remainder];
            }
            mapping[remainder]++;
        }
        
        return res;
    }
};
```

#### 复杂度分析
时间复杂度: `O(n)`
空间复杂度: `O(1)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/i9VSosl-2Js)，欢迎关注！