---
title: '[Leetcode 777] Swap Adjacent in LR String'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-04-15 12:18:48
tags: [Brainteaser，Google]
keywords:
description:
---

#### 原题说明
In a string composed of `'L'`, `'R'`, and `'X'` characters, like "RXXLRXRXL", a move consists of either replacing one occurrence of `"XL"` with `"LX"`, or replacing one occurrence of `"RX"` with `"XR"`. Given the starting string start and the ending string end, return True if and only if there exists a sequence of moves to transform one string to the other.

	Example:
	Input: start = "RXXLRXRXL", end = "XRLXXRRLX"
	Output: True
	Explanation:
	We can transform start to end following these steps:
	RXXLRXRXL ->
	XRXLRXRXL ->
	XRLXRXRXL ->
	XRLXXRRXL ->
	XRLXXRRLX
**Note**:

1. 1 <= len(start) = len(end) <= 10000.
2. Both start and end will only consist of characters in `{'L', 'R', 'X'}`.

#### 解题思路
题目要求根据给定的规则，判断能否从 start string 变换到 end string 。

给出了两种变换的规则，从“XL”到“LX”和从“RX”到“XR”。所以我们可以给出两条规律：
  
 - 如果start能变换到end，那么除去两个字符串中的`"X"`，剩余的字符串一定相同。因为任意`"R"`和`"L"`的相对顺序都不会发生变化，我们定义出去`"X"`的字符串为有效字符串
 - 根据变换的规则，`"L"`不能向右移，`“R”`不能向左移，所以 start 中`“L”`对应的 index `"i"` 一定不小于 end 中 `“L”`对应的index `"j"`；start 中`“R”`对应的 index `"i"` 一定不大于 end 中 `“R”`对应的index `"j"`；
   1. i >= j, 如果 start[i]==end[j]=="L"
   2. i <= j, 如果 start[i]==end[j]=="R"

#### 示例代码 (python)
```python
class Solution:
    def canTransform(self, start, end):
        """
        :type start: str
        :type end: str
        :rtype: bool
        """
        # 第一条规律
        startRemove = "".join(start.split("X"))
        endRemove = "".join(end.split("X"))
        if startRemove != endRemove:
            return False
        # 第二条规律
        i, j, n = 0, 0, len(start)
        while(j < n and i < n):
            while(j < n and end[j] == 'X'):
                j += 1
            while(i < n and start[i] == 'X'):
                i += 1
            if(i == n and j == n): 
                break
            if(i == n or j == n or start[i] != end[j]):
                return False
            if(start[i] == 'R' and i > j) or (start[i] == 'L' and i < j):
                return False
            i += 1
            j += 1
        return True
```

#### 复杂度分析
每个字符串遍历一边，时间复杂度为`O(n)`。没有用额外空间，时间复杂度为`O(1)`
时间复杂度: `O(n)`
空间复杂度: `O(1)`

#### 归纳总结
本题需要对变换的规律做出总结，找出不变量，从而做出进一步判断。