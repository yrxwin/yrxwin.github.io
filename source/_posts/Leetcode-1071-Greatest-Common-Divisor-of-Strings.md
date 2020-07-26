---
title: '[Leetcode 1071] Greatest Common Divisor of Strings'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-07-26 19:18:50
tags: ['Atlassian', 'Capital One', 'String']
keywords: ['Atlassian', 'Capital One', 'String']
description:
---
#### 原题说明
<div class="sql-schema-wrapper__3VBi" style="margin-bottom: 15px; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><div class="content__u3I1 question-content__JfgR" style="margin: 1em 0px;"><div class="sql-schema-wrapper__3VBi" style="margin-bottom: 15px;"><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56);">For strings&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">T</code>, we say "<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">T</code>&nbsp;divides&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S</code>" if and only if&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S = T + ... + T</code>&nbsp; (<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">T</code>&nbsp;concatenated with itself 1 or more times)</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56);">Return the largest string&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">X</code>&nbsp;such that&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">X</code>&nbsp;divides&nbsp;<font face="monospace">str1</font>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">X</code>&nbsp;divides&nbsp;<font face="monospace">str2</font>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56);"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>str1 = <span id="example-input-1-1">"ABCABC"</span>, str2 = <span id="example-input-1-2">"ABC"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">"ABC"</span>
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56);"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>str1 = <span id="example-input-2-1">"ABABAB"</span>, str2 = <span id="example-input-2-2">"ABAB"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">"AB"</span>
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56);"><span style="font-weight: bolder;">Example 3:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>str1 = <span id="example-input-3-1">"LEET"</span>, str2 = <span id="example-input-3-2">"CODE"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-3">""</span></pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56);"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= str1.length &lt;= 1000</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= str2.length &lt;= 1000</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">str1[i]</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">str2[i]</code>&nbsp;are English uppercase letters.</li></ol></div></div></div>
<!--more-->

#### 解题思路
这道题可以用递归来求解，和求两个数的最大公约数类似。
首先，`str1`和`str2`(假设`str1.size() >= str2.size()`)有最大公约数的必要条件是`str1`的前缀等于`str2`。
原因如下，假设最大公约字符串为`divisor_str`，那么`str1 = x * divisor_str`，`str2 = y * divisor_str` (`x`, `y`为正整数，且`x >= y`)，
所以`str1`的前`y`个`divisor_str`就等于`str2`。
其次，我们希望求两个字符串的最大公约字符串，就等于求两个字符串之差和其中一个字符串的最大公约字符串。还是用上述例子：
`str1`与`str2`的最大公约数，也是`str1 - str2 = (y - x) * divisor_str` 与 `str2 = y * divisor_str`的最大公约数。
当`y = x`时，`str2`本身即为`str1`和`str2`的最大公约数。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    string gcdOfStrings(string str1, string str2) {
        // Puts longer string first
        if (str1.size() < str2.size()) {
            return gcdOfStrings(str2, str1);
        }
        if (str2.empty()) {
            return str1;
        }
        // If str1 is not starts with str2, they don't have common divisor.
        if (str1.substr(0, str2.size()) != str2) {
            return "";
        }
        return gcdOfStrings(str1.substr(str2.size()), str2);
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public String gcdOfStrings(String str1, String str2) {
        if (str1.length() < str2.length()) { // make sure str1 is not shorter than str2.
            return gcdOfStrings(str2, str1); 
        }else if (!str1.startsWith(str2)) { // shorter string is not common prefix.
            return ""; 
        }else if (str2.isEmpty()) { // gcd string found.
            return str1;
        }else { // cut off the common prefix part of str1.
            return gcdOfStrings(str1.substring(str2.length()), str2); 
        }
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def gcdOfStrings(self, str1: str, str2: str) -> str:
        if not str1 or not str2:
            return str1 if str1 else str2
        elif len(str1) < len(str2):
            return self.gcdOfStrings(str2, str1)
        elif str1[: len(str2)] == str2:
            return self.gcdOfStrings(str1[len(str2) :], str2)
        else:
            return ''
```

#### 复杂度分析
时间复杂度: `O(M + N)`, `M`和`N`为`str1`和`str2`的长度, 主要是`str1.substr(0, str2.size()) != str2`这一判断会遍历一遍每一个字符
空间复杂度: `O(1)`, 栈的最大深度为`O(max(M, N))`, 因为最坏的情况`len(str2) = 1`，那么递归深度就是`len(str1)`, 即`O(M)`.

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/pUfd6fT2kxk)，欢迎关注！