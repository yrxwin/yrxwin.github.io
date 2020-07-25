---
title: '[Leetcode 1072] Flip Columns For Maximum Number of Equal Rows'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-07-25 13:30:20
tags: ['Hash Table']
keywords:
description:
---
#### 原题说明
Given a matrix consisting of 0s and 1s, we may choose any number of columns in the matrix and flip every cell in that column.  Flipping a cell changes the value of that cell from 0 to 1 or from 1 to 0.

Return the maximum number of rows that have all values equal after some number of flips.

 

Example 1:

Input: [[0,1],[1,1]]
Output: 1
Explanation: After flipping no values, 1 row has all values equal.
Example 2:

Input: [[0,1],[1,0]]
Output: 2
Explanation: After flipping values in the first column, both rows have equal values.
Example 3:

Input: [[0,0,0],[0,0,1],[1,1,0]]
Output: 2
Explanation: After flipping values in the first two columns, the last two rows have equal values.
 

Note:

1 <= matrix.length <= 300
1 <= matrix[i].length <= 300
All matrix[i].length's are equal
matrix[i][j] is 0 or 1
<!--more-->

#### 解题思路
若是需要暴力枚举解题，我们首先思考这个问题，要如何确定翻转哪些列？因为我们翻转的目的，是保证其中一行全是 `0`（或者 `1`）。所以我们可以考虑枚举每一行，使得这一行全部变成 0 （或者 1），然后统计其他行是否有所有值都相等的。

进一步考虑发现，我们没有必要对固定的那一行真正进行翻转。当某两行的值完全相等或 完全相反时，通过翻转列，我们总能把它们同时变为符合条件的行。

我们可以用每一行中每个元素相对第一个元素是否相同来组成一个特征字符串，用于代表这一行的特性。也就是说特征字符串相同的行，一定会同时变成满足条件的行(全是`0`或者`1`)。反之，若是不相同，一定不能同时变成满足条件的字符串。

举例说：对行 `100`，它的特征字符串都是`011`。对行`011`，它的特征字符串也是`011`。因此它们一定能同时变成满足题目要求的行。事实上，我们只要翻转第一列就可以了。

最后，我们用一个哈希表统计每个特征字符串的频率，频率最高的就是我们要的答案。


#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int maxEqualRowsAfterFlips(vector<vector<int>>& matrix) {
        unordered_map<string, int> mapping;
        for (auto& row : matrix) {
            string ele = "";
            for (auto& val : row) {
                ele += val == row[0] ? '0' : '1';
            }
            mapping[ele]++;
        }
        int ans = 0;
        for (auto& [key, val] : mapping) {
            ans = max(ans, val);
        }
        return ans;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int maxEqualRowsAfterFlips(int[][] matrix) {
        int ans = 0;
        int m = matrix.length, n = matrix[0].length;
        for(int i = 0; i < m; i++) {
            int cnt = 0;
            int[] flip = new int[n];
            for(int j = 0; j < n; j++) flip[j] = 1 - matrix[i][j];
            for(int k = i; k < m; k++) {
                if(Arrays.equals(matrix[k], matrix[i]) || Arrays.equals(matrix[k], flip)) cnt++;
            }
            ans = Math.max(ans, cnt);
        }
        return ans;
    }
}
```

#### 示例代码 (python)
```python
class Solution(object):
    def maxEqualRowsAfterFlips(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: int
        """
        cache = collections.defaultdict(int)
        for row in matrix:
            vals = []
            trans = []
            for c in row:
                vals.append(c)
                trans.append(1 - c)
            cache[str(vals)] += 1
            cache[str(trans)] += 1
        return max(cache.values())     
```

#### 复杂度分析
`m`是`matrix`的行数，`n`是`matrix`的列数
时间复杂度: O(mn)
空间复杂度: O(m)

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/C-mof8PvRzw)，欢迎关注！