---
title: '[Leetcode 999] Available Captures for Rook'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-03-12 23:34:19
tags: ['Square', 'Array', 'Easy']
keywords: ['Square', 'Array', 'Easy']
description:
---
#### 原题说明
On an 8 x 8 chessboard, there is one white rook.  There also may be empty squares, white bishops, and black pawns.  These are given as characters 'R', '.', 'B', and 'p' respectively. Uppercase characters represent white pieces, and lowercase characters represent black pieces.

The rook moves as in the rules of Chess: it chooses one of four cardinal directions (north, east, west, and south), then moves in that direction until it chooses to stop, reaches the edge of the board, or captures an opposite colored pawn by moving to the same square it occupies.  Also, rooks cannot move into the same square as other friendly bishops.

Return the number of pawns the rook can capture in one move.

**Example 1:**
{% asset_img 999_example_1_improved.PNG 250 %}
{% blockquote %}
**Input:** 
`[[".",".",".",".",".",".",".","."],`
`[".",".",".","p",".",".",".","."],`
`[".",".",".","R",".",".",".","p"],`
`[".",".",".",".",".",".",".","."],`
`[".",".",".",".",".",".",".","."],`
`[".",".",".","p",".",".",".","."],`
`[".",".",".",".",".",".",".","."],`
`[".",".",".",".",".",".",".","."]]`
**Output:** `3`
**Explanation:** 
In this example the rook is able to capture all the pawns.
{% endblockquote %}
**Example 2:**
{% asset_img 999_example_2_improved.PNG 250 %}
{% blockquote %}
**Input:** 
`[[".",".",".",".",".",".",".","."],`
`[".","p","p","p","p","p",".","."],`
`[".","p","p","B","p","p",".","."],`
`[".","p","B","R","B","p",".","."],`
`[".","p","p","B","p","p",".","."],`
`[".","p","p","p","p","p",".","."],`
`[".",".",".",".",".",".",".","."],`
`[".",".",".",".",".",".",".","."]]`
**Output:** `0`
**Explanation:** 
Bishops are blocking the rook to capture any pawn.
{% endblockquote %}
**Example 3:**
{% asset_img 999_example_3_improved.PNG 250 %}
{% blockquote %}
**Input:** 
`[[".",".",".",".",".",".",".","."],`
`[".",".",".","p",".",".",".","."],`
`[".",".",".","p",".",".",".","."],`
`["p","p",".","R",".","p","B","."],`
`[".",".",".",".",".",".",".","."],`
`[".",".",".","B",".",".",".","."],`
`[".",".",".","p",".",".",".","."],`
`[".",".",".",".",".",".",".","."]]`
**Output:** `3`
**Explanation:** 
The rook can capture the pawns at positions `b5`, `d6` and `f5`.
{% endblockquote %}
**Note:**
1. `board.length == board[i].length == 8`
2. `board[i][j]` is either `'R'`, `'.'`, `'B'`, or `'p'`
3. There is exactly one cell with `board[i][j] == 'R'`

#### 解题思路
题目问从`'R'`点开始上下左右直走，碰到`'B'`，`'p'`，或者边界则停止，可能遇到多少个`'p'`.
我们用`count_p`记录可能遇到的`p`的数量，遍历整个`board`。
当遇到`'R'`时，我们尝试从`'R'`的位置开始，向四个方向移动：
1) 当遇到边界，则停止当前方向探索
2) 当遇到`'B'`时，则停止当前方向探索
3) 当遇到`'p'`时，`count_p++`并停止当前方向探索
4) 当四个方向均探索完毕，则可以直接返回`count_p`
如果遍历`board`结束仍没有返回，则说明不存在`'R'`，可返回`0`

#### 示例代码 (cpp)
```cpp
class Solution {
    // move one step towards four directions
    const vector<vector<int>> dirs = {{-1, 0}, {0, 1}, {0, -1}, {1, 0}};
    const int kBoardSize = 8;
public:
    int numRookCaptures(vector<vector<char>>& board) {
        int count_p = 0;
        for (int i = 0; i < kBoardSize; ++i) {
            for (int j = 0; j < kBoardSize; ++j) {
                if (board[i][j] == 'R') {
                    // Once we find 'R', move towards each of the four directions.
                    for (int k = 0; k < dirs.size(); ++k) {
                        int cur_x = i, cur_y = j;
                        // When not reaching boundary
                        while (cur_x >= 0 && cur_x < kBoardSize && cur_y >= 0 && cur_y < kBoardSize) {
                            if (board[cur_x][cur_y] == 'B') {
                                break;
                            } else if (board[cur_x][cur_y] == 'p') {
                                ++count_p;
                                break;
                            }
                            cur_x += dirs[k][0];
                            cur_y += dirs[k][1];
                        }
                    }
                    // Since we assume at most one 'R' existed on the board
                    return count_p;
                }
            }
        }
        // We could not find 'R' on the board
        return 0;
    }
};
```

#### 复杂度分析
时间复杂度: `O(mn + (m + n)) => O(mn)`
空间复杂度: `O(1)`

#### 归纳总结
这道题并不是很难，但是理解题目需要些时间，面试的时候可能会用来作为warm up，关键是和面试官多交流，理解题目的意思，不要着急盲目开始做。
我们在**Youtube**上更新了[视频讲解](https://youtu.be/UspBaHqxjfE)，欢迎关注！