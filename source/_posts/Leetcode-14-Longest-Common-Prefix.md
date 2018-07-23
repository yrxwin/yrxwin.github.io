---
title: '[Leetcode 14] Longest Common Prefix'
categories:
  - leetcode
author: '中猩猩'
date: 2018-07-23 16:24:22
tags: [String]
keywords: [String]
description:
---
#### 原题说明
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**
{% blockquote %}
**Input:** ["flower","flow","flight"]
**Output:** "fl"
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** ["dog","racecar","car"]
**Output:** ""
{% endblockquote %}

**Note:**

All given inputs are in lowercase letters `a-z`.

#### 解题思路
本题解法大致分为两步. 第一步获取输入中字符串的最小长度, 用来防止之后访问时的内存越界. 第二步, 依次判断字符串第i位的字符是否一样.
需要特别注意一些边界条件, 如输入空列表时直接返回空字符创.

#### 示例代码 (python)
```python
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        if len(strs) == 0:
            return ''
        ret = ''
        min_len = len(strs[0])
        for i in range(1, len(strs)):
            if len(strs[i]) < min_len:
                min_len = len(strs[i])
        
        for i in range(min_len):
            for j in range(1, len(strs)):
                if strs[j][i] != strs[0][i]:
                    return ret
            ret += strs[0][i]
        return ret
```

#### 复杂度分析
时间复杂度: `O(NK)`. N为列表长度, K为字符串长度
空间复杂度: `O(K)`. K为字符串长度

#### 归纳总结
本题比较简单, 但是仍需注意边界条件, 不要大意出错.
