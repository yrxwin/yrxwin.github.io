---
title: '[Leetcode 1020] Number of Enclaves'
categories:
  - leetcode
author: '大猩猩'
date: 2019-04-11 23:00:34
tags: [Depth-first Search]
keywords:
description:
---

#### 原题说明
Given a 2D array `A`, each cell is `0` (representing sea) or `1` (representing land)

A move consists of walking from one land square `4`-directionally to another land square, or off the boundary of the grid.

Return the number of land squares in the grid for which we cannot walk off the boundary of the grid in any number of moves.

Return the largest possible sum of the array after modifying it in this way.

**Example 1:**
{% blockquote %}
**Input:** `[[0,0,0,0],[1,0,1,0],[0,1,1,0],[0,0,0,0]]`
**Output:** `3`
**Explanation:** There are three 1s that are enclosed by 0s, and one 1 that isn't enclosed because its on the boundary.
{% endblockquote %}
**Example 2:**
{% blockquote %}
**Input:** `[[0,1,1,0],[0,0,1,0],[0,0,1,0],[0,0,0,0]]`
**Output:** `0`
**Explanation:** All 1s are either on the boundary or can reach the boundary.
{% endblockquote %}
 
**Note:**
1. `1 <= A.length <= 500`
2. `1 <= A[i].length <= 500`
3. `0 <= A[i][j] <= 1`
4. All rows have the same size.

#### 解题思路
题目给出一个二维数组A，0表示sea，1表示land。要求求出不能连接到边界的land的数量。

题目很明显可以使用DFS的方法来求解。重点在于如果选择DFS。若是对每一个land进行DFS的方法来检查，会造成大量的重复计算。更好的方法是检查一个边界上的每一个land，以此为start point，通过DFS记录下它能达到的所有的land。这样就能保证所有能达到边界的land都会被visit到。同时，这样的方法能保证每个点至多只被check一次，保证了效率，时间复杂度为O(row \* col)。
    
最后返回所有没被visit过并且cell是 1(land)的个数。
    
##### 补充：
这里我们用一个二维数组visitMap来记录某个点是否被visit过，这样开辟了O(row \* col)的空间。如果允许改变A中的值，可以直接将visit过的land的点变成2。这样能避免额外空间的使用。


#### 示例代码 (cpp)
```cpp
class Solution {
private:
    vector<vector<int>> dirs= {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
public:
    int numEnclaves(vector<vector<int>>& A) {
        int row = A.size();
        int col = A[0].size();
        vector<vector<bool>> visitMap(row, vector<bool>(col, false));
        for (int r = 0; r < row; r++) {
            for (int c = 0; c < col; c++) {
                if (r == 0 || r == row - 1 || c == 0 || c == col -1) {
                    if (A[r][c] && !visitMap[r][c]) {
                        checkFunc(A, visitMap, r, c);
                    }
                }
            }
        }
        int ans = 0;
        for (int r = 0; r < row; r++) {
            for (int c = 0; c < col; c++) {
                if (!visitMap[r][c] && A[r][c]) {
                    ans++;
                }
            }
        }
        return ans;
    }
    void checkFunc(vector<vector<int>>& A, vector<vector<bool>>& visitMap, int r, int c) {
        visitMap[r][c] = true;
        for (auto dir : dirs) {
            int new_r = r + dir[0];
            int new_c = c + dir[1];
            if (new_r >= 0 && new_r < A.size() && new_c >= 0 && new_c < A[0].size()) {
                if (A[new_r][new_c] && !visitMap[new_r][new_c]) {
                    checkFunc(A, visitMap, new_r, new_c);
                }
            }
        }
    }
};
```

#### 复杂度分析
时间复杂度: O(row\*col)
空间复杂度: O(row\*col)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/GSc-F_jlYWk)，欢迎关注！