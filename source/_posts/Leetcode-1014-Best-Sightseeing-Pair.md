---
title: '[Leetcode 1014] Best Sightseeing Pair'
categories:
  - leetcode
author: '大猩猩，猩猩管理员'
date: 2019-04-10 21:37:40
tags: ['wayfair', 'Array']
keywords: ['wayfair', 'Array']
description:
---

#### 原题说明

Given an array `A` of positive integers, `A[i]` represents the value of the `i` - th sightseeing spot, and two sightseeing spots `i` and `j` have distance `j - i` between them.

The score of a pair (`i < j`) of sightseeing spots is (`A[i] + A[j] + i - j`) : the sum of the values of the sightseeing spots, minus the distance between them.

Return the maximum score of a pair of sightseeing spots.

**Example 1:**
{% blockquote %}
**Input:** `[8, 1, 5, 2, 6]`
**Output:** `11`
**Explanation:** `i = 0, j = 2, A[i] + A[j] + i - j = 8 + 5 + 0 - 2 = 11`.
{% endblockquote %}
 
**Note:**
1. `2 <= A.length <= 50000`
2. `1 <= A[i] <= 1000`

<!-- more -->

#### 解题思路
遍历数组`A`，我们用`max_score`来记录当前最大的分数，用`pre_max`来记录当前元素之前最高的分数
每遍历一个元素`a`，我们首先更新`max_score`: `max_score = max(max_score, a + pre_max)`
然后更新`pre_max`: `pre_max = max(pre_max, a) - 1`
这里`-1`是因为每往后一个元素，距离会增加`1`

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int maxScoreSightseeingPair(vector<int>& A) {
        int max_score = 0, pre_max = 0;
        for (auto a : A) {
            max_score = max(max_score, a + pre_max);
            pre_max = max(pre_max, a) - 1;
        }
        return max_score;
    }
};
```

#### 示例代码（java）
```java
class Solution {
    public int maxScoreSightseeingPair(int[] A) {
        int res = 0, cur = 0;
        for (int a: A) {
            res = Math.max(res, cur + a);
            cur = Math.max(cur, a) - 1;
        }
        return res;
    }
};
```
#### 示例代码（python）
```python
class Solution(object):
    def maxScoreSightseeingPair(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        cur = res = 0
        for a in A:
            res = max(res, cur + a)
            cur = max(cur, a) - 1
        return res
```

#### 复杂度分析
时间复杂度: `O(n)`
空间复杂度: `O(1)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/CoyAaGEhmFY)，欢迎关注！