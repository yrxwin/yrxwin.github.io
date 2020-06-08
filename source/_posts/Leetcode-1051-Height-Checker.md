---
title: '[Leetcode 1051] Height Checker'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-06-07 23:28:48
tags: ['Google', 'Array']
keywords: ['Google', 'Array']
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Students are asked to stand in non-decreasing order of heights for an annual photo.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Return the minimum number of students that must move in order for all students to be standing in non-decreasing order of height.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Notice that when a group of students is selected they can reorder in any possible way between themselves and the non selected students&nbsp;remain on their seats.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;<span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input:</span> heights = [1,1,4,2,1,3]
<span style="font-weight: bolder;">Output:</span> 3
<span style="font-weight: bolder;">Explanation:</span> 
Current array : [1,1,4,2,1,3]
Target array  : [1,1,1,2,3,4]
On index 2 (0-based) we have 4 vs 1 so we have to move this student.
On index 4 (0-based) we have 1 vs 3 so we have to move this student.
On index 5 (0-based) we have 3 vs 4 so we have to move this student.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input:</span> heights = [5,1,2,3,4]
<span style="font-weight: bolder;">Output:</span> 5
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 3:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input:</span> heights = [1,2,3,4,5]
<span style="font-weight: bolder;">Output:</span> 0
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Constraints:</span><br></p><ul style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= heights.length &lt;= 100</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= heights[i] &lt;= 100</code></li></ul>
<!--more-->

#### 解题思路
这道题可以有很多做法。最高效的方法是：
建立一个数组`height_to_num`, 其`index`为`height`，对应的值为`height`出现的次数，该数组可替代排序
遍历一遍`heights`数组来更新`height_to_num`。
然后再遍历一遍`heights`数组，同时从`height_to_num`中找到排序后的高度`sort_height`,
比较`height`和`sort_height`, 如果不同则返回结果`+1`。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    // Use height as vector index to aovid sorting
    int heightChecker(vector<int>& heights) {
        vector<int> height_to_num = vector<int>(101, 0);
        for (const auto height : heights) {
            height_to_num[height]++;
        }
        int switch_count = 0;
        int sort_height = 0;
        for (const auto height : heights) {
            while (height_to_num[sort_height] == 0) {
                ++sort_height;
            }
            if (sort_height != height) {
                ++switch_count;
            }
            height_to_num[sort_height]--;
        }
        return switch_count;
    }
    // use sort 
    // O(nlogn)
    int heightChecker(vector<int>& heights) {
        const auto original_heights = heights;
        sort(heights.begin(), heights.end());
        int switch_count = 0;
        for (int i = 0; i < heights.size(); ++i) {
            if (heights[i] != original_heights[i]) {
                ++switch_count;
            }
        }
        return switch_count;
    } 
    // use priority queue 
    // O(nlogn)
    int heightChecker(vector<int>& heights) {
        priority_queue<int, vector<int>, greater<int>> pq(heights.begin(), heights.end());
        int switch_count = 0;
        for (const auto height : heights) {
            int sort_height = pq.top();
            pq.pop();
            if (sort_height != height) {
                ++switch_count;
            }
        }
        return switch_count;
    } 
};
```

#### 示例代码 (java)
```java
class Solution {
    public int heightChecker(int[] heights) {
        int[] heightToFreq = new int[101];
        
        for (int height : heights) {
            heightToFreq[height]++;
        }
        
        int result = 0;
        int curHeight = 0;
        
        for (int i = 0; i < heights.length; i++) {
            while (heightToFreq[curHeight] == 0) {
                curHeight++;
            }
            
            if (curHeight != heights[i]) {
                result++;
            }
            heightToFreq[curHeight]--;
        }
        
        return result;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def heightChecker(self, heights: List[int]) -> int:
        return sum(h1 != h2 for h1, h2 in zip(heights, sorted(heights))) 
```

#### 复杂度分析
时间复杂度: `O(N)`
空间复杂度: `O(height)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/qrfuxwcpJzY)，欢迎关注！