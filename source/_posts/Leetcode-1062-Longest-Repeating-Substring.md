---
title: '[Leetcode 1062] Longest Repeating Substring'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-06-28 12:14:22
tags: ['String','Google','Facebook']
keywords:
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given a string&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S</code>, find out the length of the longest repeating substring(s). Return&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0</code>&nbsp;if no repeating substring exists.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-1-1">"abcd"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">0</span>
<span style="font-weight: bolder;">Explanation: </span>There is no repeating substring.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-2-1">"abbaba"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">2</span>
<span style="font-weight: bolder;">Explanation: </span>The longest repeating substrings are "ab" and "ba", each of which occurs twice.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 3:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-3-1">"aabcaabdaab"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-3">3</span>
<span style="font-weight: bolder;">Explanation: </span>The longest repeating substring is "aab", which occurs <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">3</code> times.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 4:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-4-1">"aaaaa"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-4">4</span>
<span style="font-weight: bolder;">Explanation: </span>The longest repeating substring is "aaaa", which occurs twice.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Constraints:</span></p><ul style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li>The string&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S</code>&nbsp;consists of only lowercase English letters from&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">'a'</code>&nbsp;-&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">'z'</code>.</li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= S.length &lt;= 1500</code></li></ul>
<!--more-->

#### 解题思路
这题我们采用动态规划的方法。
我们先定义`dp[i][j]`为分别以第`i`个字符和第`j`个字符结尾的`substring`有相同共同后缀的最大长度。因此，我们也要求`i>j`。
我们注意到，当`S[i] != S[j]`, 那么`dp[i][j] = 0`， 否则`dp[i][j] = dp[i-1][j-1] + 1`。这就是我们的状态转移方程。

`dp[i][j] = dp[i-1][j-1] + 1 -----------  S[i] == S[j]`
`dp[i][j] = 0                -----------  S[i] != S[j]` 

我们更新`dp[i][j]`的最大值，就可以得到最后的答案。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int longestRepeatingSubstring(string S) {
        int ans = INT_MIN;
        vector<vector<int>> dp(S.size() + 1, vector<int>(S.size() + 1, 0));
        for (auto i = 1; i <= S.size(); i++) {
            for (auto j = 1; j < i; j++) {
                if (S[i-1] == S[j-1]) {
                    dp[i][j] = dp[i-1][j-1] + 1;
                }
                ans = max(ans, dp[i][j]);
            }
        }
        return ans;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int longestRepeatingSubstring(String S) {
        int res = 0;
        int n = S.length();
        int[] dp = new int[n + 1];
        
        for (int i = 1; i <= n; i++) {
		   // Need start from i - 1 to use values from last iteration
            for (int j = i - 1; j >= 1; j--) {
                if (S.charAt(i - 1) == S.charAt(j - 1)) {
                    dp[j] = dp[j - 1] + 1;
                } else {
                    dp[j] = 0;
                }
                
                res = Math.max(res, dp[j]);
            }
        }
        
        return res;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def longestRepeatingSubstring(self, S: str) -> int:
        ans = 0
        for i in range(1, len(S)):
            if ans >= len(S)-i: 
                break 
                
            tmp = 0
            for x, y in zip(S[i:],S[:-i]):
                if x == y:
                    tmp += 1 
                    ans = max(ans, tmp)
                else:
                    tmp = 0 
            
        return ans
```

#### 复杂度分析
`N`是字符串的长度。
时间复杂度: O(N^2)
空间复杂度: O(N^2)

#### 视频讲解
我们在**Youtube**上更新了[视频讲解](https://youtu.be/iA6TDMV5g2M)，欢迎关注！