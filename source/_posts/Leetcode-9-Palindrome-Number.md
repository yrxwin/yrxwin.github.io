---
title: '[Leetcode 9] Palindrome Number'
categories:
  - leetcode
author: '中猩猩'
date: 2018-07-14 14:42:24
tags: [Math]
keywords: [Math]
description:
---
#### 原题说明
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

**Example 1:**
{% blockquote %}
**Input:** 121
**Output:** true

{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** -121
**Output:** false
**Explanation:** From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
{% endblockquote %}

**Example 3:**
{% blockquote %}
**Input:** 10
**Output:** false
**Explanation:** Reads 01 from right to left. Therefore it is not a palindrome.
{% endblockquote %}

#### 解题思路
最简单的思路是先转换成字符串, 然后用两个指针来判断. 但是这样需要`O(n)`的空间复杂度. 为了用`O(1)`的空间复杂度, 我们可以直接把输入转换成反转后的数字. 如果一个数字反转后, 大小不变, 则是回文数. 解法也比较直观, 按位取余后逐渐生成反转后的数字. 要注意判断是否溢出. 

#### 示例代码 (python)
```python
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x < 0:
            return False
        rev = 0
        x_ = x
        while x_ > 0:
            tmp = rev * 10 + x_ % 10
            if (tmp - x_ % 10 ) / 10 != rev:
                return False
            rev = tmp
            x_ /= 10
        return x == rev
```

#### 复杂度分析
时间复杂度: `O(n)`
空间复杂度: `O(1)`

#### 归纳总结
在解题时需要判断是否会溢出.
