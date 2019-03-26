---
title: '[Leetcode 995] Minimum Number of K Consecutive Bit Flips'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-03-11 23:14:18
tags: ['Akuna Capital', 'Greedy', 'Sliding Window', 'Hard']
keywords: ['Akuna Capital', 'Greedy', 'Sliding Window', 'Hard']
description:
---
#### 原题说明
In an array `A` containing only `0`s and `1`s, a K-bit flip consists of choosing a (contiguous) subarray of length `K` and simultaneously changing every `0` in the subarray to `1`, and every `1` in the subarray to `0`.

Return the minimum number of K-bit flips required so that there is no `0` in the array.  If it is not possible, return `-1`.

**Example 1:**
{% blockquote %}
**Input:** `A = [0,1,0], K = 1`
**Output:** `2`
**Explanation:** Flip `A[0]`, then flip `A[2]`.
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** `A = [1,1,0], K = 2`
**Output:** `-1`
**Explanation:** No matter how we flip subarrays of size `2`, we can't make the array become `[1,1,1]`.
{% endblockquote %}

**Example 3:**
{% blockquote %}
**Input:** `A = [0,0,0,1,0,1,1,0], K = 3`
**Output:** `3`
**Explanation:**
Flip `A[0]`,`A[1]`,`A[2]`: `A` becomes `[1,1,1,1,0,1,1,0]`
Flip `A[4]`,`A[5]`,`A[6]`: `A` becomes `[1,1,1,1,1,0,0,0]`
Flip `A[5]`,`A[6]`,`A[7]`: `A` becomes `[1,1,1,1,1,1,1,1]`
{% endblockquote %}

**Note:**
1. `1 <= A.length <= 30000`
2. `1 <= K <= A.length`
<!-- more -->

#### 解题思路
先从数组的最左元素开始，因为要改变最左元素的状态，只能以这个元素为起始点。

如果这个元素是`1`，那么不需要`kBitFlip`操作；如果这个元素是`0`， 那么需要进行一次`kBitFlip`操作， `kBitFlip`的操作次数 `++ans`。当元素值变为`1`之后，进入下一个元素判断。

这样的操作最多进行`A.size() - K + 1`次。这样能保证`index`从`0`到`A.size() - K`的值都是`1`，只需要对剩下的元素进行检查。如果有`0`，`return -1`；否则`return` `kBitFlip`的操作次数`ans`。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int minKBitFlips(vector<int>& A, int K) {
        if (K > A.size()) {
            for (auto i = 0; i < A.size(); ++i) {
                if (A[i] == 0)
                    return -1;
            }
            return 0;
        } 
        int ans = 0;
        for (auto i = 0; i < A.size() - K + 1; ++i) {
            if (A[i] == 0) {
                kBitFlip(A, K, i);
                ++ans;
            }
        }
        for (auto j = A.size() - K; j < A.size(); ++j) {
            if (A[j] == 0) {
                return -1;
            }
        }
        return ans;
    }
    void kBitFlip(vector<int>& A, const int K, const int loc) {
        for (auto i = loc; i < loc + K; ++i) {
            A[i] = (A[i]==1) ? 0 : 1;
        }
    }
};
```

#### 复杂度分析
时间复杂度: `O(N * K)`
空间复杂度: `O(1)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/IUSI727XIwg)，欢迎关注！