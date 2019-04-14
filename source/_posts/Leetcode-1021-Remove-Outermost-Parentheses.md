---
title: '[Leetcode 1021] Remove Outermost Parentheses'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-04-14 01:58:04
tags: ['Google', 'Stack']
keywords: ['Google', 'Stack']
description:
---
#### 原题说明
A valid parentheses string is either empty `("")`, `"(" + A + ")"`, or `A + B`, where `A` and `B` are valid parentheses strings, and + represents string concatenation.  For example, `""`, `"()"`, `"(())()"`, and `"(()(()))"` are all valid parentheses strings.

A valid parentheses string `S` is primitive if it is nonempty, and there does not exist a way to split it into `S = A+B`, with A and B nonempty valid parentheses strings.

Given a valid parentheses string `S`, consider its primitive decomposition: `S = P_1 + P_2 + ... + P_k`, where `P_i` are primitive valid parentheses strings.

Return `S` after removing the outermost parentheses of every primitive string in the primitive decomposition of `S`.


**Example 1:**
{% blockquote %}
**Input:** `"(()())(())"`
**Output:** `"()()()"`
**Explanation:** 
The input string is `"(()())(())"`, with primitive decomposition `"(()())" + "(())"`.
After removing outer parentheses of each part, this is `"()()" + "()" = "()()()"`.
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** `"(()())(())(()(()))"`
**Output:** `"()()()()(())"`
**Explanation:** 
The input string is `"(()())(())(()(()))"`, with primitive decomposition `"(()())" + "(())" + "(()(()))"`.
After removing outer parentheses of each part, this is `"()()" + "()" + "()(())" = "()()()()(())"`.
{% endblockquote %}

**Example 3:**
{% blockquote %}
**Input:** `"()()"`
**Output:** `""`
**Explanation:** 
The input string is `"()()"`, with primitive decomposition `"()" + "()"`.
After removing outer parentheses of each part, this is `"" + "" = ""`.
{% endblockquote %}

**Note:**
1. `S.length <= 10000`
2. `S[i]` is `"("` or `")"`
3. `S` is a valid parentheses string
<!--more-->

#### 解题思路
用一个整型变量`opened`来记录左括号比右括号多出的数量
遍历S，遇到左括号`++opened`，遇到右括号`--opened`
除非遇到第一个左括号（`opened = 1`）或者最后一个右括号（`opened = 0`）
不然其余字符均加入最终结果`res`

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    string removeOuterParentheses(string S) {
        int opened = 0;
        string res;
        for (auto ch : S) {
            if (ch == '(') {
                ++opened;
                if (opened != 1) {
                    res += ch;
                }
            } else {
                --opened;
                if (opened != 0) {
                    res += ch;
                }
            }
        }
        return res;
    }
};
```

#### 示例代码（java）
```java
class Solution {  
    public String removeOuterParentheses(String S) {
        StringBuilder s = new StringBuilder();
        int opened = 0;
        for (char c : S.toCharArray()) {
            if (c == '(' && opened++ > 0) s.append(c);
            if (c == ')' && opened-- > 1) s.append(c);
        }
        return s.toString();
    }
}
```

#### 示例代码（python）
```python
class Solution(object):
    def removeOuterParentheses(self, S):
        """
        :type S: str
        :rtype: str
        """
        res, opened = [], 0
        for c in S:
            if c == '(' and opened > 0: res.append(c)
            if c == ')' and opened > 1: res.append(c)
            opened += 1 if c == '(' else -1
        return "".join(res)
```

#### 复杂度分析
时间复杂度: `O(N)`
空间复杂度: `O(N)` 如果包含返回的`string`，不然为`O(1)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/e1yJ40MdF50)，欢迎关注！