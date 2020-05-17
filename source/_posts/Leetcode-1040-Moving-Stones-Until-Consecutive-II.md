---
title: Leetcode-1040-Moving-Stones-Until-Consecutive-II
categories:
  - leetcode
author: '大猩猩'
date: 2020-05-17 13:43:57
tags: ['Facebook','Array','Sliding Window']
keywords: ['Facebook','Array','Sliding Window']
description:
---
#### 原题说明
On an *infinite* number line, the position of the i-th stone is given by `stones[i]`.  Call a stone an *endpoint* stone if it has the smallest or largest position.

Each turn, you pick up an endpoint stone and move it to an unoccupied position so that it is no longer an endpoint stone.

In particular, if the stones are at say, `stones = [1,2,5]`, you *cannot* move the endpoint stone at position 5, since moving it to any position (such as 0, or 3) will still keep that stone as an endpoint stone.

The game ends when you cannot make any more moves, ie. the stones are in consecutive positions.

When the game ends, what is the minimum and maximum number of moves that you could have made?  Return the answer as an length 2 array: `answer = [minimum_moves, maximum_moves]`

**Example 1**
{% blockquote %}
**Input:** [7,4,9]
**Output:** [1,2]
**Explanation:** We can move 4 -> 8 for one move to finish the game.
Or, we can move 9 -> 5, 4 -> 6 for two moves to finish the game.
{% endblockquote %}

**Example 2**
{% blockquote %}
**Input:** [6,5,4,3,10]
**Output:** [2,3]
**Explanation:** We can move 3 -> 8 then 10 -> 7 to finish the game.
Or, we can move 3 -> 7, 4 -> 8, 5 -> 9 to finish the game.
Notice we cannot move 10 -> 2 to finish the game, because that would be an illegal move.
{% endblockquote %}

**Example 3**
{% blockquote %}
**Input:** [100,101,104,102,103]
**Output:** [0,0]
{% endblockquote %}

**Note**
{% blockquote %}
1. `3 <= stones.length <= 10^4`
2. `1 <= stones[i] <= 10^9`
3. `stones[i] have distinct values.`
{% endblockquote %}

<!--more-->

#### 解题思路
题目要求求出让石头堆连续排列的最大和最小移动步数。我们需要将最大和最小移动步数分成两个问题考虑。将总共的石头堆的数目用`n`表示。另外，我们首先需要做预处理，将给我们的`array`做个排序。

对最大移动步数，用贪心的思想，要么都移动到最左端，要么都移动到最右端。我们需要考察`stones[n-2]`到`stones[0]`和`stones[n-1]`到`stones[1]`的间距，进行比较。在这两个选择中。选择空的position最多的那个。同时，因为一开始需要将一个`endpoint`做一次移动，所以需要额外加上这次步骤。

对最小移动步数，用sliding window 的方法。`window`的长度是`n`。计算每个window中，最多已经被填满的空间数量。剩下的未被填满的空间就是最小的移动数目。

需要额外注意的是，这里存在一种`corner case`违背了上述的结论，需要特殊处理。举例如下：
如果石头堆是`1，2，3，6`, 那么`n`是`4`，对于第一个`window`，它有一个空位置，在`4`， 但是`6`不能移动到`4`，这不是一个`valid move`，所以必须将`1` 移动到`5`，`6`移动到`4`，必须至少`2`步才能完成要求。

也就是说，当一个`window`的长度是n，它包含了连续的n-1个非空位，同时这n-1个非空位在原来石头堆的位置也是连续的，那我们就需要`2`步才能完成石头堆的最小移动。
#### 示例代码 (cpp)
```cpp
class Solution {
public:
    vector<int> numMovesStonesII(vector<int>& stones) {
        int n = stones.size();
        sort(stones.begin(), stones.end());
        int upper;
        int lower = n;
        // calculate upper bound
        upper = max(stones[n-1] - stones[1] + 1 - n  + 1, stones[n - 2] - stones[0] + 1 - n + 1);
        // calculate lower bound
        int start = 0;
        for (auto&& end = 0; end < n; ++end) {
            while (stones[end] - stones[start] + 1 > n) {
                start++;
            }
            if (stones[end] - stones[start] + 1 == n - 1 && end - start + 1 == n - 1) {
                lower = min(lower, 2);
            }
            else {
                lower = min(lower, n - (end - start + 1));
            }
        }
        return {lower, upper};
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int[] numMovesStonesII(int[] stones) {
        Arrays.sort(stones);
        int i = 0, n = stones.length, lower = n;
        int upper = Math.max(stones[n - 1] - n + 2 - stones[1], stones[n - 2] - stones[0] - n + 2);
        for (int j = 0; j < n; ++j) {
            while (stones[j] - stones[i] >= n) ++i;
            if (j - i + 1 == n - 1 && stones[j] - stones[i] == n - 2)
                lower = Math.min(lower, 2);
            else
                lower = Math.min(lower, n - (j - i + 1));
        }
        return new int[] {lower, upper};
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def numMovesStonesII(self, stones: List[int]) -> List[int]:
        stones.sort()
        i, n, lower = 0, len(stones), len(stones)
        upper = max(stones[-1] - n + 2 - stones[1], stones[-2] - stones[0] - n + 2)
        for j in range(n):
            while stones[j] - stones[i] >= n: i += 1
            if j - i + 1 == n - 1 and stones[j] - stones[i] == n - 2:
                lower = min(lower, 2)
            else:
                lower = min(lower, n - (j - i + 1))
        return [lower, upper]
```

#### 复杂度分析
时间复杂度: O(nlogn + n + 1) = O(nlogn)
空间复杂度: O(1)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://www.youtube.com/watch?v=0SoB5F5GUFg)，欢迎关注！