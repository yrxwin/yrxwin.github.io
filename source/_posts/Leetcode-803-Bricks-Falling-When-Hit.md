---
title: '[Leetcode 803] Bricks Falling When Hit'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-06-05 16:15:34
tags: [Google, Union Find]
keywords: [Google, Union Find, Bricks Falling When Hit]
description:
---
#### 原题说明
We have a grid of 1s and 0s; the 1s in a cell represent bricks.  A brick will not drop if and only if it is directly connected to the top of the grid, or at least one of its (4-way) adjacent bricks will not drop.

We will do some erasures sequentially. Each time we want to do the erasure at the location (i, j), the brick (if it exists) on that location will disappear, and then some other bricks may drop because of that erasure.

Return an array representing the number of bricks that will drop after each erasure in sequence.

{% blockquote %}
**Example 1**:
**Input**: 
grid = `[[1,0,0,0],[1,1,1,0]]`
hits = `[[1,0]]`
**Output**: `[2]`
**Explanation**: 
If we erase the brick at (1, 0), the brick at (1, 1) and (1, 2) will drop. So we should return 2.
{% endblockquote %}
{% blockquote %}
**Example 2**:
**Input**: 
grid = `[[1,0,0,0],[1,1,0,0]]`
hits = `[[1,1],[1,0]]`
**Output**: `[0,0]`
**Explanation**: 
When we erase the brick at (1, 0), the brick at (1, 1) has already disappeared due to the last move. So each erasure will cause no bricks dropping.  Note that the erased brick (1, 0) will not be counted as a dropped brick.
{% endblockquote %}

**Note**:
- The number of rows and columns in the grid will be in the range `[1, 200]`.
- The number of erasures will not exceed the area of the grid.
- It is guaranteed that each erasure will be different from any other erasure, and located inside the grid.
- An erasure may refer to a location with no brick - if it does, no bricks drop.

#### 解题思路
这道题tag里有`union find`的方法, 解题思路可以参考官方解答.

实际上, 用`DFS`一样可以给出清晰的解答. 在面试过程中, 除非利用`union find`可以明显简化问题, 否则不是很推荐使用. 曾经有人使用`union find`解答`number of islands I`, 就被面试官追问, `union find`如何删除一个节点, 如果不熟悉的话就会很被动.

这里我们提供两种`DFS`的思路。

方法1(c++): 每次落下一个砖块, 要从砖块的上下左右四个方向分别做`DFS`, 第一遍判断`DFS`经过的砖块是否与顶部砖块连通, 如果不连通, 则该砖块会落下, 并且所有与之相连的砖块都不与顶部砖块连通, 因此做第二遍`DFS`, 标记访问过的砖块为落下. 注意每一次`DFS`都是一次新的遍历, 因此我们使用`_id`的来标记第`_id`次`DFS`, 并且在新的一次遍历前更新`id`.

方法2(python): 将所有击落的砖块，先行去除(在`Grid`矩阵中-1)，接着用`DFS`找出所有与顶部砖块连通的砖块，并用一个矩阵`connected`记录(既表示已经访问过，又表示与顶部连通)。然后，从最后一块被击落的砖块向前逐一恢复。每次恢复被击落砖块时，在`Grid`中+1，并且判断该位置是否原来有砖块存在，是否处于顶部或者四周有没有与顶部连通的砖块存在。若满足这些条件，说明该被击落的砖块可以恢复，并且以它为起点做`DFS`，所有与他连通的砖块都可以被恢复，恢复的数量即为该次击落后，落下砖块的数量。

#### 示例代码 (cpp)
```cpp
class Solution {
    vector<vector<int>> _g; // 用一个私有变量 _g 可以减少 fall 函数的参数数量
    int _m, _n;
    int _id = 1;
    vector<int> dx = {-1, 0, 0, 1};
    vector<int> dy = {0, -1, 1, 0};
    bool fall(int x, int y, bool isClear, int& cnt) {
        if (x < 0 || x >= _m || y < 0 || y >= _n) {
            return true;
        }
        if (_g[x][y] == _id || _g[x][y] == 0) {
            return true;
        }
        if (x == 0) {
            return false;
        }
        _g[x][y] = isClear ? 0 : _id;
        ++cnt;
        for (int i = 0; i < 4; ++i) {
            int xx = x + dx[i], yy = y + dy[i];
            if (!fall(xx, yy, isClear, cnt)) {
                return false;
            }
        }
        return true;
    }
public:
    vector<int> hitBricks(vector<vector<int>>& grid, vector<vector<int>>& hits) {
        _m = grid.size();
        _n = grid[0].size();
        _g.swap(grid);
        vector<int> rets;
        for (auto& hit : hits) {
            int ret = 0;
            int x = hit[0], y = hit[1];
            _g[x][y] = 0;
            for (int i = 0; i < 4; ++i) {
                ++_id;
                int xx = x + dx[i];
                int yy = y + dy[i];
                int cnt = 0;
                if (!fall(xx, yy, false, cnt)) {
                    continue;
                }
                ++_id;
                ret += cnt;
                fall(xx, yy, true, cnt);
            }
            rets.push_back(ret);
        }
        return rets;
    }    
};
```
#### 示例代码 (python)
```python
class Solution(object):
    def check_valid(self, r, c, grid):
        if r < 0 or r >= len(grid) or c < 0  or c >= len(grid[0]) or grid[r][c] < 1:
            return False
        else:
            return True
        
    def dfs_connect(self, grid, connected, r, c):
        num_connected = 1
        for rr, cc in [(r - 1, c), (r + 1, c), (r, c - 1), (r, c + 1)]:
            if self.check_valid(rr, cc, grid) and not connected[rr][cc]:
                connected[rr][cc] = 1
                num_connected += self.dfs_connect(grid, connected, rr, cc)
        return num_connected
    
    def build_connection(self, grid):
        connected = [[0 for c in range(len(grid[0]))] for r in range(len(grid))]
        for c in range(len(grid[0])):
            if self.check_valid(0, c, grid):
                connected[0][c] = 1
                self.dfs_connect(grid, connected, 0, c)
        return connected
    
    def check_new_block_connection(self, r, c, grid, connected):
        if grid[r][c] < 1:
            return False
        if r == 0:
            return True
        for rr, cc in [(r - 1, c), (r + 1, c), (r, c - 1), (r, c + 1)]:
            if self.check_valid(rr, cc, grid) and connected[rr][cc] == 1:
                return True
        return False
    
    def hitBricks(self, grid, hits):
        """
        :type grid: List[List[int]]
        :type hits: List[List[int]]
        :rtype: List[int]
        """
        ret = [0 for i in range(len(hits))]
        for hit in hits:
            grid[hit[0]][hit[1]] -= 1
        connected = self.build_connection(grid)
        for idx in range(len(hits)):
            r, c = hits[-1 - idx]
            grid[r][c] += 1
            if self.check_new_block_connection(r, c, grid, connected):
                connected[r][c] = 1
                add_num = self.dfs_connect(grid, connected, r, c) - 1
                ret[-1 - idx] = add_num
                
        return ret
```

#### 复杂度分析
方法1：
时间复杂度: `O(N * Q)` 其中`N`是砖块数量, `Q`是`hits`的长度
空间复杂度: `O(1)`

方法2：
时间复杂度: `O(N + Q)` 其中`N`是砖块数量, `Q`是`hits`的长度
空间复杂度: `O(N)`

#### 归纳总结
这是一道比较复杂的深度遍历问题, 如果同学一下子不会做也没有关系, 面试的时候不要紧张, 要和面试官讨论并且慢慢理清思路.
