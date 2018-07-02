---
title: '[Leetcode 10] Regular Expression Matching'
categories:
  - leetcode
date: 2018-06-25 17:44:41
tags: [Google, Facebook, Uber, Twitter, Airbnb, String, Dynamic Programming, Backtracking]
author: 中猩猩

---
#### 原题说明
Given an input string (`s`) and a pattern (`p`), implement regular expression matching with support for `'.'` and `'*'`.

{% blockquote %}
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
{% endblockquote %}

The matching should cover the **entire** input string (not partial).

**Note:**
- `s` could be empty and contains only lowercase letters `a-z`.
- `p` could be empty and contains only lowercase letters `a-z`, and characters like `.` or `*`.

**Example 1:**
{% blockquote %}
**Input:**
s = "aa"
p = "a"
**Output:** false
**Explanation:** "a" does not match the entire string "aa".
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:**
s = "aa"
p = "a\*"
**Output:** true
**Explanation:** '\*' means zero or more of the precedeng element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
{% endblockquote %}

**Example 3:**
{% blockquote %}
**Input:**
s = "ab"
p = ".\*"
**Output:** true
**Explanation:** ".\*" means "zero or more (\*) of any character (.)".
{% endblockquote %}

**Example 4:**
{% blockquote %}
**Input:**
s = "aab"
p = "c\*a\*b"
**Output:** true
**Explanation:** c can be repeated 0 times, a can be repeated 1 time. Therefore it matches "aab".
{% endblockquote %}

**Example 5:**
{% blockquote %}
**Input:**
s = "mississippi"
p = "mis\*is\*p\*."
**Output:** false
{% endblockquote %}

#### 解题思路 
*以下解题思路以python版本为准, cpp版本则是简化的(无递归)动态规划解答, 读者任选其一即可*

如果熟悉[Edit distance](https://en.wikipedia.org/wiki/Edit_distance)的话, 可以比较容易得想到用动态规划的办法求解.
类似[Edit distance](https://en.wikipedia.org/wiki/Edit_distance)的解法, 我们可以构建一个`SxP`的矩阵来记录状态. 
该矩阵中位于坐标`i, j`的值代表字符串`s[i:]`和Pattern`p[j:]`是否匹配(若为None, 则代表未知).
求解该矩阵的过程可以看作遵循一定走法的同时，试图寻找一条从`(0, 0)`走到`(S + 1, P + 1)`的路径. (`S + 1`和`P + 1`可以看作是s和p的终结状态)

如果`s[i]`和`p[j]`是匹配的(`s[i] == p[j]` 或者 `p[j] == '.'`):
- 如果`j + 1`是`*`的话，我们可以从`(i, j)`走到`(i, j + 2)`代表我们跳过这个pattern, 或者从`(i, j)`走到`(i + 1, j)`代表我们选择匹配这个字符
- 如果不是`*`的话，那么我们直接从`(i, j)`走到`(i + 1, j + 1)`. 这意味着我们匹配了`(i, j)`

如果不匹配:
- 如果`j + 1`是`*`的话, 我们可以从`(i, j)`走到`(i, j + 2)`代表我们跳过这个pattern
- 如果不是, 那么说明必然不匹配, `(i, j)`的状态是`False`
终结状态就是`s`和`p`都用完, 也就是走到`(S + 1, P + 1)`的时候.
如果`p`用完了, 但是`s`还有剩余, 那么显然不匹配.
如果`s`用完了, `p`还有剩余, 那么只有当接下来都是有`*`的pattern的时候才匹配.

#### 示例代码 (python)
```python
class Solution(object):
    def dfs(self, i, j, s, p, dp):
        if j == len(p):
            return i == len(s)
        
        if i == len(s):
            if j < len(p) - 1 and p[j + 1] == '*':
                return self.dfs(i, j + 2, s, p, dp)
            else:
                return False
            
        if dp[i][j] is not None:
            return dp[i][j]
        
        curr_match = p[j] == '.' or s[i] == p[j]
        if j + 1 < len(p) and p[j + 1] == '*':
            dp[i][j] = self.dfs(i, j + 2, s, p, dp) \
                        or curr_match and self.dfs(i + 1, j, s, p, dp)
        else:
            dp[i][j] = curr_match and self.dfs(i + 1, j + 1, s, p, dp)
        return dp[i][j]
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        dp = [[None for i in range(len(p))] for j in range(len(s))]
        return self.dfs(0, 0, s, p, dp)
```

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.size(), n = p.size();
        vector<vector<bool>> dp(m + 1, vector<bool>(n + 1, false));
        dp[0][0] = true;
        for (int i = 0; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                if (p[j - 1] != '*' && p[j - 1] != '.') {
                    if (i > 0 && s[i - 1] == p[j - 1]) {
                        dp[i][j] = dp[i - 1][j - 1];
                    }
                } else if (p[j - 1] == '.') {
                    if (i > 0) {
                        dp[i][j] = dp[i - 1][j - 1];
                    }
                } else {
                    if (j == 1) {
                        continue;
                    }
                    dp[i][j] = dp[i][j - 2];
                    if (i > 0 && (p[j - 2] == '.' || p[j - 2] == s[i - 1])) {
                        dp[i][j] = dp[i][j] || dp[i - 1][j];
                    }
                }
            }
        }
        return dp[m][n];
    }
};
```

#### 复杂度分析
时间复杂度: `O(SP)`, 其中`S`为`s`的长度, `P`为`p`的长度. 
空间复杂度: `O(SP)`, 其中`S`为`s`的长度, `P`为`p`的长度

#### 归纳总结
这道题的思路还是比较容易想到用动态规划/递归来做的. 虽然这里python版本使用了DFS，但是因为记录了中间状态，本质上就是动态规划(如果读者细心比较，会发现时间空间复杂度也是一样的). 面试时, 还需要额外注意终结状态的判断和边界条件, 避免出现edge case或者访问了超出边界的矩阵坐标.
