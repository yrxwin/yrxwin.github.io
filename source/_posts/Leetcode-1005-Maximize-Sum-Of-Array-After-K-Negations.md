---
title: '[Leetcode 1005] Maximize Sum Of Array After K Negations'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-03-23 18:42:52
tags: ['druva', 'Greedy']
keywords: ['druva', 'Greedy']
description:
---
#### 原题说明
Given an array `A` of integers, we must modify the array in the following way: we choose an i and replace `A[i]` with `-A[i]`, and we repeat this process `K` times in total.  (We may choose the same index `i` multiple times.)

Return the largest possible sum of the array after modifying it in this way.

**Example 1:**
{% blockquote %}
**Input:** `A = [4,2,3], K = 1`
**Output:** `5`
**Explanation:** Choose indices (1,) and A becomes `[4,-2,3]`.
{% endblockquote %}
**Example 2:**
{% blockquote %}
**Input:** `A = [3,-1,0,2], K = 3`
**Output:** 6
**Explanation:** Choose indices (1, 2, 2) and A becomes `[3,1,0,2]`.
{% endblockquote %}
**Example 3:**
{% blockquote %}
**Input:** `A = [2,-3,-1,5,-4], K = 2`
**Output:** `13`
**Explanation:** Choose indices (1, 4) and A becomes `[2,3,-1,5,4]`.
{% endblockquote %}
 
**Note:**
1. `1 <= A.length <= 10000`
2. `1 <= K <= 10000`
3. `-100 <= A[i] <= 100`

<!-- more -->

#### 解题思路
我们首先排序数组`A`，然后按顺序从小到大遍历数组，将负的元素变为正数，每改变一个元素，需要`--K`来记录翻转的个数，停止的条件有三个：
 1）如果数组遍历完毕
 2）如果`K`不再大于`0`，则说明翻转次数用完了
 3）如果当前元素`A[i] >= 0`, 为了保证最终结果最大，不用继续翻转
遍历结束后得到的`A`的和已经是最大可能，当然还必须将剩余的`K`次翻转用掉：
 1）如果K为偶数，只需要对任意元素翻转相同次数，`A`的和不变
 2）如果K为奇数，则对最小的元素翻转K次，最终结果为A的和减去两倍的最小元素
所以我们再顺序遍历一遍数组（用`getSum`函数），取得当前的和`sum`，以及数组最小元素`min_ele`。
返回 `sum - (K % 2) * 2 * min_ele` 即可。

#### 示例代码 (cpp)
```cpp
class Solution {
    // Get the sum of vector A, and make min_ele equal to the minimum element in A
    int getSum(const vector<int>& A, int& min_ele) {
        int sum = 0;
        min_ele = INT_MAX;
        for (auto ele : A) {
            min_ele = min(min_ele, ele); 
            sum += ele;
        }
        return sum;
    }
public:
    int largestSumAfterKNegations(vector<int>& A, int K) {
        sort(A.begin(), A.end());
        for (int i = 0; K > 0 && i < A.size() && A[i] < 0; ++i, --K) {
            A[i] = -A[i];
        }
        int min_ele;
        int sum = getSum(A, min_ele);
        return sum - (K % 2) * min_ele * 2;
    }
};
```

#### 示例代码 (python)
```python
class Solution(object):
    def largestSumAfterKNegations(self, A, K):
        """
        :type A: List[int]
        :type K: int
        :rtype: int
        """
        A.sort()
        i = 0
        while i < len(A) and i < K and A[i] < 0:
            A[i] = -A[i]
            i += 1
        return sum(A) - (K - i) % 2 * min(A) * 2
```

#### 示例代码 (java)
```java
class Solution {
    public int largestSumAfterKNegations(int[] A, int K) {
        Arrays.sort(A);
        for (int i = 0; K > 0 && i < A.length && A[i] < 0; ++i, --K)
            A[i] = -A[i];
        int res = 0, min = Integer.MAX_VALUE;
        for (int a : A) {
            res += a;
            min = Math.min(min, a);
        }
        return res - (K % 2) * min * 2;
    }
}
```

#### 复杂度分析
时间复杂度: `O(nlog(n))`
空间复杂度: `O(1)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/7iMipH_1mKo?list=PLwVaSd26TDqoGHGYifjGqGx9o87LuuRcS)，欢迎关注！