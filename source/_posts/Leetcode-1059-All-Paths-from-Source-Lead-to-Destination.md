---
title: '[Leetcode 1059] All Paths from Source Lead to Destination'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-06-21 23:52:35
tags: ['Google', 'Depth-first Search', 'Graph']
keywords: ['Google', 'Depth-first Search', 'Graph']
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given the&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">edges</code>&nbsp;of a directed graph, and two nodes&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">source</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">destination</code>&nbsp;of this graph, determine whether or not all paths starting from&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">source</code>&nbsp;eventually end at&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">destination</code>, that is:</p><ul style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li>At least one path exists from the&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">source</code>&nbsp;node to the&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">destination</code>&nbsp;node</li><li>If a path exists from the&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">source</code>&nbsp;node to a node with no outgoing edges, then that node is equal to&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">destination</code>.</li><li>The number of possible paths from&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">source</code>&nbsp;to&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">destination</code>&nbsp;is a finite number.</li></ul><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Return&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">true</code>&nbsp;if and only if all roads from&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">source</code>&nbsp;lead to&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">destination</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/16/485_example_1.png" style="border-style: none; max-width: 100%; height: 208px; width: 200px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>n = 3, edges = <span id="example-input-1-2">[[0,1],[0,2]]</span>, source = <span id="example-input-1-3">0</span>, destination = 2
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">false</span>
<span style="font-weight: bolder;">Explanation: </span>It is possible to reach and get stuck on both node 1 and node 2.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/16/485_example_2.png" style="border-style: none; max-width: 100%; height: 230px; width: 200px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>n = <span id="example-input-2-1">4</span>, edges = <span id="example-input-2-2">[[0,1],[0,3],[1,2],[2,1]]</span>, source = <span id="example-input-2-3">0</span>, destination = <span id="example-input-2-4">3</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">false</span>
<span style="font-weight: bolder;">Explanation: </span>We have two possibilities: to end at node 3, or to loop over node 1 and node 2 indefinitely.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 3:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/16/485_example_3.png" style="border-style: none; max-width: 100%; height: 183px; width: 200px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>n = <span id="example-input-3-1">4</span>, edges = <span id="example-input-3-2">[[0,1],[0,2],[1,3],[2,3]]</span>, source = <span id="example-input-3-3">0</span>, destination = <span id="example-input-3-4">3</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-3">true</span>
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 4:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/16/485_example_4.png" style="border-style: none; max-width: 100%; height: 183px; width: 200px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>n = <span id="example-input-4-1">3</span>, edges = <span id="example-input-4-2">[[0,1],[1,1],[1,2]]</span>, source = <span id="example-input-4-3">0</span>, destination = <span id="example-input-4-4">2</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-4">false</span>
<span style="font-weight: bolder;">Explanation: </span>All paths from the source node end at the destination node, but there are an infinite number of paths, such as 0-1-2, 0-1-1-2, 0-1-1-1-2, 0-1-1-1-1-2, and so on.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 5:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/16/485_example_5.png" style="border-style: none; max-width: 100%; height: 131px; width: 150px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>n = <span id="example-input-5-1">2</span>, edges = <span id="example-input-5-2">[[0,1],[1,1]]</span>, source = <span id="example-input-5-3">0</span>, destination = <span id="example-input-5-4">1</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-5">false</span>
<span style="font-weight: bolder;">Explanation: </span>There is infinite self-loop at destination node.</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li><italic>The given graph may have self loops and parallel edges.</italic></li><li>The number of nodes&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">n</code>&nbsp;in the graph is between&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">10000</code></li><li>The number of edges in the graph is between&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">10000</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0 &lt;= edges.length &lt;= 10000</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">edges[i].length == 2</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0 &lt;= source &lt;= n - 1</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0 &lt;= destination &lt;= n - 1</code></li></ol>
<!--more-->

#### 解题思路
使用DFS，用一个数组`visited`来记录以每一个节点为`source`，到`destination`应当返回的值(not visited, true, or false)。
然后要明确边界条件：
1. 当遇到一个没有出度的节点，则需要判断是否该点为`destination`，是的话返回`true`，不然则为`false`。
2. 判断当前节点是否被访问过，如果访问过，则返回visited对应的值。

在DFS中，要首先将`visited[source]`记录为`isFalse`, 然后再开始递归，这样遇到cycle，则会返回`false`，不然就会返回`true`，那就不对了。
DFS要求`source`的每一个child到`destination`都为`true`，这样`source`到`destination`也为`true`，反之则为`false`。

#### 示例代码 (cpp)
```cpp
class Solution {
    enum State {notVisited, isTrue, isFalse};
    bool dfs(const vector<vector<int>>& mapping, int source, int destination, vector<State>& visited) {
        if (mapping[source].empty()) {
            if (source == destination) {
                return true;
            }
            return false;
        }
        if (visited[source] != notVisited) {
            return visited[source] == isTrue;
        }
        visited[source] = isFalse;
        for (const auto child : mapping[source]) {
            if (!dfs(mapping, child, destination, visited)) {
                return false;
            }
        }
        visited[source] = isTrue;
        return true;
    }
public:
    bool leadsToDestination(int n, vector<vector<int>>& edges, int source, int destination) {
        vector<vector<int>> mapping(n, vector<int>());
        for (const auto& edge : edges) {
            mapping[edge[0]].push_back(edge[1]);
        }
        vector<State> visited(n, notVisited);
        return dfs(mapping, source, destination, visited);
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    enum State { PROCESSING, PROCESSED }
    
    public boolean leadsToDestination(int n, int[][] edges, int src, int dest) {
        List<Integer>[] graph = buildDigraph(n, edges);
        return leadsToDest(graph, src, dest, new State[n]);
    }
    
    private boolean leadsToDest(List<Integer>[] graph, int node, int dest, State[] states) {
        if (states[node] != null) return states[node] == State.PROCESSED;
        if (graph[node].isEmpty()) return node == dest;
        states[node] = State.PROCESSING;
        for (int next : graph[node]) {
            if (!leadsToDest(graph, next, dest, states)) return false;
        }
        states[node] = State.PROCESSED;
        return true;
    }
    
    private List<Integer>[] buildDigraph(int n, int[][] edges) {
        List<Integer>[] graph = new List[n];
        for (int i = 0; i < n; i++) {
            graph[i] = new ArrayList<>();
        }
        for (int[] edge : edges) {
            graph[edge[0]].add(edge[1]);
        }
        return graph;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def leadsToDestination(self, n: int, edges: List[List[int]], source: int, destination: int) -> bool:
        def dfs(i):
            seen.add(i)
            for j in graph[i]:
                if j == i or j in seen or not dfs(j):
                    return False
            seen.discard(i)
            return len(graph[i]) != 0 or i == destination
        graph, seen = collections.defaultdict(set), set()
        for a, b in edges:
            graph[a].add(b)
        return dfs(source)
```

#### 复杂度分析
时间复杂度: `O(N)`
空间复杂度: `O(N)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/FzRFfyyCMP0)，欢迎关注！