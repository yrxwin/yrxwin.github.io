---
title: '[Leetcode 1029] Two City Scheduling'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-04-28 18:22:02
tags: ['Bloomberg', 'Greedy']
keywords: ['Bloomberg', 'Greedy']
description:
---
#### 原题说明
There are `2N` people a company is planning to interview. The cost of flying the i-th person to city A is `costs[i][0]`, and the cost of flying the i-th person to city B is `costs[i][1]`.

Return the minimum cost to fly every person to a city such that exactly N people arrive in each city.

**Example 1:**
{% blockquote %}
**Input:** `[[10,20],[30,200],[400,50],[30,20]]`
**Output:** `110`
**Explanation:** 
The first person goes to city A for a cost of `10`.
The second person goes to city A for a cost of `30`.
The third person goes to city B for a cost of `50`.
The fourth person goes to city B for a cost of `20`.

The total minimum cost is `10 + 30 + 50 + 20 = 110` to have half the people interviewing in each city.
{% endblockquote %}
 

**Note:**
1. `1 <= costs.length <= 100`
2. It is guaranteed that costs.length is even.
3. `1 <= costs[i][0], costs[i][1] <= 1000`
<!--more-->

#### 解题思路
我们排序每一个面试者到A地和到B地`cost`之差，前`N`个（到A地`cost`较小的`N`个）取到A地cost，后`N`个取到B地cost，这样平均情况时间复杂度是`NlogN`
考虑到我们只需要到A地较小的元素在前半部分（较小元素之间的排序无关紧要），而到B地`cost`较小的元素在后半部分，所以可以考虑使用快速选择算法替代快速排序，将平均复杂度从`NlogN`减小到`N`

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int twoCitySchedCost(vector<vector<int>>& costs) {
        // sort(costs.begin(), costs.end(), [](const vector<int>& c1, const vector<int>& c2) {
        //     return (c1[0] - c1[1]) < (c2[0] - c2[1]);
        //  });
        nth_element(costs.begin(), costs.begin() + costs.size() / 2 - 1, costs.end(), [](const vector<int>& c1, const vector<int>& c2) {
            return (c1[0] - c1[1]) < (c2[0] - c2[1]);
        });
        int res_cost = 0;
        for (int i = 0, j = costs.size() - 1; i < j; ++i, --j) {
            res_cost += costs[i][0] + costs[j][1];
        }
        return res_cost;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int twoCitySchedCost(int[][] costs) {
        Arrays.sort(costs, new Comparator<int[]>() {
            public int compare(int[] a, int[] b) {
                return (a[1] - a[0]) - (b[1] - b[0]);
            }
        });
        int cost = 0;
        for (int i = 0; i < costs.length / 2; i++) {
            cost += costs[i][1] + costs[costs.length-i-1][0];
        }
        return cost;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def twoCitySchedCost(self, costs: List[List[int]]) -> int:
        costs.sort(key = lambda x: x[0]-x[1])
        return sum(i[0] for i in costs[:len(costs)//2]) + sum(j[1] for j in costs[len(costs)//2:])
```

#### 复杂度分析
时间复杂度: `O(N)` for cpp, `O(Nlog(N))` for java and python
空间复杂度: `O(1)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/vTtOqONCWbs)，欢迎关注！