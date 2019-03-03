---
title: '[Leetcode 1001] Grid Illumination'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-03-03 15:40:57
tags: ['Dropbox', 'Hash Table']
keywords: ['Dropbox', 'Hash Table']
description:
---
#### 原题说明
On a N x N grid of cells, each cell `(x, y)` with `0 <= x < N` and `0 <= y < N` has a lamp.

Initially, some number of lamps are on.  `lamps[i]` tells us the location of the i-th lamp that is on.  Each lamp that is on illuminates every square on its x-axis, y-axis, and both diagonals (similar to a Queen in chess).

For the i-th query `queries[i] = (x, y)`, the answer to the query is 1 if the cell `(x, y)` is illuminated, else 0.

After each query `(x, y)` \[in the order given by queries\], we turn off any lamps that are at cell `(x, y)` or are adjacent 8-directionally (ie., share a corner or edge with cell `(x, y)`.)

Return an array of answers.  Each value `answer[i]` should be equal to the answer of the i-th query `queries[i]`.

 
**Example 1:**

**Input:** `N = 5, lamps = [[0,0],[4,4]], queries = [[1,1],[1,0]]`
**Output:** `[1,0]`
**Explanation:** 
Before performing the first query we have both lamps `[0,0]` and `[4,4]` on.
The grid representing which cells are lit looks like this, where `[0,0]` is the top left corner, and `[4,4]` is the bottom right corner:
```
1 1 1 1 1
1 1 0 0 1
1 0 1 0 1
1 0 0 1 1
1 1 1 1 1
```
Then the query at `[1, 1]` returns 1 because the cell is lit.  After this query, the lamp at `[0, 0]` turns off, and the grid now looks like this:
```
1 0 0 0 1
0 1 0 0 1
0 0 1 0 1
0 0 0 1 1
1 1 1 1 1
```
Before performing the second query we have only the lamp `[4, 4]` on.  Now the query at `[1, 0]` returns 0, because the cell is no longer lit.
 
**Note:**
1. `1 <= N <= 10^9`
2. `0 <= lamps.length <= 20000`
3. `0 <= queries.length <= 20000`
4. `lamps[i].length == queries[i].length == 2`

#### 解题思路
每个点对于横向(`x`)、纵向(`y`)、斜向(`x - y`)和反斜向(`x + y`)，都有各自对应的位置变量，一共4个
以这四种位置变量为基础，建立4个hash table。hash table的key是位置变量，value是对应位置变量上的亮灯个数 
每个点是否被照亮取决于这个点对应的四个位置变量在对应的hash table中是否存在（当`value == 0`时，我们会直接erase这对key-value）

**亮灯阶段:**
    更新四个hash table，同时用一个hash table (命名为`lamps_status`) 记录灯的坐标和状态
    
**query阶段:**
1. 对于每一个query，先以该query点的4个位置变量check这个点是不是会被照亮
2. 遍历该点的邻居和它自身。如果有灯并且灯亮着，需要update相应的4个hash map的信息以及`lamps_status`的信息

#### 示例代码 (cpp)
```cpp
class Solution {
    vector<vector<int>> dirs = {{-1,-1},{-1,0},{-1,1},
                                {0,-1},{0,0},{0,1},
                                {1,-1},{1,0},{1,1}};
public:
    vector<int> gridIllumination(int N, vector<vector<int>>& lamps, vector<vector<int>>& queries) {
        unordered_map<int,int> row_count; // row information, value is the number of lightening lamps in the same row
        unordered_map<int,int> col_count; // column information
        unordered_map<int,int> diag_count; // diag information
        unordered_map<int,int> anti_diag_count; // anti_diag information
        unordered_map<int, unordered_map<int,int>> lamps_status; //lamps information, key is the coordinate of the lamp, value is the status of lamp
        vector<int> res;
        for (const auto& lamp : lamps) {
            int x = lamp[0];
            int y = lamp[1];
            lamps_status[x][y] = 1;
            row_count[x]++;
            col_count[y]++;
            diag_count[x - y]++;
            anti_diag_count[x + y]++;
        }
        for (const auto& query : queries) {
            int x = query[0];
            int y = query[1];
            // check if this query point is light
            if (row_count.count(x) || col_count.count(y) || diag_count.count(x-y) || anti_diag_count.count(x + y)) {
                res.push_back(1);
            }
            else {
                res.push_back(0);
            }
            // turn off the light if necessary
            for (const auto& dir : dirs) {
                int xNew = x + dir[0];
                int yNew = y + dir[1];
                if (xNew >= 0 && xNew < N && yNew >= 0 && yNew < N && lamps_status.count(xNew) && lamps_status[xNew].count(yNew) && lamps_status[xNew][yNew]) {
                    // update the lamp status, turn it off
                    lamps_status[xNew][yNew] = 0;
                    if (row_count.count(xNew) && --row_count[xNew] == 0) {
                        row_count.erase(xNew);
                    }
                    if (col_count.count(yNew) && --col_count[yNew] == 0) {
                        col_count.erase(yNew);
                    }
                    if (diag_count.count(xNew - yNew) && --diag_count[xNew - yNew] == 0) {
                        diag_count.erase(xNew - yNew);
                    }
                    if (anti_diag_count.count(xNew + yNew) && --anti_diag_count[xNew + yNew] == 0) {
                        anti_diag_count.erase(xNew + yNew);
                    }
                }
            }
        }
        return res;
    }
};
```

#### 复杂度分析
如果我们有`k`个queries
时间复杂度: `O(N^2 + K)`
空间复杂度: `O(4N + N^2) = O(N^2)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/V0ebjgzDZdA)，欢迎关注！