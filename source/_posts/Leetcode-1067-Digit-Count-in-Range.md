---
title: '[Leetcode 1067] Digit Count in Range'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-07-26 19:15:02
tags: ['Amazon', 'Math', 'Dynamic Programming']
keywords: ['Amazon', 'Math', 'Dynamic Programming']
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given an integer&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">d</code>&nbsp;between&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">9</code>, and two positive integers&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">low</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">high</code>&nbsp;as lower and upper bounds, respectively. Return the number of times that&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">d</code>&nbsp;occurs as a digit in all integers between&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">low</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">high</code>, including the bounds&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">low</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">high</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>d = <span id="example-input-1-1">1</span>, low = <span id="example-input-1-2">1</span>, high = <span id="example-input-1-3">13</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">6</span>
<span style="font-weight: bolder;">Explanation: </span>
The digit <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">d=1</code> occurs <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">6</code> times in <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">1,10,11,12,13</code>. Note that the digit <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">d=1</code> occurs twice in the number <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">11</code>.
</pre><div style="color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>d = <span id="example-input-2-1">3</span>, low = <span id="example-input-2-2">100</span>, high = <span id="example-input-2-3">250</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">35</span>
<span style="font-weight: bolder;">Explanation: </span>
The digit <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">d=3</code> occurs <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">35</code> times in <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">103,113,123,130,131,...,238,239,243</code>.</pre><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0 &lt;= d &lt;= 9</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= low &lt;= high &lt;= 2×10^8</code></li></ol></div>
<!--more-->

#### 解题思路
这道题我们用递归的方式，递归函数为`recursiveCount(N, d)`, 将`N`当中出现`d`的次数分为个位数中出现的次数，加上非个位数出现的次数。
个位数出现的次数为`N/10`, 非个位数中出现的次数为`recursiveCount(N / 10, d) * 10`, 可以理解为`N / 10`中每一个数都可以加后缀0 - 9成为`N`中的一个数字。
当然还要考虑最后一位的大小，从而加减一个偏差，详见代码注释。

#### 示例代码 (cpp)
```cpp
class Solution {
    int recursiveCount(int N, int d) {
        // 退出条件
        if (N <= 9) {
            return d == 0 ? 0 : (d <= N);
        }
        int ret = 0;
        // 个位数字d出现的次数，不包含最后一次，e.g. N=797，这里只计算1 - 789之间个位数字出现d的次数
        ret += (d == 0 ? (N / 10 - 1) : N / 10);
        // 判断最后一次个位数字是否包含d，e.g. N=797，判断790-797之间个位数字是否出现d
        if (N % 10 >= d) {
            ++ret;
        }
        // 除了个位数字以外其他位数d出现的个数, e.g. N=797，我们计算了1 - 799之间非个位数字出现d的次数
        ret += recursiveCount(N / 10, d) * 10;
        // 前面默认最后一位到9，因此我们要减去最后一位不到9的情况，e.g. N=797, 我们计算798 - 799两数非个位数字出现d的次数
        string nstr = to_string(N / 10);
        ret -= std::count(nstr.begin(), nstr.end(), d + '0') * (9 - N % 10);
        return ret;
    }
public:
    int digitsCount(int d, int low, int high) {
        return recursiveCount(high, d) - recursiveCount(low - 1, d);
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int digitsCount(int d, int low, int high) {
        return countDigit(high, d) - countDigit(low-1, d);
    }
    
    int countDigit(int n, int d) {
        if(n < 0 || n < d) {
            return 0;
        }
        
        int count = 0;
        for(long i = 1; i <= n; i*= 10) {
            long divider = i * 10;
            count += (n / divider) * i;
            
            if (d > 0) {
                count += Math.min(Math.max(n % divider - d * i + 1, 0), i); // comment1: tailing number need to be large than d *  i to qualify.
            } else {
                if(n / divider > 0) {
                    if(i > 1) {  // comment2: when d == 0, we need avoid to take numbers like 0xxxx into account.
                        count -= i;
                        count += Math.min(n % divider + 1, i);  
                    }
                }
            }
        }
        
        return count;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def digitsCount(self, d: int, low: int, high: int) -> int:
        def helper(n, k):
            pivot, res = 1, 0
            while n >= pivot:
                res += (n // (10 * pivot)) * pivot + min(pivot, max(n % (10 * pivot) - k * pivot + 1, 0))
                res -= pivot if k == 0 else 0 # no leading zero
                pivot *= 10
            return res + 1 # last-digit can be zero
        return helper(high, d) - helper(low-1, d)
```

#### 复杂度分析
时间复杂度: `O(log(N))`
空间复杂度: `O(1)`

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/wtiNO6BmTfg)，欢迎关注！