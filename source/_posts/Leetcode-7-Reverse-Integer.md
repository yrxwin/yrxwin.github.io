---
title: '[Leetcode 7] Reverse Integer'
categories:
  - leetcode
author: '中猩猩'
date: 2018-07-06 15:09:14
tags: [Math]
keywords: [Math]
description:
---
#### 原题说明
Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**
{% blockquote %}
**Input:** 123
**Output:** 321
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** -123
**Output:** -321
{% endblockquote %}

**Example 3:**
{% blockquote %}
**Input:** 120
**Output:** 21
{% endblockquote %}

**Note:**

Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1].
For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

#### 解题思路
解法比较简单, 按位取余即可. 难点在于如何处理溢出的问题. 在python中, 会自动处理溢出问题, 只需要直接判断是否在`INT_32`的范围内即可. 
但是python的取余在负数上的行为与预期不同, 因此需要记下符号, 并转换成非负数. 其他语言中, 需要在结果乘`10`之前与`INT_MAX`作比较，观察是否会溢出.

#### 示例代码 (python)
```python
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        sign = 1 if x > 0 else -1
        x = x if x > 0 else -x
        ret = 0
        while x != 0:
            ret *= 10
            ret += x % 10
            x /= 10
        ret *= sign
        if (ret < -2**31) or (ret > 2**31 - 1):
            return 0
        return ret
```

#### 复杂度分析
时间复杂度: `O(log n)`
空间复杂度: `O(1)`

#### 归纳总结
在解题时需要考虑清楚何时会溢出, 或者转换成长整型后再作判断.
