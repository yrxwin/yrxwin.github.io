---
title: '[Leetcode 31] Next Permutation'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-07-03 23:08:40
tags: [Array, Google]
keywords: [Array]
description:
---

#### 原题说明
Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.


{% blockquote %}
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
{% endblockquote %}

#### 解题思路
不熟悉排列数的，可以看一下[permutation](https://en.wikipedia.org/wiki/Permutation)的基本定义。同时，我们要清楚字典顺序的定义[Lexicographical order](https://en.wikipedia.org/wiki/Lexicographical_order)。

最直接的想法是把所有的全排列找出，但是这显然不是最优解，并且不符合题目要求的`constant extra memory`。

我们这里用一个例子来说明如何找出下一个字典顺序的排列数。
假定我们有下面这组排列是

{% blockquote %}
6 5 4 8 7 5 1
{% endblockquote %}

 - 我们从后往前看，找到第一个非递减的数，这里是 4 .
 - 我们可以发现，以 `6 5 4`开头的排列数，`8 7 5 1` 已经是最后一个排列数，因此需要把 4 做替换
 - 在 `8 7 5 1` 中，比 4 大的最小的数是 5，因此把 5 和 4 做交换，我们得到 `6 5 5 8 7 4 1`
 - 显然 `6 5 5 8 7 4 1` 并不是我们要求的，但只要把最后 4 位 `8 7 4 1` 做从小到大的排序，变成 `1 4 7 8`, 我们就得到了想要的字典顺序的排列数 `6 5 5 1 4 7 8`。

按照这个思路，我们给出相对应的代码。

#### 示例代码 (cpp)

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size(), left = -1;
        for (int i = n-1; i > 0; i--) {
            if (nums[i-1] < nums[i]) {
                left = i-1;
                break;
            }
        }
        if (left != -1) {
            for (int i = n-1; i > left; i--) {
                if (nums[left] < nums[i]) {
                    swap(nums[left], nums[i]);
                    break;
                }
            }
        }
        reverse(nums.begin() + left + 1, nums.end());
    }
};
```

#### 复杂度分析
搜索第一个非递减的数，复杂度为 `O(n)`，reverse数组，复杂度为 `O(n)`, 所以总的时间复杂度是 `O(n)` 。
没用额外空间，复杂度是 `O(1)`。

- 时间复杂度: `O(n)` 
- 空间复杂度: `O(1)`

#### 归纳总结
这题主要需要先明白 `permutation` 和 `lexicographical order`, 然后才能找出 `next permutation`的规律。借助一些具体的例子，能帮助提供一些思路。比单纯抽象的思考可能更好。
