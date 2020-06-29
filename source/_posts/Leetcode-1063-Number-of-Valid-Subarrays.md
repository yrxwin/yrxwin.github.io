---
title: '[Leetcode 1063] Number of Valid Subarrays'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-06-29 00:26:05
tags: ['Hulu', 'Stack']
keywords: ['Hulu', 'Stack']
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given an array&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A</code>&nbsp;of integers, return the number of&nbsp;<span style="font-weight: bolder;">non-empty continuous subarrays</span>&nbsp;that satisfy the following condition:</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">The leftmost element of the subarray is not larger than other elements in the subarray.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-1-1">[1,4,2,5,3]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">11</span>
<span style="font-weight: bolder;">Explanation: </span>There are 11 valid subarrays: [1],[4],[2],[5],[3],[1,4],[2,5],[1,4,2],[2,5,3],[1,4,2,5],[1,4,2,5,3].
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-2-1">[3,2,1]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">3</span>
<span style="font-weight: bolder;">Explanation: </span>The 3 valid subarrays are: [3],[2],[1].
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 3:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-3-1">[2,2,2]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-3">6</span>
<span style="font-weight: bolder;">Explanation: </span>There are 6 valid subarrays: [2],[2],[2],[2,2],[2,2],[2,2,2].</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= A.length &lt;= 50000</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0 &lt;= A[i] &lt;= 100000</code></li></ol>
<!--more-->

#### 解题思路
建立一个从顶往下递减的栈`stk`，遍历`nums`中每个元素`num`，比较`num`与栈顶元素大小。
如果`num`较大，则不断`pop`栈顶元素，直到栈空或者栈顶元素小于等于`num`，然后将`num`插入栈顶。
此时，我们可以以`stk`中任意元素为开头，以`num`为结尾组成符合题目条件的subarray，因此
以`num`为结尾的subarray个数为`stk`的`size`。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int validSubarrays(vector<int>& nums) {
        stack<int> stk;
        int count = 0;
        for (const auto num : nums) {
            while (!stk.empty() && num < stk.top()) {
                stk.pop();
            }
            stk.push(num);
            count += stk.size();
        }
        return count;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int validSubarrays(int[] nums) {
        int res = nums.length;
        if(nums.length <= 1) {
            return res;
        }
        Deque<Integer> stack = new ArrayDeque<>();
        stack.push(nums[0]);
        for(int i = 1; i < nums.length; i++) {
            int num = nums[i];
            while(!stack.isEmpty() && num < stack.peek()) {
                stack.pop();
            }
            res += stack.size();
            stack.push(num);
        }
        return res;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def validSubarrays(self, nums: List[int]) -> int:
        stack = []
        nextSmaller = [len(nums)] * len(nums)
        for i, v in enumerate(nums):
            while stack and stack[-1][1] > v:
                nextSmaller[stack.pop()[0]] = i
            stack.append([i, v])
        return sum([v - i for i, v in enumerate(nextSmaller)])
```

#### 复杂度分析
时间复杂度: `O(N)`
空间复杂度: `O(N)`

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/tVU8DhZbXCw)，欢迎关注！