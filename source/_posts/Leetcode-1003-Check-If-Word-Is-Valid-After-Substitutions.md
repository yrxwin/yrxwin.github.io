---
title: '[Leetcode 1003] Check If Word Is Valid After Substitutions'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-03-11 23:33:37
tags: ['Nutanix', 'String', 'Stack', 'Medium']
keywords: ['Nutanix', 'String', 'Stack', 'Medium']
description:
---
#### 原题说明
We are given that the string `"abc"` is valid.

From any valid string `V`, we may split `V` into two pieces `X` and `Y` such that `X + Y` (`X` concatenated with `Y`) is equal to `V`.  (`X` or `Y` may be empty.)  Then, `X + "abc" + Y` is also valid.

If for example `S = "abc"`, then examples of valid strings are: `"abc"`, `"aabcbc"`, `"abcabc"`, `"abcabcababcc"`.  Examples of invalid strings are: `"abccba"`, `"ab"`, `"cababc"`, `"bac"`.

Return true if and only if the given string `S` is valid.

**Example 1:**
{% blockquote %}
**Input:** `"aabcbc"`
**Output:** `true`
**Explanation:** 
We start with the valid string `"abc"`.
Then we can insert another `"abc"` between `"a"` and `"bc"`, resulting in `"a" + "abc" + "bc"` which is `"aabcbc"`.
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** `"abcabcababcc"`
**Output:** `true`
**Explanation:**
`"abcabcabc"` is valid after consecutive insertings of `"abc"`.
Then we can insert `"abc"` before the last letter, resulting in `"abcabcab" + "abc" + "c"` which is `"abcabcababcc"`.
{% endblockquote %}

**Example 3:**
{% blockquote %}
**Input:** `"abccba"`
**Output:** `false`
{% endblockquote %}

**Example 4:**
{% blockquote %}
**Input:** `"cababc"`
**Output:** `false`
{% endblockquote %}

**Note:**
1. `1 <= S.length <= 20000`
2. `S[i]` is `'a'`, `'b'`, or `'c'`


#### 解题思路
这道题和括号相关的题很像
遍历`S`:
1) 当遇到`'a'`或`'b'`时，用一个栈`stk`来存储
2) 当遇到`'c'`时，pop栈中的元素，看能否依次pop出`'b'`和`'c'`，如果不能则返回`false`
遍历结束后，如果`stk`为空，则返回`true`，不然为`false`

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    bool isValid(string S) {
        stack<char> stk;
        for (auto ch : S) {
            if (ch != 'c') {
                stk.push(ch);
            } else {
                if (stk.size() < 2) {
                    return false;
                }
                if (stk.top() != 'b') {
                    return false;
                }
                stk.pop();
                if (stk.top() != 'a') {
                    return false;
                }
                stk.pop();
            }
        }
        return stk.empty();
    }
};
```

#### 复杂度分析
时间复杂度: `O(n)` `n`为`S`的长度
空间复杂度: `O(n)` 

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/1fYgCFsQCxk)，欢迎关注！