---
title: '[Leetcode 832] Flipping an Image'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-06-03 00:49:43
tags: [Google, Array]
keywords: [Flipping an Image, Google, Array]
description:
---
#### 原题说明
Given a binary matrix A, we want to flip the image horizontally, then invert it, and return the resulting image.

To flip an image horizontally means that each row of the image is reversed.  For example, flipping `[1, 1, 0]` horizontally results in `[0, 1, 1]`.

To invert an image means that each 0 is replaced by 1, and each 1 is replaced by 0. For example, inverting `[0, 1, 1]` results in `[1, 0, 0]`.

Example 1:
{% blockquote %}
Input: `[[1,1,0],[1,0,1],[0,0,0]]`
Output: `[[1,0,0],[0,1,0],[1,1,1]]`
Explanation: First reverse each row: `[[0,1,1],[1,0,1],[0,0,0]]`.
Then, invert the image: `[[1,0,0],[0,1,0],[1,1,1]]`
{% endblockquote %}
Example 2:
{% blockquote %}
Input: `[[1,1,0,0],[1,0,0,1],[0,1,1,1],[1,0,1,0]]`
Output: `[[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]`
Explanation: First reverse each row: `[[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]]`.
Then invert the image: `[[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]`
{% endblockquote %}
Notes:

- `1 <= A.length = A[0].length <= 20`
- `0 <= A[i][j] <= 1`


#### 解题思路
这道题并不难, 属于谷歌面试中的热身题或者是Intern电话面试的难度. 关键是要在短时间内形成清晰的思路, 并且形成代码, 为之后的题或者followup争取到足够的时间.
这里介绍的思路是逐行进行`swap`, 然后每个元素异或, 虽然这样每个元素会扫面两遍, 但是思路足够清晰.

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    vector<vector<int>> flipAndInvertImage(vector<vector<int>>& A) {
        for (auto &row : A) {
            for (int i = 0; i < row.size() / 2; ++i) {
                swap(row[i], row[row.size() - 1 - i]);
            }
            for (auto &ele : row) {
                ele ^= 1;
            }
        }
        return A;
    }
};
```

#### 复杂度分析
时间复杂度: `O(n^2)` (n为A的边长)
空间复杂度: `O(1)`

#### 归纳总结
需要训练在白板上10分钟之内搞定.