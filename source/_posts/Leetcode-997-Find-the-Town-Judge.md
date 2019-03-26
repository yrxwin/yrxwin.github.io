---
title: '[Leetcode 997] Find the Town Judge'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-03-10 00:11:16
tags: ['Arista', 'Graph']
keywords: ['Arista', 'Graph']
description:
---
#### 原题说明
In a town, there are `N` people labelled from `1` to `N`.  There is a rumor that one of these people is secretly the town judge.

If the town judge exists, then:
1. The town judge trusts nobody.
2. Everybody (except for the town judge) trusts the town judge.
3. There is exactly one person that satisfies properties 1 and 2.
You are given trust, an array of pairs `trust[i] = [a, b]` representing that the person labelled a trusts the person labelled `b`.

If the town judge exists and can be identified, return the label of the town judge.  Otherwise, return `-1`.

**Example 1:**
{% blockquote %}
**Input:** `N = 2, trust = [[1,2]]`
**Output:** `2`
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** `N = 3, trust = [[1,3],[2,3]]`
**Output:** `3`
{% endblockquote %}

**Example 3:**
{% blockquote %}
**Input:** `N = 3, trust = [[1,3],[2,3],[3,1]]`
**Output:** `-1`
{% endblockquote %}

**Example 4:**
{% blockquote %}
**Input:** `N = 3, trust = [[1,2],[2,3]]`
**Output:** `-1`
{% endblockquote %}

**Example 5:**
{% blockquote %}
**Input:** `N = 4, trust = [[1,3],[1,4],[2,3],[2,4],[4,3]]`
**Output:** `3`
{% endblockquote %}

**Note:**
1. `1 <= N <= 1000`
2. `trust.length <= 10000`
3. `trust[i]` are all different
4. `trust[i][0] != trust[i][1]`
5. `1 <= trust[i][0], trust[i][1] <= N`
<!-- more -->

#### 解题思路
这是一道单向图的题，实际上我们要寻找图中入度为`N-1`,出度为`0`的点。
因为每个点的入度最大即为`N-1`（即村上所有其他人都`trust`他）,所以`入度 - 出度 = N - 1`是入度为`N-1`,出度为`0`的充分必要条件，所以本题用一个`counts`数组统计每个点入度和出度之差，遍历`trust`来更新`counts`数组，之后再遍历`counts`数组寻找值为`N-1`的点，返回坐标即可，如果在`counts`中不存在值为`N-1`的点，说明不存在judge，返回`-1`。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int findJudge(int N, vector<vector<int>>& trust) {
        vector<int> counts(N + 1, 0);
        for (const auto& relation : trust) {
            counts[relation[0]]--;
            counts[relation[1]]++;
        }
        for (int i = 1; i <= N; ++i) {
            if (counts[i] == N - 1) {
                return i;
            }
        }
        return -1;
    }
};
```

#### 复杂度分析
时间复杂度: `O(T + N)`, `T`为`trust`数组的长度
空间复杂度: `O(N)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/clkmS3_AP2w)，欢迎关注！