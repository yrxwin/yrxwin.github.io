---
title: '[Leetcode 1056] Confusing Number'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-06-13 18:22:35
tags: ['Google','Math']
keywords:
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given a number&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">N</code>, return&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">true</code>&nbsp;if and only if it is a&nbsp;<em>confusing number</em>, which satisfies the following condition:</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">We can rotate digits by 180 degrees to form new digits. When 0, 1, 6, 8, 9 are rotated 180 degrees, they become 0, 1, 9, 8, 6 respectively. When 2, 3, 4, 5 and 7 are rotated 180 degrees, they become invalid. A&nbsp;<em>confusing number</em>&nbsp;is a number that when rotated 180 degrees becomes a&nbsp;<span style="font-weight: bolder;">different</span>&nbsp;number with each digit valid.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/23/1268_1.png" style="border-style: none; max-width: 100%; height: 90px; width: 180px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-1-1">6</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">true</span>
<span style="font-weight: bolder;">Explanation: </span>
We get <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">9</code> after rotating <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">6</code>, <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">9</code> is a valid number and <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">9!=6</code>.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/23/1268_2.png" style="border-style: none; max-width: 100%; height: 90px; width: 180px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-2-1">89</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">true</span>
<span style="font-weight: bolder;">Explanation: </span>
We get <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">68</code> after rotating <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">89</code>, <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">86</code> is a valid number and <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">86!=89</code>.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 3:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/26/1268_3.png" style="border-style: none; max-width: 100%; height: 121px; width: 301px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-3-1">11</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-3">false</span>
<span style="font-weight: bolder;">Explanation: </span>
We get <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">11</code> after rotating <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">11</code>, <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">11</code> is a valid number but the value remains the same, thus <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">11</code> is not a confusing number.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 4:</span></p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><img alt="" src="https://assets.leetcode.com/uploads/2019/03/23/1268_4.png" style="border-style: none; max-width: 100%; height: 90px; width: 180px;"></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-4-1">25</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-4">false</span>
<span style="font-weight: bolder;">Explanation: </span>
We get an invalid number after rotating <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">25</code>.</pre>
<!--more-->

#### 解题思路
我们用哈希表保存每个可以翻转的字符翻转后对应的字符，然后对每一位数字进行翻转，检查翻转后的数字和原来的数字是否相等即可。


#### 示例代码 (cpp)
```cpp
class Solution {
private:
    unordered_map<int,int> dict = {{0,0},{1,1},{6,9},{8,8},{9,6}};
public:
    bool confusingNumber(int N) {
        int rotate = 0;
        int init = N;
        while (init != 0) {
            int digit  = init % 10;
            if (!dict.count(digit)) {
            	return false;
            }
            rotate = rotate * 10 + dict[digit];
            init = init / 10;
        }
        return postNum != N;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public boolean confusingNumber(int N) {
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        map.put(6, 9);
        map.put(9, 6);
        map.put(0, 0);
        map.put(1, 1);
        map.put(8, 8); 
        int newNum = 0;
        int x = N;
        while (x != 0) {
            int remainder = x % 10;
            if (!map.containsKey(remainder)) 
                return false;
            if(newNum > Integer.MAX_VALUE/10)
                return false;
            newNum = newNum * 10 + map.get(remainder);
            x /= 10;
        }    
        return N == newNum? false: true;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def confusingNumber(self, N: int) -> bool:
        S = str(N)
        rotation = {"0" : "0", "1" : "1", "6" : "9", "8" : "8", "9" : "6"}
        result = []        
        for c in S[::-1]:           # iterate in reverse
            if c not in rotation:
                return False
            result.append(rotation[c])                
        return "".join(result) != S
```

#### 复杂度分析
时间复杂度: O(N)
空间复杂度: O(1)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/GSc-F_jlYWk)，欢迎关注！