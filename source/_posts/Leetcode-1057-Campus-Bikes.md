---
title: '[Leetcode 1057] Campus Bikes'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-06-21 23:52:07
tags: ['Amazon', 'Facebook', 'Greedy', 'Sort']
keywords: ['Amazon', 'Facebook', 'Greedy', 'Sort']
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">On a campus represented as a 2D grid, there are&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">N</code>&nbsp;workers and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">M</code>&nbsp;bikes, with&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">N &lt;= M</code>. Each worker and bike is a 2D coordinate on this grid.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Our goal is to assign a bike to each worker. Among the available bikes and workers, we choose the (worker, bike) pair with the shortest Manhattan distance between each other, and assign the bike to that worker. (If there are multiple (worker, bike) pairs with the same shortest Manhattan distance, we choose the pair with the smallest worker index; if there are multiple ways to do that, we choose the pair with the smallest bike index). We repeat this process until there are no available workers.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">The Manhattan distance between two points&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">p1</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">p2</code>&nbsp;is&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">Manhattan(p1, p2) = |p1.x - p2.x| + |p1.y - p2.y|</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Return a vector&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">ans</code>&nbsp;of length&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">N</code>, where&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">ans[i]</code>&nbsp;is the index (0-indexed) of the bike that the&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">i</code>-th worker is assigned to.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/06/1261_example_1_v2.png" style="border-style: none; max-width: 100%; height: 264px; width: 264px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>workers = <span id="example-input-1-1">[[0,0],[2,1]]</span>, bikes = <span id="example-input-1-2">[[1,2],[3,3]]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">[1,0]</span>
<span style="font-weight: bolder;">Explanation: </span>
Worker 1 grabs Bike 0 as they are closest (without ties), and Worker 0 is assigned Bike 1. So the output is [1, 0].
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/06/1261_example_2_v2.png" style="border-style: none; max-width: 100%; height: 264px; width: 264px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>workers = <span id="example-input-2-1">[[0,0],[1,1],[2,0]]</span>, bikes = <span id="example-input-2-2">[[1,0],[2,2],[2,1]]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">[0,2,1]</span>
<span style="font-weight: bolder;">Explanation: </span>
Worker 0 grabs Bike 0 at first. Worker 1 and Worker 2 share the same distance to Bike 2, thus Worker 1 is assigned to Bike 2, and Worker 2 will take Bike 1. So the output is [0,2,1].</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0 &lt;= workers[i][j], bikes[i][j] &lt; 1000</code></li><li>All worker and bike locations are distinct.</li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= workers.length &lt;= bikes.length &lt;= 1000</code></li></ol>
<!--more-->

#### 解题思路
这道题首先可以肯定是要遍历每一对可能的`worker`和`bike`，计算其距离
如果用priority queue，在pop出来的时候时间复杂度是`MNlog(MN)`的，这里由于距离最大是`2000`，
所以可以考虑用一个数组`buckets`来存储每一个距离对应的worker bike组合
即：`buckets[i]`对应所有距离为`i`的`WorkerBikePair`。
遍历一遍`workers`和`bikes`，更新`buckets`。
然后：
1. 用一个数组`bike_used`记录对应的`bike`是否被访问过。
2. 将需要返回的数组记为`results`,初始化为`-1`，这样`results`本身可以用来记录对应的`worker`是否访问过（`-1`则未被访问过）
3. 按顺序遍历`buckets`数组，并更新`results`和`bike_used`数组即可。

#### 示例代码 (cpp)
```cpp
class Solution {
    struct WorkerBikePair {
        int worker;
        int bike;
    };
public:
    vector<int> assignBikes(vector<vector<int>>& workers, vector<vector<int>>& bikes) {
        // vector<WorkerBikePair> in buckets[i] means all worker bike pairs with distance i.
        vector<vector<WorkerBikePair>> buckets(2001, vector<WorkerBikePair>()); 
        for (int i = 0; i < workers.size(); ++i) {
            for (int j = 0; j < bikes.size(); ++j) {
                int distance = abs(workers[i][0] - bikes[j][0]) + abs(workers[i][1] - bikes[j][1]);
                buckets[distance].push_back(WorkerBikePair{i, j});
            }
        }
        vector<int> results(workers.size(), -1);
        vector<bool> bike_used(bikes.size(), false);
        for (const auto& bucket : buckets) {
            for (const auto& worker_bike_pair : bucket) {
                if (!bike_used[worker_bike_pair.bike] && results[worker_bike_pair.worker] == -1) {
                    bike_used[worker_bike_pair.bike] = true;
                    results[worker_bike_pair.worker] = worker_bike_pair.bike;
                }
            }
        }
        return results;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
   public int[] assignBikes(int[][] workers, int[][] bikes) {
        int n = workers.length;
        
        // order by Distance ASC, WorkerIndex ASC, BikeIndex ASC
        PriorityQueue<int[]> q = new PriorityQueue<int[]>((a, b) -> {
            int comp = Integer.compare(a[0], b[0]);
            if (comp == 0) {
                if (a[1] == b[1]) {
                    return Integer.compare(a[2], b[2]);
                }
                
                return Integer.compare(a[1], b[1]);
            }
            
            return comp;
        });
            
        // loop through every possible pairs of bikes and people,
        // calculate their distance, and then throw it to the pq.
        for (int i = 0; i < workers.length; i++) {
            
            int[] worker = workers[i];
            for (int j = 0; j < bikes.length; j++) {
                int[] bike = bikes[j];
                int dist = Math.abs(bike[0] - worker[0]) + Math.abs(bike[1] - worker[1]);
                q.add(new int[]{dist, i, j}); 
            }
        }
        
        // init the result array with state of 'unvisited'.
        int[] res = new int[n];
        Arrays.fill(res, -1);
        
        // assign the bikes.
        Set<Integer> bikeAssigned = new HashSet<>();
        while (bikeAssigned.size() < n) {
            int[] workerAndBikePair = q.poll();
            if (res[workerAndBikePair[1]] == -1 
                && !bikeAssigned.contains(workerAndBikePair[2])) {   
                
                res[workerAndBikePair[1]] = workerAndBikePair[2];
                bikeAssigned.add(workerAndBikePair[2]);
            }
        }
        
        return res;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def assignBikes(self, workers: List[List[int]], bikes: List[List[int]]) -> List[int]:
        distances = []     # distances[worker] is tuple of (distance, worker, bike) for each bike 
        for i, (x, y) in enumerate(workers):
            distances.append([])
            for j, (x_b, y_b) in enumerate(bikes):
                distance = abs(x - x_b) + abs(y - y_b)
                distances[-1].append((distance, i, j))
            distances[-1].sort(reverse = True)  # reverse so we can pop the smallest distance
        
        result = [None] * len(workers)
        used_bikes = set()
        queue = [distances[i].pop() for i in range(len(workers))]   # smallest distance for each worker
        heapq.heapify(queue)
        
        while len(used_bikes) < len(workers):
            _, worker, bike = heapq.heappop(queue)
            if bike not in used_bikes:
                result[worker] = bike
                used_bikes.add(bike)
            else:
                heapq.heappush(queue, distances[worker].pop())  # bike used, add next closest bike
        
        return result
```

#### 复杂度分析
时间复杂度: `O(MN)` 如果用priority_queue则为`O(MNlog(MN))`
空间复杂度: `O(MN)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/21HYbNz15oc)，欢迎关注！