---
title: '[Leetcode 1058] Minimize Rounding Error to Meet Target'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-06-21 12:39:27
tags: ['Math', 'Greedy', 'Heap', 'Airbnb']
keywords: 
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given an array of prices&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">[p<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">1</span>,p<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">2</span>...,p<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">n</span>]</code>&nbsp;and a&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">target</code>, round each price&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">p<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">i</span></code>&nbsp;to&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">Round<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">i</span>(p<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">i</span>)</code>&nbsp;so that the rounded array&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">[Round<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">1</span>(p<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">1</span>),Round<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">2</span>(p<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">2</span>)...,Round<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">n</span>(p<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">n</span>)]</code>&nbsp;sums to the given&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">target</code>. Each operation&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">Round<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">i</span>(p<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">i</span>)</code>&nbsp;could be either&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">Floor(p<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">i</span>)</code>&nbsp;or&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">Ceil(p<span style="font-size: 9.75px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">i</span>)</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Return the string&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">"-1"</code>&nbsp;if the rounded array is impossible to sum to&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">target</code>. Otherwise, return the smallest rounding error, which is defined as Σ |Round<span style="font-size: 10.5px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">i</span>(p<span style="font-size: 10.5px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">i</span>) - (p<span style="font-size: 10.5px; line-height: 0; position: relative; vertical-align: baseline; bottom: -0.25em;">i</span>)| for&nbsp;<italic>i</italic>&nbsp;from 1 to&nbsp;<italic>n</italic>, as a string with three places after the decimal.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>prices = <span id="example-input-1-1">["0.700","2.800","4.900"]</span>, target = <span id="example-input-1-2">8</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">"1.000"</span>
<span style="font-weight: bolder;">Explanation: </span>
Use Floor, Ceil and Ceil operations to get (0.7 - 0) + (3 - 2.8) + (5 - 4.9) = 0.7 + 0.2 + 0.1 = 1.0 .
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>prices = <span id="example-input-2-1">["1.500","2.500","3.500"]</span>, target = <span id="example-input-2-2">10</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">"-1"</span>
<span style="font-weight: bolder;">Explanation: </span>
It is impossible to meet the target.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= prices.length &lt;= 500</code>.</li><li>Each string of prices&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">prices[i]</code>&nbsp;represents a real number which is between 0 and 1000 and has exactly 3 decimal places.</li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">target</code>&nbsp;is between 0 and 1000000.</li></ol>
<!--more-->

#### 解题思路
如果一个数字是一个整数， 那么我们只能取`floor`，不能取`ceil`。这相当于一个无法调整的数字，否则就是一个可调整的数字。我们把所有可调整的数字的小数部分放入一个`priority queue`中，把`priority queue`的`size`记为`pqsize`。 

然后我们先判断什么情况下无法得到target：
1. 如果取最小的可能的和，那么所有数字都要取floor。如果这个和仍然比target大，或者比`target-pqsize`小，那么就说明无论如何也不可能得到`target`。这样我们就返回 `“-1”`
2. 若满足上述条件，我们一定可以取到满足题目条件的和。我们需要知道调整多少个数字，即把floor操作变成ceil操作。需要调整的数字个数等于`target-pqsize`。
3. 为了的达到最小的`rounding error`，对于每个调整的操作，我们希望它们小数尽可能大，这可以由之前的`priority queue`得到。取那个数字的`ceil`。最后把所有不需要调整的小数也加上，就是最小的`rounding error`了。

注意最后返回字符串是，需要做些特殊处理，只保留最后3位小数即可。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    string minimizeError(vector<string>& prices, int target) {
        priority_queue<double> pq;
        int sum = 0;
        for (auto price : prices) {
            sum += floor(stod(price));
            double diffPrice = stod(price) - floor(stod(price));
            if (diffPrice != 0) {
                pq.push(diffPrice);
            }
        }
        if (sum > target || sum < target - pq.size()) {
            return "-1";
        }
        int diff = target - sum;
        double error = 0;
        while (!pq.empty()) {
            double fl = pq.top();
            pq.pop();
            error += diff > 0 ? 1 - fl : fl;
            diff--;
        }        
        string ans = to_string(error);
        return ans.substr(0, ans.find('.') + 4);
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public String minimizeError(String[] prices, int target) {
        float res = 0;
        PriorityQueue<Double> diffHeap = new PriorityQueue<>();
        
        for (String s : prices) {
            float f = Float.valueOf(s);
            double low = Math.floor(f);
            double high = Math.ceil(f);
            
            if (low != high)
                diffHeap.offer((high-f)-(f-low));
            
            res += f-low;
            target -= low;
        }
        
        if (target < 0 || target > diffHeap.size())
            return "-1";
        
        while (target-- > 0)
            res += diffHeap.poll();
        
        return String.format("%.3f", res);
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def minimizeError(self, prices: List[str], target: int) -> str:
        diff = []
        low, high = 0, 0
        for i, p in enumerate(map(float, prices)):
            f, c = math.floor(p), math.ceil(p)
            low, high = low + f, high + c
            fDiff, cDiff = p - f, c - p
            diff.append((fDiff - cDiff, fDiff, cDiff))
        if not low <= target <= high:
            return "-1"
        ceilN = target - low
        diff = sorted(diff, reverse=True)
        return "{:.3f}".format(sum([d[2] for d in diff[:ceilN]]) + sum([d[1] for d in diff[ceilN:]]))
```

#### 复杂度分析
时间复杂度: O(NlogN)
空间复杂度: O(N)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/d35MHk_Krgc)，欢迎关注！