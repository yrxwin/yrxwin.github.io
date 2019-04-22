---
title: '[Leetcode 1027] Longest Arithmetic Sequence'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-04-21 20:10:53
tags: ['Google', 'Microsoft', 'snapdeal', 'Dynamic Programming']
keywords: ['Google', 'Microsoft', 'snapdeal', 'Dynamic Programming']
description:
---
#### 原题说明
Given an array `A` of integers, return the length of the longest arithmetic subsequence in `A`.

Recall that a subsequence of `A` is a list `A[i_1]`, `A[i_2]`, ..., `A[i_k]` with `0 <= i_1 < i_2 < ... < i_k <= A.length - 1`, and that a sequence `B` is arithmetic if `B[i+1] - B[i]` are all the same value (for `0 <= i < B.length - 1`).

{% blockquote %}
**Example 1:**
**Input:** `[3,6,9,12]`
**Output:** `4`
**Explanation:** 
The whole array is an arithmetic sequence with steps of length = 3.
{% endblockquote %}

{% blockquote %}
**Example 2:**
**Input:** `[9,4,7,2,10]`
**Output:** `3`
**Explanation:** 
The longest arithmetic subsequence is `[4,7,10]`.
{% endblockquote %}

{% blockquote %}
**Example 3:**
**Input:** `[20,1,15,3,10,5,8]`
**Output:** `4`
**Explanation:** 
The longest arithmetic subsequence is `[20,15,10,5]`.
{% endblockquote %}
 

**Note:**
1. `2 <= A.length <= 2000`
2. `0 <= A[i] <= 10000`

<!--more-->

#### 解题思路
动态规划，`dp[diff][idx]`表示等差为`diff`，以系数`idx`结尾的最长子序列长度。
`dp[diff][idx]`最初都为`0`，但凡遍历到的最小则为`2`。
双重循环，外循环系数`i`，内循环系数`j`，每一次我们让`j`从`0`走到`i-1`，通过`A[j]`与`A[i]`组成等差数列(`diff = A[i] - A[j]`)，更新`dp[diff][i]`的值为：`max(dp[diff][j] + 1, dp[diff][i])`，同时更新返回值`res = max(res, dp[diff][i])`
最后返回`res`即可。
**Testcase 示例**
```
[3, 6, 9, 12]
i = 1, j = 0: dp[3][1] = 2, dp[3][1] = max(dp[3][0] + 1, dp[3][1]) = 2
i = 2, j = 0: dp[6][2] = 2, ...
i = 2, j = 1: dp[3][2] = 2, dp[3][2] = max(dp[3][1] + 1, dp[3][2]) = 3
i = 3, j = 0: dp[9][3] = 2, ...
i = 3, j = 1: dp[6][3] = 2, ...
i = 3, j = 2: dp[3][3] = 2, dp[3][3] = max(dp[3][2] + 1, dp[3][3]) = 4
```

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int longestArithSeqLength(vector<int>& A) {
        unordered_map<int, unordered_map<int, int>> dp;
        if (A.size() <= 1) {
            return A.size();
        }
        int res = 2;
        for (int i = 0; i < A.size(); ++i) {
            for (int j = 0; j < i; ++j) {
                int diff = A[i] - A[j];
                if (!dp[diff].count(i)) {
                    dp[diff][i] = 2;
                }
                dp[diff][i] = max(dp[diff][j] + 1, dp[diff][i]);
                res = max(res, dp[diff][i]);
            }
        }
        return res;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int longestArithSeqLength(int[] A) {
        Map<Integer, Map<Integer, Integer>> dp = new HashMap<>();
        int res = 2;
        for (int i = 0; i < A.length; i++) {
            for (int j = i + 1; j < A.length; j++) {
                Map<Integer, Integer> m = dp.computeIfAbsent(A[j] - A[i], d -> new HashMap<>());
                m.put(j, m.getOrDefault(i, 1) + 1);
                res = Math.max(res, m.get(j));
            }
        }
        return res;
    }
}
```

#### 示例代码 (python)
```python
class Solution(object):
    def longestArithSeqLength(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        dp = {}
        for i in xrange(len(A)):
            for j in xrange(i + 1, len(A)):
                dp[j, A[j] - A[i]] = dp.get((i, A[j] - A[i]), 1) + 1
        return max(dp.values())
```

#### 复杂度分析
时间复杂度: `O(N^2)`
空间复杂度: `O(N^2)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/mSplC7Q-Rm8)，欢迎关注！