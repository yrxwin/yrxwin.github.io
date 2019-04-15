---
title: '[Leetcode 1016] Binary String With Substrings Representing 1 To N'
categories:
  - leetcode
author: '大猩猩，猩猩管理员'
date: 2019-04-10 23:10:52
tags: ['String', 'Google']
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

<!--more-->

#### 解题思路
这道题最重要的是估计`N`的上限，超过上限全都是`false`了。
由于题目中给了`S.length`最大为`1000`，我们考虑11位二进制数（也就是1024 - 2047）总共有 > 1000个
然而长度为1000的字符串，取连续的11位数（即长度为11的子串），总共只能取`1000 - 10 = 990`种 < 1000 => 不可能包含所有11位binary，所以N最多也就是11位数，其上限为`2^11 = 2048`
一般来说（分析时间复杂度会用到）：`2^(k+1) - 2^k <= S.length => 2^k <= S.length`, 上限为`2^(k+1)`次也就是`2 * S.length`
知道了这一上限，我们直接暴力求解即可: 将1 - N每一个转化为二进制，然后在S中寻找看是否能找到。
另外有一个优化是：我们只需要算 > N/2的数，因为如果一个数k的二进制是`S`的子串，那么`k/2`只不过少了一位，一定也是`S`的子串，没有必要再算。

#### 示例代码 (cpp)
```cpp
class Solution {
    string intToBinary(int N) {
        string binary = "";
        while (N) {
            if (N & 1) {
                binary = "1" + binary;
            } else {
                binary = "0" + binary;
            }
            N /= 2;
        }
        return binary;
    }
public:
    bool queryString(string S, int N) {
        if (N >= 2048) {
            return false;
        }
        for (int i = N; i > N / 2; --i) {
            if (S.find(intToBinary(i)) == string::npos) {
                return false;
            }
        }
        return true;
    }
};
```

#### 示例代码（java）
```java
class Solution {
    public boolean queryString(String S, int N) {
        for (int i = N; i > N / 2; --i)
            if (!S.contains(Integer.toBinaryString(i)))
                return false;
        return true;
    }
}
```

#### 示例代码（python）
```python
class Solution(object):
    def queryString(self, S, N):
        """
        :type S: str
        :type N: int
        :rtype: bool
        """
        return all(bin(i)[2:] in S for i in xrange(N, N / 2, -1))
```

#### 复杂度分析
时间复杂度: `O(S.length^2)` 平方是因为每一次在`S`中查找子串需要`O(S.length)`的时间，而`N`最大就是`2 * S.length`
空间复杂度: `O(log(S.length))` 因为转化成字符串需要空间，`N`最大是`2 * S.length`, 对应二进制的长度就是`O(log(S.length))`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/bYoc35QYUhI)，欢迎关注！