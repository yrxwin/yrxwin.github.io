---
title: '[Leetcode 6] ZigZag Conversion'
categories:
  - leetcode
author: '中猩猩'
date: 2018-07-01 16:23:17
tags: [String]
keywords: [String]
description:
---
#### 原题说明
The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
{% blockquote %}  
P&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;H&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;N  
A&nbsp;&nbsp;P&nbsp;&nbsp;L&nbsp;&nbsp;S&nbsp;&nbsp;&nbsp;I&nbsp;&nbsp;&nbsp;I&nbsp;&nbsp;&nbsp;G  
Y&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;R
{% endblockquote %}
And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:
{% blockquote %}
string convert(string s, int numRows);
{% endblockquote %}

**Example 1:**
{% blockquote %}
**Input:** s = "PAYPALISHIRING", numRows = 3
**Output:** "PAHNAPLSIIGYIR"
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** s = "PAYPALISHIRING", numRows = 4
**Output:** "PINALSIGYAHRPI"
**Explanation:**

P     I    N
A   L S  I G
Y A   H R
P     I
{% endblockquote %}

#### 解题思路
这道题需要把一个字符串变成ZigZag的排列后按行输出。所以我们只需要依次判断每个字符应该出现在ZigZag排列中的哪一行就可以了。
对于一个`N`行的ZigZag排列，我们可以把它看作一个周期为`2N - 2`的循环。在这个周期内，如果一个字符位于周期的前`N`位，
那么它的位数就是行号。如果在`N`位置后，那么它的行号就是超出部分的倒序，如`N + 1`那么，行号就是`N - 1`. (以上行号，从1开始计)

#### 示例代码 (python)
```python
class Solution(object):
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        if numRows == 1:
            return s
        rows = ['' for i in range(numRows)]
        for i in range(len(s)):
            r = i % (2 * numRows - 2)
            if r >= numRows:
                r = 2 * numRows - r - 2
            rows[r] += s[i]
        return ''.join(rows)
```

#### 复杂度分析
时间复杂度: `O(n)` 其中`n`为`s`的长度
空间复杂度: `O(n)`

#### 归纳总结
这道题难度不高, 只需要考虑清楚字符串转换前后的对应关系即可。
