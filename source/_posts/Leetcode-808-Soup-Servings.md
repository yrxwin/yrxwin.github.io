---
title: '[Leetcode 808] Soup Servings'
categories:
  - leetcode
author: '中猩猩'
date: 2018-04-10 00:25:11
tags: [Google, Dynamic Programming]
keywords:
description:
---
#### 原题说明
There are two types of soup: type A and type B. Initially we have N ml of each type of soup. There are four kinds of operations:

1. Serve 100 ml of soup A and 0 ml of soup B
2. Serve 75 ml of soup A and 25 ml of soup B
3. Serve 50 ml of soup A and 50 ml of soup B
4. Serve 25 ml of soup A and 75 ml of soup B

When we serve some soup, we give it to someone and we no longer have it.  Each turn, we will choose from the four operations with equal probability 0.25. If the remaining volume of soup is not enough to complete the operation, we will serve as much as we can.  We stop once we no longer have some quantity of both types of soup.

Note that we do not have the operation where all 100 ml's of soup B are used first.  

Return the probability that soup A will be empty first, plus half the probability that A and B become empty at the same time.

{% blockquote %}
**Example:**
**Input:** N = 50
**Output:** 0.625
**Explanation:** 
If we choose the first two operations, A will become empty first. For the third operation, A and B will become empty at the same time. For the fourth operation, B will become empty first. So the total probability of A becoming empty first plus half the probability that A and B become empty at the same time, is 0.25 * (1 + 1 + 0.5 + 0) = 0.625.
{% endblockquote%}
**Notes:**
- 0 <= N <= 10^9. 
- Answers within 10^-6 of the true value will be accepted as correct.
<!-- more -->

#### 解题思路
虽然题目乍一看比较复杂，好像让你去算概率，难道是概率题，不是编程题？
但稍加分析，可以总结如下信息：
初始状态下，`A`和`B`同时拥有`N`的汤。
终结状态下，
- 若`A`先被倒完，则`A`剩余的汤为`0`或`负数`。（因为在剩余汤不足时，可以倒比所需少的量）此时`B`剩余的汤应当大于`0`。
- 若`A`和`B`同时倒完，则`A`和`B`的汤均为`0`或`负数`。
- 若`B`先被倒完，则`B`剩余的汤为`0`或`负数`。此时`A`剩余的汤应当大于`0`。

有了初始状态和终结状态，可以想到用递归的方法来求解。在结算时，因为同时倒完的概率只需计算一半。因此，判断其为A先倒完时，返回`1`，而同时倒完时返回`0.5`。
又考虑到所有操作中汤的份量都是`25`的倍数，实际中间状态的可能最多为`Ceil(N/25)^2`。因此可以用动态规划来避免冗余计算。

以上基本实现了本题的主体解法。然而这是一个两次方复杂度的解法，随着`N`的上升，需要指数的时间去计算。此时我们可以利用题目中提到的精度要求来做文章。让我们从概率的角度重新审题。四个操作对汤消耗的期望值为`A = 62.5, B = 37.5`。`A`的消耗速度远高于`B`。因此，当`N`变大时，`A`先倒完的概率趋向于1。我们尝试不断递增的`N`来运行程序后，可以发现当N>4800时，所得概率已经落在`1 - 10^-6`内。也就是说所有大于4800的输入，都可以直接输出1作为结果。

#### 示例代码 (cpp)
```cpp
class Solution {
    double recurse(int a, int b, unordered_map<int, unordered_map<int, double>>& memo) {
        if (a <= 0 && b > 0) {
            return 1;
        }
        if (a <= 0 && b <= 0) {
            return 0.5;
        }
        if (b <= 0) {
            return 0;
        }
        if (memo.count(a) && memo[a].count(b)) {
            return memo[a][b];
        }
        double prob = (recurse(a - 100, b, memo) + recurse(a - 75, b - 25, memo) + recurse(a - 50, b - 50, memo) + recurse(a - 25, b - 75, memo)) / 4.0;
        memo[a][b] = prob;
        return prob;
    }
public:
    double soupServings(int N) {
        if (N >= 5000) {
            return 1;
        }
        unordered_map<int, unordered_map<int, double>> memo;
        return recurse(N, N, memo);
    }
};
```

#### 示例代码 (python)
```python
class Solution(object): 
    def soupHelper(self, A, B, state):
        if (A, B) in state:
            return state[A, B]
        
        if A <=0 or B <= 0:
            if A <= 0 and B <= 0:
                return 0.5
            if B > 0:
                return 1
            return 0
        prob = 0
        prob += self.soupHelper(A - 100, B, state)
        prob += self.soupHelper(A - 75, B - 25, state)
        prob += self.soupHelper(A - 50, B - 50, state)
        prob += self.soupHelper(A - 25, B - 75, state)
        state[A, B] = 0.25 * prob
        return state[A, B]
        
    def soupServings(self, N):
        """
        :type N: int
        :rtype: float
        """
        if N > 4800:
            return 1.
        state = dict()
        prob = self.soupHelper(N, N, state)
        return prob
```

#### 复杂度分析
当N<=4800时：
- 时间复杂度: `O(n^2)`
- 空间复杂度: `O(n^2)`

当N>4800时：
- 时间复杂度: `O(1)`
- 空间复杂度: `O(1)`

#### 归纳总结
本题主要有两个难点:
- 想到用递归结合动态规划的办法来求解概率。
- 利用精度和定性的概率判断，避免计算时间会指数量级的膨胀
