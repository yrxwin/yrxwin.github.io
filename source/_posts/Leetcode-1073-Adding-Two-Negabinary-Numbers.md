---
title: '[Leetcode 1073] Adding Two Negabinary Numbers'
categories:
  - leetcode
author: '猩猩管理员'
date: 2020-08-02 18:28:55
tags: ['Grab', 'Math']
keywords: ['Grab', 'Math']
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given two numbers&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">arr1</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">arr2</code>&nbsp;in base&nbsp;<span style="font-weight: bolder;">-2</span>, return the result of adding them together.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Each number is given in&nbsp;<em>array format</em>:&nbsp; as an array of 0s and 1s, from most significant bit to least significant bit.&nbsp; For example,&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">arr = [1,1,0,1]</code>&nbsp;represents the number&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">(-2)^3&nbsp;+ (-2)^2 + (-2)^0 = -3</code>.&nbsp; A number&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">arr</code>&nbsp;in&nbsp;<em>array format</em>&nbsp;is also guaranteed to have no leading zeros: either&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">arr == [0]</code>&nbsp;or&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">arr[0] == 1</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Return the result of adding&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">arr1</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">arr2</code>&nbsp;in the same format: as an array of 0s and 1s with no leading zeros.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>arr1 = <span id="example-input-1-1">[1,1,1,1,1]</span>, arr2 = <span id="example-input-1-2">[1,0,1]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">[1,0,0,0,0]
</span><span style="font-weight: bolder;">Explanation: </span>arr1 represents 11, arr2 represents 5, the output represents 16.</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= arr1.length &lt;= 1000</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= arr2.length &lt;= 1000</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">arr1</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">arr2</code>&nbsp;have no leading zeros</li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">arr1[i]</code>&nbsp;is&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0</code>&nbsp;or&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">arr2[i]</code>&nbsp;is&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">0</code>&nbsp;or&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1</code></li></ol>
<!--more-->

#### 解题思路
这道题主要考察bit manipulation，也就是位数的转换。
与base 2相比，只需要每次`carry`变换符号即可，因为相邻位上`-2^n`与`-2^(n+1)`的符号相反。
但要注意，我们一定要使用`current & 1` 以及 `-(current >> 1)` 来计算当前位的值以及`carry`的值，
如果使用`%`和除法的话，对于负数将得到错误的结果。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    vector<int> addNegabinary(vector<int>& arr1, vector<int>& arr2) {
        vector<int> rets;
        int carry = 0;
        int i = arr1.size() - 1;
        int j = arr2.size() - 1;
        while (i >= 0 || j >= 0 || carry != 0) {
            int current = carry;
            if (i >= 0) {
                current += arr1[i];
            }
            if (j >= 0) {
                current += arr2[j];
            }
            // 当current = -1时，使用 current % 1将得到-1
            rets.push_back(current & 1);
            // 当current = -1时，使用 -current / 2将得到0
            carry = -(current >> 1);
            --i;
            --j;
        }
        // 把前缀为0的位数去除，只保留最后一位
        while (rets.size() > 1 && rets.back() == 0) {
            rets.pop_back();
        }
        reverse(rets.begin(), rets.end());
        return rets;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int[] addNegabinary(int[] arr1, int[] arr2) {
        int i = arr1.length - 1, j = arr2.length - 1, carry = 0;
        Stack<Integer> stack = new Stack<>();
        while (i >= 0 || j >= 0 || carry != 0) {
            int v1 = i >= 0 ? arr1[i--] : 0;
            int v2 = j >= 0 ? arr2[j--] : 0;
            carry = v1 + v2 + carry;
            stack.push(carry & 1);
            carry = -(carry >> 1);
        }
        while (!stack.isEmpty() && stack.peek() == 0) stack.pop();
        int[] res = new int[stack.size()];
        int index = 0;
        while (!stack.isEmpty()) {
            res[index++] = stack.pop();
        }
        return res.length == 0 ? new int[1] : res;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def addNegabinary(self, arr1: List[int], arr2: List[int]) -> List[int]:
        res = []
        carry = 0
        while arr1 or arr2 or carry:
            carry += (arr1 or [0]).pop() + (arr2 or [0]).pop()
            res.append(carry & 1)
            carry = -(carry >> 1)
        while len(res) > 1 and res[-1] == 0:
            res.pop()
        return res[::-1]
```

#### 复杂度分析
时间复杂度: `O(M + N)`
空间复杂度: `O(1)`

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/I8cGuDVViq8)，欢迎关注！