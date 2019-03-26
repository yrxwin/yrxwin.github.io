---
title: '[Leetcode 994] Rotting Oranges'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-02-17 23:17:05
tags: [Amazon, Breadth-first Search]
keywords: [Amazon, Breadth-first Search]
description: 
---
#### 原题说明
In a given grid, each cell can have one of three values:
- the value 0 representing an empty cell;
- the value 1 representing a fresh orange;
- the value 2 representing a rotten orange.

Every minute, any fresh orange that is adjacent (4-directionally) to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange.  If this is impossible, return -1 instead.

 
**Example 1:**
{% asset_img oranges.png 400 %}{% blockquote %}
**Input:** `[[2,1,1],[1,1,0],[0,1,1]]`
**Output:** `4`
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input**: `[[2,1,1],[0,1,1],[1,0,1]]`
**Output**: `-1`
**Explanation**:  The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.
{% endblockquote %}

**Example 3:**
{% blockquote %}
**Input**: `[[0,2]]`
**Output**: `0`
**Explanation**:  Since there are already no fresh oranges at minute 0, the answer is just 0.
{% endblockquote %}

**Note:**
1. `1 <= grid.length <= 10`
2. `1 <= grid[0].length <= 10`
3. `grid[i][j] is only 0, 1, or 2`.
<!-- more -->

#### 解题思路
这类问题问需要多少时间遍历整个二维数组，并且每次遍历一次，自然想到要用广度优先搜索（BFS）来做：
1. 遍历二维数组，统计新鲜橘子(value=1)的数量`fresh_count`，并且将烂橘子(value=2)的坐标加入队列qu
2. minutes为经过的时间，如果队列qu非空且`fresh_count`不为0，则用BFS方法遍历当前队列qu中所有元素
    i）如果其周围有新鲜橘子，则`fresh_count--`，将其坐标加入qu，并更新为烂橘子(value=2)
    ii) 否则直接跳过
   每一轮遍历完使`minutes++`
3. 如果`fresh_count`不为0，则返回-1，否则返回`minutes`

#### 示例代码 (cpp)
```cpp
class Solution {
    vector<vector<int>> dirs = {{-1, 0}, {0, 1}, {0, -1}, {1, 0}};
public:
    int orangesRotting(vector<vector<int>>& grid) {
        queue<int> qu;
        int m = grid.size();
        if (!m) {
            return 0;
        }
        int n = grid[0].size();
        int minutes = 0, fresh_count = 0;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] == 1) {
                    ++fresh_count;
                } else if (grid[i][j] == 2) {
                    qu.push(i * n + j);
                }
            }
        }
        while (!qu.empty() && fresh_count != 0) {
            for (int i = qu.size(); i > 0; --i) {
                int cur = qu.front();
                qu.pop();
                for (const auto& dir : dirs) {
                    int x = cur / n + dir[0];
                    int y = cur % n + dir[1];
                    if (x < 0 || x >= m || y < 0 || y >= n || grid[x][y] != 1) {
                        continue;
                    }
                    grid[x][y] = 2;
                    qu.push(x * n + y);
                    --fresh_count;
                }
            }
            ++minutes;
        }
        if (fresh_count) {
            return -1;
        }
        return minutes;
    }
};
```

#### 复杂度分析
因为只遍历了一遍二维数组，所以时间空间复杂度都是二维数组中元素个数
时间复杂度: `O(m * n)`
空间复杂度: `O(m * n)`

#### 归纳总结
这道题稍微与一般BFS不同的是截止条件判断需要为:`!qu.empty() && fresh_count != 0`，即除了队列为空外，还要判断新鲜橘子还有没有。
另外，遍历二维数组时常用的找到周边上下左右坐标的方法:
```cpp
vector<vector<int>> dirs = {{-1, 0}, {0, 1}, {0, -1}, {1, 0}}
```
以及如果将二维坐标`(i, j)`转换为一维的index: `i * n + j` 也是需要熟练掌握的。
我们在**Youtube**上更新了[视频讲解](https://youtu.be/GSc-F_jlYWk)，欢迎关注！
