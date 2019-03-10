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


#### 解题思路


#### 示例代码 (cpp)


#### 复杂度分析
时间复杂度:
空间复杂度:

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/GSc-F_jlYWk)，欢迎关注！