---
title: '[Leetcode 1030] Matrix Cells in Distance Order'
categories:
  - leetcode
author: '大猩猩'
date: 2019-04-27 22:41:14
tags: ['Yahoo','Sort']
keywords: ['Yahoo','Sort']
description:
---

#### 原题说明
We are given a matrix with `R` rows and `C` columns has cells with integer coordinates `(r, c)`, where `0 <= r < R` and `0 <= c < C`.

Additionally, we are given a cell in that matrix with coordinates `(r0, c0)`.

Return the coordinates of all cells in the matrix, sorted by their distance from `(r0, c0)` from smallest distance to largest distance.  Here, the distance between two cells `(r1, c1)` and `(r2, c2)` is the Manhattan distance, `|r1 - r2| + |c1 - c2|`.  (You may return the answer in any order that satisfies this condition.)

**Example 1:**
{% blockquote %}
**Input:** `R = 1, C = 2, r0 = 0, c0 = 0`
**Output:** `[[0,0],[0,1]]`
**Explanation:** `The distances from (r0, c0) to other cells are: [0,1]`
{% endblockquote %}
**Example 2:**
{% blockquote %}
**Input:** `"R = 2, C = 2, r0 = 0, c0 = 1"`
**Output:** `[[0,1],[0,0],[1,1],[1,0]]`
**Explanation:** `The distances from (r0, c0) to other cells are: [0,1,1,2]
The answer [[0,1],[1,1],[0,0],[1,0]] would also be accepted as correct.`
{% endblockquote %}
**Example 3:**
{% blockquote %}
**Input:** `R = 2, C = 3, r0 = 1, c0 = 2`
**Output:** `[[1,2],[0,2],[1,1],[0,1],[1,0],[0,0]]`
**Explanation:**  `The distances from (r0, c0) to other cells are: [0,1,1,2,2,3]
There are other answers that would also be accepted as correct, such as [[1,2],[1,1],[0,2],[1,0],[0,1],[0,0]].` 
{% endblockquote %}

<!--more-->

#### 解题思路
按照Manhattan距离的定义，我们需要从小到大所搜所有的坐标，并按离给定点的距离，返回所有的坐标。
显然，最小的距离一定是１，而最大的距离不会超过R+C-1。我们那给定点为中心，从里向外依次搜索。这本质上与BFS是一个思想。这里不直接使用BFS的原因，是为了避免使用额外空间记录某个cell是否被visit过。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    vector<vector<int>> allCellsDistOrder(int R, int C, int r0, int c0) {
        vector<vector<int>> res = {{r0, c0}};
        for (auto level = 1; level < R + C - 1; ++level) {
            for (int x = -level; x <= level; ++x) {
                int r1 = r0 + x;
                int c1_a = c0 + level - abs(x);
                int c1_b = c0 + abs(x) - level;
                if (r1 >= 0 && r1 < R) {
                    if (c1_a >= 0 && c1_a < C){
                        res.push_back({r1, c1_a});
                    }
                    if (c1_a != c1_b && c1_b >= 0 && c1_b < C) {
                        res.push_back({r1, c1_b});    
                    }
                }
            }
        }
        return res;
    }
};
```
#### 示例代码 (java)
```java
class Solution {
    public int[][] allCellsDistOrder(int R, int C, int r0, int c0) {
        int[][] origin = new int[R * C][2];
        for (int i = 0; i < R; i++) {
            for (int j = 0; j < C; j++) {
                origin[i * C + j] = new int[] {i, j};
            }
        }

        Arrays.sort(origin, new Comparator<int[]>(){
            public int compare(int[] a, int[] b) {
                return Math.abs(a[0] - r0) + Math.abs(a[1] - c0)
                        - Math.abs(b[0] - r0) - Math.abs(b[1] - c0);
            }
        });
        return origin;
    }
}
```



#### 复杂度分析
时间复杂度: O(RC）
空间复杂度: O(1)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/mHOs-Uzq-Fk)，欢迎关注！