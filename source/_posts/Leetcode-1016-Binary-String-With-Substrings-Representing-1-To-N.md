---
title: '[Leetcode 1016] Binary String With Substrings Representing 1 To N'
categories:
  - leetcode
author: '大猩猩'
date: 2019-04-10 23:10:52
tags: [String,Google]
keywords:
description:
---

#### 原题说明
Given a binary string `S` (a string consisting only of `'0'` and `'1'`s) and a positive integer `N`, return true if and only if for every integer `X` from `1` to `N`, the binary representation of `X` is a substring of `S`.


**Example 1:**
{% blockquote %}
**Input:** `S = "0110", N = 3`
**Output:** `true`
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** `S = "0110", N = 4`
**Output:** `false`
{% endblockquote %}

 
**Note:**
1. `1 <= S.length <= 1000`
2. `1 <= N <= 10^9`

#### 解题思路
最简答的想法是判断1到N的二进制表达是否存在于S的子字符串中。但是`N`最大有`10^9`，每次检查子字符串时间复杂度是O(1)，但是由于`N`可能很大，效率会低。

转换一下思路，反过来判断`S`中能否组成从`1`到`N`中所有的数。

我们将`S`中的所有子字符串遍历一遍，若是在`1`到`N`之间，我们将其记录在一个`set`中。最后检查`set`的大小是否等于`N`即可。

这个算法理论上的时间复杂度会是 `O(n^2)`， 这里`n`是`S`的长度。但实际中，当子字符串代表的数大于`N`时，我们就停止检查了，意味着我们并不需要检查所有的子字符串。

###### 补充:
其实我们发现最简单的想法也是可以AC。这样的原因可能是只要检查出一个`1`到`N`中找不到的数，就可以及时跳出循环，这样的概率是很大的。当然，如果从最坏的情况考虑，还是我们提出的思路能保证优于直接从`1`到`N`检查的方法。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    bool queryString(string S, int N) {
        unordered_set<int> pool;
        for (int i = S.size() - 1; i >= 0; i--) {
            int tmp = 0;
            int power = 0;
            for (int j = i; j >= 0; j--) {
                if (S[j] == '1') {
                    tmp += pow(2, power);
                    if (tmp > 0 && tmp <= N) {
                        pool.insert(tmp);
                    }
                    if (tmp > N) {
                        break;
                    }
                }
                power++;
            }
        }
        return pool.size() == N;
    }
};

```

#### 复杂度分析
时间复杂度: O(n^2)
空间复杂度: O(1)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/GSc-F_jlYWk)，欢迎关注！