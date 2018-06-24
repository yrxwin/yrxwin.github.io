---
title: '[Leetcode 5] Longest Palindromic Substring'
categories:
  - leetcode
author: '猩猩管理员'
date: 2018-06-19 16:41:57
tags: [Microsoft, Amazon, Bloomberg, String, Dynamic Programming]
keywords: [Longest Palindromic Substring, Dynamic Programming]
description:
---
#### 原题说明
Given a string `s`, find the longest palindromic substring in `s`. You may assume that the maximum length of `s` is 1000.

**Example 1**:
{% blockquote %}
Input: `"babad"`
Output: `"bab"`
Note: `"aba"` is also a valid answer.
{% endblockquote %}**Example 2**:

{% blockquote %}
Input: `"cbbd"`
Output: `"bb"`
{% endblockquote %}


#### 解题思路
很多`palindrome`相关的问题都可以用动态规划去解决. 做动态规划的问题, 要想清楚以下几件事情:
- 动归数组代表了什么
- 递推公式是什么, 从而可以决定从什么方向开始递推. 例如`dp[i] = func(dp[i-1])`那就从左向右递推, 反之如果`dp[i] = func(dp[i+1])`那么就要从右向左递推
- 处理边界条件

回到这道题, 我们用一个二维布尔数组`dp[j][i]`代表从`j`开始到`i`结束的子字符串是否为回文字符串. 初始条件为对于任意下标`i`, `dp[i][i]`为`true`, 这一初始条件可以在递推过程中更新. 递推公式和递推方向请见具体代码.

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        if (!s.size()) {
            return "";
        }
        string ret;
        int left = 0, maxLen = 1;
        int n = s.size();
        vector<vector<bool>> dp(n, vector<bool>(n, false));
        for (int i = 0; i < n; ++i) { // i自左向右更新
            dp[i][i] = true;
            for (int j = i - 1; j >= 0; --j) { // j自右向左更新
                dp[j][i] = (s[i] == s[j] && (i - j < 2 || dp[j + 1][i - 1]));
                // 上面这行就是递推公式
                if (dp[j][i]) {
                    if (maxLen < i - j + 1) {
                        maxLen = i - j + 1;
                        left = j;
                    }
                }
            }
        }
        return s.substr(left, maxLen);
    }
};
```

#### 示例代码 (python)
```python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        maxlen = 0
        ret = None
        dp = [[None for i in range(len(s))] for j in range(len(s))]
        for right in range(len(s)):
            for left in range(right, -1, -1):
                dp[left][right] = s[left] == s[right] and (right - left < 3 or dp[left + 1][right - 1])
                if dp[left][right] and (right - left + 1 > maxlen):
                    maxlen = right - left + 1
                    ret = s[left:right + 1]
        return ret
```

#### 复杂度分析
时间复杂度: `O(n^2)`, 其中`n`为`s`的长度
空间复杂度: `O(n^2)`

#### 归纳总结
动态规划的题一般思路比较难想清楚, 但是有了思路之后代码实现比较容易. 因此面试中不要慌张, 记住本文归纳的三个要点, 先讨论清楚了再开始写代码.
