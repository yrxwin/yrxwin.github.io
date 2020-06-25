---
title: '[Leetcode 1042] Flower Planting With No Adjacent'
categories:
  - leetcode
author: '大猩猩'
date: 2020-05-23 22:00:27
tags: ['Graph','LinkedIn']
keywords:
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">You have&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">N</code>&nbsp;gardens, labelled&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1</code>&nbsp;to&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">N</code>.&nbsp; In each garden, you want to plant one of 4 types of flowers.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">paths[i] = [x, y]</code>&nbsp;describes the existence of a bidirectional path from garden&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">x</code>&nbsp;to garden&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">y</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Also, there is no garden that has more than 3 paths coming into or leaving it.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Your task is to choose a flower type for each garden such that,&nbsp;for any two gardens connected by a path, they have different types of flowers.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Return&nbsp;<span style="font-weight: bolder;">any</span>&nbsp;such a choice as an array&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">answer</code>, where&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">answer[i]</code>&nbsp;is the type of flower&nbsp;planted in the&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">(i+1)</code>-th garden.&nbsp; The flower types are denoted&nbsp;<font face="monospace">1</font>,&nbsp;<font face="monospace">2</font>,&nbsp;<font face="monospace">3</font>, or&nbsp;<font face="monospace">4</font>.&nbsp; It is guaranteed an answer exists.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><div style="color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>N = <span id="example-input-1-1">3</span>, paths = <span id="example-input-1-2">[[1,2],[2,3],[3,1]]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">[1,2,3]</span>
</pre><div><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>N = <span id="example-input-2-1">4</span>, paths = <span id="example-input-2-2">[[1,2],[3,4]]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">[1,2,1,2]</span>
</pre><div><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example 3:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>N = <span id="example-input-3-1">4</span>, paths = <span id="example-input-3-2">[[1,2],[2,3],[3,4],[4,1],[1,3],[2,4]]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-3">[1,2,3,4]</span>
</pre><p style="font-size: inherit; margin-bottom: 1em;">&nbsp;</p><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Note:</span></p><ul style="margin-bottom: 1em;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= N &lt;= 10000</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0 &lt;= paths.size &lt;= 20000</code></li><li>No garden has 4 or more paths coming into or leaving it.</li><li>It is guaranteed an answer exists.</li></ul></div></div></div>
<!--more-->

#### 解题思路
这道题相当与给我们`N`个点，每个点最多与图中另外三个点相连，要求我们用`4`种颜色给图染色，同时任意一条边上的`2`个点不能是相同的颜色。

因为题目保证了一定存在解，所以我们只要搜索出一种染色方法就可以了。对于一个图，它一定是由若干个最大连通子图组成的。任意两个不同的连通图，它们之间的染色互相不影响。而我们对每个连通图，分别做一次`dfs`就可以把这个连通图中所有的点做一次满足要求的染色，并把结果保存到我们返回的染色数组中即可。

#### 示例代码 (cpp)
`Java`和`Python`代码与`C++`略有不同，但主题思想是一致的。
```cpp
class Solution {
public:
    vector<int> gardenNoAdj(int N, vector<vector<int>>& paths) {
        vector<int> ans(N, 0);
        unordered_map<int, unordered_set<int>> edges;
        for (auto path : paths) {
            edges[path[0] - 1].insert(path[1] - 1);
            edges[path[1] - 1].insert(path[0] - 1);
        }
        for (auto i = 0; i < N; ++i) {
            if (edges.count(i) == 0) {
                ans[i] = 1;
            }
            else if (ans[i] == 0) {
                color(ans, edges, i);
            }
        }
        return ans;
    }
    void color(vector<int>& ans, unordered_map<int, unordered_set<int>>& edges, int i) {
        for (int c = 1; c <= 4; ++c) {
            bool canColor = true;
            for (auto next : edges[i]) {
                if (ans[next] == c) {
                    canColor = false;
                    break;
                }
            }
            if (canColor) {
                ans[i] = c;
                break;
            }
        }
        for (auto next : edges[i]) {
            if (ans[next] == 0) {
                color(ans, edges, next);
            }
        }
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int[] gardenNoAdj(int N, int[][] paths) {
        Map<Integer, Set<Integer>> G = new HashMap<>();
        for (int i = 0; i < N; i++) G.put(i, new HashSet<>());
        for (int[] p : paths) {
            G.get(p[0] - 1).add(p[1] - 1);
            G.get(p[1] - 1).add(p[0] - 1);
        }
        int[] res = new int[N];
        for (int i = 0; i < N; i++) {
            int[] colors = new int[5];
            for (int j : G.get(i))
                colors[res[j]] = 1;
            for (int c = 4; c > 0; --c)
                if (colors[c] == 0)
                    res[i] = c;
        }
        return res;
    }
}
```

#### 示例代码 (python)
```python
class Solution(object):
    def gardenNoAdj(self, N, paths):
        """
        :type N: int
        :type paths: List[List[int]]
        :rtype: List[int]
        """
        g = collections.defaultdict(list)
        for x, y in paths:
            g[x].append(y)
            g[y].append(x)
        plantdict = {i: 0 for i in range(1, N + 1)}
        for garden in g: 
            pick = set(range(1,5))
            for each in g[garden]:
                if plantdict[each] != 0 and plantdict[each] in pick:
                    pick.remove(plantdict[each])
            plantdict[garden] = pick.pop()
        return [plantdict[x] if plantdict[x] != 0 else 1 for x in range(1, N+1)]
```

#### 复杂度分析
时间复杂度: 每个点都会被`visit`一次，同时每次`visit`一个点，都会同时检查它连接的最多`3`个点。因此，时间复杂度就是O(N + 3\*N) = O(N)
空间复杂度: O(N)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/bzr104qA5Js)，欢迎关注！