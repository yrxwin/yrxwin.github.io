---
title: '[Leetcode 1034] Coloring A Border'
categories:
  - leetcode
author: '大猩猩'
date: 2019-05-01 21:40:47
tags: ['Depth-first Search']
keywords: ['Depth-first Search']
description:
---
#### 原题说明
Given a 2-dimensional `grid` of integers, each value in the grid represents the color of the grid square at that location.

Two squares belong to the same connected component if and only if they have the same color and are next to each other in any of the 4 directions.

The *border* of a connected component is all the squares in the connected component that are either 4-directionally adjacent to a square not in the component, or on the boundary of the grid (the first or last row or column).

Given a square at location `(r0, c0)` in the grid and a `color`, color the border of the connected component of that square with the given `color`, and return the final `grid`.
<!--more-->

#### 解题思路
题目给我们一个坐标，要求将这个坐标表示的点所属的`component`的边界用给定的颜色标记出来。

我们用`DFS`的方法解决这道题。从给定的起点`A`开始，我们可以方便的遍历`A`所在的`component`的所有点。为了不开辟额空间，我们直接将`A`原来的颜色`origincolor`翻转为`-origincolor`。

那如何在找出边界呢？我们只需要在完成一个点上下左右四个方向的遍历之后，检查这个点是不是在`component`内部，在的话我们再次翻转`-origincolor`,把它复原为`origincolor`。经过这样的步骤之后，地图上所有标记为`-origincolor`的点就是我们需要的边界了。我们将这些点重新标记为题目要求的`color`即可。

同学们可以看下图给出的例子有个具体认识（图片引自*Discuss*中*votrubac*的发帖）。

{% asset_img lc1034.png 800 "" %}
#### 示例代码 (cpp)
```cpp
class Solution {
private:
    vector<vector<int>> dirs = {{1,0},{0,1},{-1,0},{0,-1}};
public:
    vector<vector<int>> colorBorder(vector<vector<int>>& grid, int r0, int c0, int color) {
        vector<vector<bool>> visit(grid.size(),vector<bool>(grid[0].size(),false));
        dfs(grid, r0, c0, grid[r0][c0]);
        for (int i = 0; i < grid.size(); ++i) {
            for (int j = 0; j < grid[0].size(); ++j) {
                if (grid[i][j] < 0) {
                    grid[i][j] = color;
                }
            }
        }
        return grid;
    }
    void dfs(vector<vector<int>>& grid, int r, int c, int originColor) {
        grid[r][c] = -originColor;
        for (auto dir : dirs) {
            int rNew = r + dir[0];
            int cNew = c + dir[1];
            if (rNew >= 0 && rNew < grid.size() && cNew >= 0 && cNew < grid[0].size()) {
                if (grid[rNew][cNew] == originColor) {
                    dfs(grid, rNew, cNew, originColor);
                }
            }
        }
        if (r > 0 && r < grid.size() - 1 && c > 0 && c < grid[0].size() - 1) {
            if (abs(grid[r - 1][c]) == originColor &&
                abs(grid[r + 1][c]) == originColor &&
                abs(grid[r][c + 1]) == originColor &&
                abs(grid[r][c - 1]) == originColor) {
                grid[r][c] = originColor;
            }
        }
        return;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    private int[] d = { 0, 1, 0, -1, 0 }; // neighbors' relative displacements.
    public int[][] colorBorder(int[][] grid, int r0, int c0, int color) {
        dfs(grid, r0, c0, grid[r0][c0]);
        for (int[] g : grid) {
            for (int i = 0; i < g.length; ++i) {
                if (g[i] < 0) { g[i] = color; }
            }
        }
        return grid;
    }
    private void dfs(int[][] grid, int r, int c, int clr) {
        grid[r][c] = -clr; // mark as visited.
        int cnt = 0; // use to count grid[r][c]'s component neighbors (same color as itself).
        for (int i = 0; i < 4; ++i) { // traverse 4 neighbors.
            int x = r + d[i], y = c + d[i + 1]; // nieghbor's coordinates.
            if (x < 0 || x >= grid.length || y < 0 || y >= grid[0].length || Math.abs(grid[x][y]) != clr) { continue; } // out of grid or not same component.
            ++cnt; // only if all 4 neighbors of grid[r][c] have same color as itself, it is on inner part.
            if (grid[x][y] == clr) { dfs(grid, x, y, clr); }
        }
        if (cnt == 4) { grid[r][c] = clr; } // inner part, change back.
    }
}
```

#### 示例代码 (python)
```python
# python代码提供一种使用额外空间记录遍历点的方法
class Solution(object):
    def colorBorder(self, grid, r0, c0, color):
        """
        :type grid: List[List[int]]
        :type r0: int
        :type c0: int
        :type color: int
        :rtype: List[List[int]]
        """
        m, n = len(grid), len(grid[0])
        border, seen = set(), set()

        def dfs(x, y):
            if not (0 <= x < m and 0 <= y < n and grid[x][y] == grid[r0][c0]): 
                return False
            if (x, y) in seen: 
                return True
            seen.add((x, y))
            if dfs(x + 1, y) + dfs(x - 1, y) + dfs(x, y + 1) + dfs(x, y - 1) < 4: 
                border.add((x, y))
            return True
        dfs(r0, c0)
        for x, y in border: grid[x][y] = color
        return grid
```

#### 复杂度分析
时间复杂度: O(N\*M)
空间复杂度: O(1)
`N`, `M`分别是`grid`的长和宽。
#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/GSc-F_jlYWk)，欢迎关注！