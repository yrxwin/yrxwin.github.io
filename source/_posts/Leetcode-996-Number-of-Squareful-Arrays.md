---
title: '[Leetcode 996] Number of Squareful Arrays'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-03-03 16:09:52
tags: ['Apple', 'Math', 'Backtracking', 'Graph']
keywords: ['Apple', 'Math', 'Backtracking', 'Graph']
description:
---
#### 原题说明
Given an array A of non-negative integers, the array is squareful if for every pair of adjacent elements, their sum is a perfect square.

Return the number of permutations of A that are squareful.  Two permutations A1 and A2 differ if and only if there is some index i such that `A1[i] != A2[i]`.

**Example 1:**
{% blockquote %}
**Input:** `[1,17,8]`
**Output:** `2`
**Explanation:** 
`[1,8,17]` and `[17,8,1]` are the valid permutations.
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** `[2,2,2]`
**Output:** `1`
{% endblockquote %}
 
**Note:** 
1. `1 <= A.length <= 12`
2. `0 <= A[i] <= 1e9`
<!-- more -->

#### 解题思路
经典的backtracking回溯算法:
用一个`vector<int> cur`记录当前的permutation, 用`vector<bool> used`记录第i个元素是否被选如当前的permutation中。
遍历过程中要判断重复元素的情况，因此需要先排序将重复的元素排在一起，每一轮遍历都只选择重复元素中第一个出现的。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int numSquarefulPerms(vector<int>& A) {
        if (A.size() <= 1)
            return 0;
        vector<int> cur;
        vector<vector<int>> res;
        vector<bool> used(A.size(),false);
        // vector A must be sorted, the test case is not complete
        sort(A.begin(), A.end());
        // do dfs
        dfs(A, res, cur, used);
        return res.size();
    }
    void dfs(vector<int>& nums, vector<vector<int>>& res, vector<int>& cur, vector<bool>& used) {
        if (cur.size() ==  nums.size()) {
            res.push_back(cur);            
            return;
        }
        for (int i = 0; i < nums.size(); i++) {
            // prune的过程
            if (used[i] || (i > 0 && !used[i-1] && nums[i]==nums[i-1])) { 
                continue;
            }
            
            // check if it is a valid insert
            if (cur.size() > 0 && !isSquare(cur.back() + nums[i])) { 
                continue;
            }
            used[i] = true;
            cur.push_back(nums[i]);
            dfs(nums, res, cur, used);
            
            // for backtracking in the next step
            cur.pop_back();
            used[i] = false;
        }
    }      
    bool isSquare(const int num) {
        if (num == 0 && num == 1)
            return true;
        int i = sqrt(num);
        return i * i == num;
    }
};
```

#### 复杂度分析
时间复杂度: `O(N!)` 因为一共有`N！`种可能的排列组合，每一种都会遍历一遍
空间复杂度: `O(N * N!) = O(N!)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/V5eeRgQsr6o)，欢迎关注！