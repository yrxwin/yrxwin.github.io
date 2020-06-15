---
title: '[Leetcode 1053]Previous Permutation With One Swap'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-06-15 00:20:54
tags: ['Quora', 'Facebook', 'Array', 'Greedy']
keywords: ['Quora', 'Facebook', 'Array', 'Greedy']
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given an array&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A</code>&nbsp;of positive integers (not necessarily distinct), return the lexicographically largest permutation that is smaller than&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A</code>, that can be&nbsp;<span style="font-weight: bolder;">made with one swap</span>&nbsp;(A&nbsp;<em>swap</em>&nbsp;exchanges the positions of two numbers&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A[i]</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A[j]</code>).&nbsp; If it cannot be done, then return the same array.&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>[3,2,1]
<span style="font-weight: bolder;">Output: </span>[3,1,2]
<span style="font-weight: bolder;">Explanation: </span>Swapping 2 and 1.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>[1,1,5]
<span style="font-weight: bolder;">Output: </span>[1,1,5]
<span style="font-weight: bolder;">Explanation: </span>This is already the smallest permutation.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 3:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>[1,9,4,6,7]
<span style="font-weight: bolder;">Output: </span>[1,7,4,6,9]
<span style="font-weight: bolder;">Explanation: </span>Swapping 9 and 7.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 4:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>[3,1,1,3]
<span style="font-weight: bolder;">Output: </span>[1,3,1,3]
<span style="font-weight: bolder;">Explanation: </span>Swapping 1 and 3.</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= A.length &lt;= 10000</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= A[i] &lt;= 10000</code></li></ol>
<!--more-->

#### 解题思路
我们找到A当中需要交换的位置`left`和`right`：
left的位置应当尽量往右：应当为`A`从右往左第一个变大的位置，因为其右边肯定有比其小的值了。
找到`left`的位置后，`right`应当是`left`右侧最大的数：
由于`left`右侧为从右往左递减的序列（从左往右递增），所以需要从右往左找到第一个大于`A[left]`的数`A[right]`。
如果`A[right]`有连续相同的数，比如`[3, 1, 1, 3]`中中间连续的1，那么我们希望`right`指向最左侧的那个1。
所以我们还需要继续将`right`向左移直到`A[right] != A[right - 1]`。
此时交换`A[right]`与`A[left]`，并返回`A`即可。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    vector<int> prevPermOpt1(vector<int>& A) {
        if (A.size() <= 1) {
            return A;
        }
        // 找到从右往左第一个增大的位置left, 比如[3 1 1 3]中index 0
        int left = A.size() - 2;
        while (left >= 0 && A[left] <= A[left + 1]) {
            --left;
        }
        if (left < 0) {
            return A;
        }
        // 找到left右侧，从右往左第一个比A[left]小的位置right，比如[3 1 1 3]中index 2
        int right = A.size() - 1;
        while (A[right] >= A[left]) {
            --right;
        }
        // 从A[right]开始向左，最左边的连续与A[right]相同的位置，比如 [3 1 1 3]中index 1
        while (A[right] == A[right - 1]) {
            --right;
        }
        swap(A[left], A[right]);
        return A;
    }
};
```

#### 示例代码 (java)
```java
public class Solution {
    public int[] prevPermOpt1(int[] A) {
        // 1. 边界情况处理
        if (A.length == 1) {
            return A;
        }
 
        // 2. 找左边要交换的位置
        int left = A.length - 2;
        while (left >= 0) {
            if (A[left] > A[left + 1]) {
                break;
            }
            left--;
        }
 
        // 2.1 如果一直递减
        if (left < 0) {
            return A;
        }
 
        // 3. 找右边 第一个小于 left 的值
        int right = A.length - 1;
        while (A[right] >= A[left]) {
            right--;
        }
 
        // 4. 向左错位，如果 right 的左边 跟 right 一样
        int rightValue = A[right];
        while (A[right] == rightValue) {
            right--;
        }
        right++;
 
        // 5. 交换
        int temp = A[left];
        A[left] = A[right];
        A[right] = temp;
 
        return A;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def prevPermOpt1(self, A: List[int]) -> List[int]:
 
        # 1. 边界情况处理
        if len(A) == 1 :
            return A
 
        # 2. 找左边要交换的位置
        left = len(A) - 2
        while left >= 0 :
            if A[left] > A[left + 1] :
                break
            left -= 1
        else :
            # 2.1 如果一直递减
            return A
 
        # 3. 找右边 第一个小于 left 的值
        right = len(A) - 1
        while A[right] >= A[left] :
            right -= 1
        
        # 4. 向左错位，如果 right 的左边 跟 right 一样
        right_value = A[right]
        while (A[right] == right_value) :
            right -= 1
        right += 1
 
        # 5. 交换
        A[left], A[right] = A[right], A[left]
 
        return A
```

#### 复杂度分析
时间复杂度: `O(N)`
空间复杂度: `O(1)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/5O0erD3KHCU)，欢迎关注！