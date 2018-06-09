---
title: '[Leetcode 812] Largest Triangle Area'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-06-04 16:20:55
tags: [Google, Math]
keywords: [Google, Math]
description:
---
#### 原题说明
You have a list of points in the plane. Return the area of the largest triangle that can be formed by any 3 of the points.

{% asset_img sample.png 350 %}
{% blockquote %}
**Example**:
**Input**: points = `[[0,0],[0,1],[1,0],[0,2],[2,0]]`
**Output**: 2
**Explanation**: 
The five points are show in the figure below. The red triangle is the largest.
{% endblockquote %}

**Notes**:
- `3 <= points.length <= 50`.
- No points will be duplicated.
- `-50 <= points[i][j] <= 50`.
- Answers within 10^-6 of the true value will be accepted as correct.

#### 解题思路
这道题主要考察解析几何中三角形面积的计算(如[叉乘计算面积](http://www.maths.usyd.edu.au/u/MOW/vectors/vectors-11/v-11-7.html), [行列式计算面积
](https://people.richland.edu/james/lecture/m116/matrices/applications.html)), 也比较适合Google电话面试或者Intern面试的难度, 可能会用来考察简历有相关背景的面试者.
做法上比较暴力, 直接三重循环找到所有可能组成三角形的点计算最大面积即可, 还是要求快速形成思路, 代码清晰, 建议把叉乘部分单独写成一个Function, 这样做即使面试时叉乘公式不记得了, 但是整体思路清晰, 也可能会过面试. 

#### 示例代码 (cpp)
```cpp
class Solution {
    double multiply(vector<int> v1, vector<int> v2) {
        return 0.5 * abs(v1[0] * v2[1] - v2[0] * v1[1]);
    }
public:
    double largestTriangleArea(vector<vector<int>>& points) {
        int n = points.size();
        double ret = 0;
        for (int i = 0; i < n; ++i) {
            for (int j = i + 1; j < n; ++j) {
                for (int k = j + 1; k < n; ++k) {
                    ret = max(ret, multiply({points[k][0] - points[i][0], points[k][1] - points[i][1]}, {points[k][0] - points[j][0], points[k][1] - points[j][1]}));
                }
            }
        }
        return ret;
    }
};
```

#### 示例代码 (python)
```python
class Solution(object):
    def calArea(self, p1, p2, p3):
        #Use Determinant to get triangle area
        return .5 * abs(p1[0] * p2[1] + p2[0] * p3[1] + p3[0] * p1[1] - p1[0] * p3[1] - p2[0] * p1[1] - p3[0] * p2[1])
    
    def largestTriangleArea(self, points):
        """
        :type points: List[List[int]]
        :rtype: float
        """
        maxS = 0
        for i in range(len(points) - 2):
            for j in range(i + 1, len(points) - 1):
                for k in range(j + 1, len(points)):
                    S = self.calArea(points[i], points[j], points[k])
                    if S > maxS:
                        maxS = S
        return maxS
```

#### 复杂度分析
时间复杂度: `O(N^3)`
空间复杂度: `O(1)`

#### 归纳总结
谷歌有时候会考察矩阵叉乘, 点乘相关的知识点, 面试的时候即使不记得也可以问面试官要提示, 当然如果自己能够记得肯定是加分的. 之后会整理相关的考题.
