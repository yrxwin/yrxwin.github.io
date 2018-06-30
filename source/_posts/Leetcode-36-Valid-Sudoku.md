---
title: Leetcode-36-Valid-Sudoku
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-06-30 12:47:02
tags:
keywords:
description:
---

#### 原题说明
Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits 1-9 without repetition.
2. Each column must contain the digits 1-9 without repetition.
3. Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.

The Sudoku board could be partially filled, where empty cells are filled with the character `'.'`.

{% asset_img lc36.png 400 "" %}

**Example 1:**
{% blockquote %}

**Input:**
[
  	["5" , "3" , " . " , " . " , "7" , " . " , " . " , " . " , " . "],
  	["6" , " . " , " . " , "1" , "9" , "5" , " . " , " . " , " . "],
  	[" . " , "9" , "8" , " . " , " . " , " . " , " . " , "6" , " . "],
  	["8" , " . " , " . " , " . " , "6" , " . " , " . " , " . " , "3"],
  	["4" , " . " , " . " , "8" , " . " , "3" , " . " , " . " , "1"],
  	["7" , " . " , " . " , " . " , "2" , " . " , " . " , " . " , "6"],
  	[" . " , "6" , " . " , " . " , " . " , " . " , "2" , "8" , " . "],
  	[" . " , " . " , " . "  , "4" , "1" , "9" , " . " , " . " , "5"],
  	[" . " , " . " , " . " , " . " , "8" , " . " , " . " , "7" , "9"]
]
**Output:** true
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:**
[
  	["8" , "3" , " . " , " . " , "7" , " . " , " . " , " . " , " . "],
  	["6" , " . " , " . " , "1" , "9" , "5" , " . " , " . " , " . "],
  	[" . " , "9" , "8" , " . " , " . " , " . " , " . " , "6" , " . "],
  	["8" , " . " , " . " , " . " , "6" , " . " , " . " , " . " , "3"],
  	["4" , " . " , " . " , "8" , " . " , "3" , " . " , " . " , "1"],
  	["7" , "6" , " . " , " . " , " . " , " . " , "2" , "8" , " . "],
  	[" . " , " . " , " . " , "4" , "1" , "9" , " . " , " . " , "5"],
  	[" . " , " . " , " . " , " . " , "8" , " . " , " . " , "7" , "9"]
]
**Output:** false
**Explanation:** Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
{% endblockquote %}

**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.
- The given board contain only digits 1-9 and the character '.'.
- The given board size is always 9x9.

#### 解题思路
本题要求确定一个 9 x 9 的数独是否valid。题目说明并不要求数独是可解的，因此难度不是很高。

根据数独的规则，需要对每一行，每一列，以及规定的 9 个 3 x 3 的矩阵做检查。因为每次检查需要对9个数进行查重，我们另外写一个函数 `isValidSec` ，用一个map记录下遍历过的值，遇到有相同的数字是返回`false`, 否则最终返回`true`。
然后分别按行、列、矩阵块遍历即可。 

具体代码如下：

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        vector<char> nineNum;
        // 检查行
        for (int i = 0; i < board.size(); i++) {
            if (!isValidSec(board[i])) {
                return false;
            }
        }
        // 检查列
        for (int i = 0; i < board[0].size(); i++) {
            nineNum.clear();
            for (int j = 0; j < board.size(); j++) {
                nineNum.push_back(board[j][i]);
            }
            if (!isValidSec(nineNum)) {
                return false;
            }
        }
        // 检查矩阵块
        for (int i = 0; i < board.size(); i = i + 3) {
            for (int j = 0; j < board[0].size(); j = j + 3) {
                nineNum.clear();
                for (int l = i; l < i+3; l++){
                    for (int m = j; m < j+3; m++){
                        nineNum.push_back(board[l][m]);
                    }
                }
                if (!isValidSec(nineNum)) {
                    return false;
                }
            }
        }
        return true;
    }
    bool isValidSec(vector<char>& nineNum) {
        unordered_map<char, int> table;
        for(int i = 0 ; i < nineNum.size(); i++) {
            if (nineNum[i] != '.' && table.count(nineNum[i]) > 0) {
                return false;
            }
            else {
                table[nineNum[i]] = 1;
            }
        }
        return true;
    }
};
```
#### 复杂度分析
我们遍历了3遍整个数独，因此时间复杂度为`O(n)`, 同时空间复杂度为`O(n^0.5)`.

 - 时间复杂度: `O(n)`
 - 空间复杂度: `O(n^0.5)`

#### 归纳总结
这题的难度不高，按照数独的规则一次做检查即可。代码虽然显得较长，但可读性会显得比较好。之后我们会再介绍这题的进阶版，[[LeetCode 37] Sudoku Solver](/Leetcode-37-Sudoku-Solver)。