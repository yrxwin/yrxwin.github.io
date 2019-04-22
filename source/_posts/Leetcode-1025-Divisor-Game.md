---
title: '[Leetcode 1025] Divisor Game'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2019-04-21 19:52:18
tags:
keywords:
description:
---
#### 原题说明
Alice and Bob take turns playing a game, with Alice starting first.

Initially, there is a number N on the chalkboard.  On each player's turn, that player makes a move consisting of:

Choosing any `x` with `0 < x < N` and `N % x == 0`.
Replacing the number `N` on the chalkboard with `N - x`.
Also, if a player cannot make a move, they lose the game.

Return True if and only if Alice wins the game, assuming both players play optimally.
 
{% blockquote %}
**Example 1:**
**Input:** `2`
**Output:** `true`
**Explanation:** Alice chooses 1, and Bob has no more moves.
{% endblockquote %}
{% blockquote %}
**Example 2:**
**Input:** `3`
**Output:** `false`
**Explanation:** Alice chooses 1, Bob chooses 1, and Alice has no more moves.
{% endblockquote %}

**Note:**
1. `1 <= N <= 1000`
<!--more-->

#### 解题思路
如果`N`为偶数，则坚持选择`x = 1`，对方得到`N - 1`为大于`0`的奇数
如果`N`为奇数：
  1. 如果`N > 1`, 其因子必然也是奇数，所以无论选择任何`x`，`N - x`都将变为偶数
     由于`x < N`，给予对方的`N - x`必然是 `> 0`的偶数
  2. 如果`N = 1`，直接失败。
 综上，`N`为偶数时必然大于`0`，只需要坚持选择`x = 1`，最终对方会得到`N = 1`而失败。
 所以`N`为偶数时返回`true`。

{% blockquote %}
用Flip Game II的方法也可以。
{% endblockquote %}

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    bool divisorGame(int N) {
        return N % 2 == 0;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public boolean divisorGame(int N) {
        return N % 2 == 0;
    }
}
```

#### 示例代码 (python)
```python
class Solution(object):
    def divisorGame(self, N):
        """
        :type N: int
        :rtype: bool
        """
        return N % 2 == 0
```

#### 复杂度分析
时间复杂度: `O(1)`
空间复杂度: `O(1)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/p5CeIwHRVxQ)，欢迎关注！