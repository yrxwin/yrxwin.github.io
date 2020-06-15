---
title: '[Leetcode 1055]Shortest Way to Form String'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-06-15 00:21:23
tags: ['Google', 'Dynamic Programming', 'Greedy']
keywords: ['Google', 'Dynamic Programming', 'Greedy']
description: 
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">From any string, we can form a&nbsp;<i>subsequence</i>&nbsp;of that string by deleting some number of characters (possibly no deletions).</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given two strings&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">source</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">target</code>, return the minimum number of subsequences of&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">source</code>&nbsp;such that their concatenation equals&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">target</code>. If the task is impossible, return&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">-1</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>source = <span id="example-input-1-1">"abc"</span>, target = <span id="example-input-1-2">"abcbc"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">2</span>
<span style="font-weight: bolder;">Explanation: </span>The target "abcbc" can be formed by "abc" and "bc", which are subsequences of source "abc".
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>source = <span id="example-input-2-1">"abc"</span>, target = <span id="example-input-2-2">"acdbc"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">-1</span>
<span style="font-weight: bolder;">Explanation: </span>The target string cannot be constructed from the subsequences of source string due to the character "d" in target string.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 3:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>source = <span id="example-input-3-1">"xyz"</span>, target = <span id="example-input-3-2">"xzyxz"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-3">3</span>
<span style="font-weight: bolder;">Explanation: </span>The target string can be constructed as follows "xz" + "y" + "xz".</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Constraints:</span></p><ul style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li>Both the&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">source</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">target</code>&nbsp;strings consist of only lowercase English letters from "a"-"z".</li><li>The lengths of&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">source</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">target</code>&nbsp;string are between&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1000</code>.</li></ul>
<!--more-->

#### 解题思路
`O(MN)`的解法较为直观，只需要用两个`index` `i`和`j`分别对应`source`和`target`的位置，然后对于每一个`target[j]`,在`source`中找到对应的`source[i]`, 并于每次i归零时计数即可。
这里介绍`O(M + N)`的解法：用一个二维哈希表（或者二维数组）`index_to_next`来表示当前`source`的`index`右边（包括`index`本身), 每一个字母第一次出现的位置的下一个位置。比如`abbc`，那么`index[0]['a'] = 1, index[0]['b'] = 2, index[1]['b'] = 2, index[2]['b'] = 3...`
从右向左遍历一遍`source`即可完成更新`index_to_next`, 然后遍历`target`，`source`和`target`的位置分别记为`i`和`j`，我们执行以下操作：
1. `index_to_next[0]`当中是否存在`target[j]`，即整个`source`中是否存在`j`，不存在则返回`-1`
2. `index_to_next[i]`当中是否存在`target[j]`，如果不存在，说明`source`在位置`i`右侧不存在`target[j]`，`i`应当归零从头开始找
3. 如果`i == 0`，说明`source`被遍历了一边，返回值`round`应该增加1
4. 更新`i = index_to_next[i][target[i]]` 即`source`中`i`右侧第一个`target[j]`的右侧的位置，这样相当于在`source`中读取了一个最近的`target[i]`
最后返回`round`即可。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int shortestWay(string source, string target) {
        // 第一个int：source当前index
        // 第二个int：souce中读取对应的char后，下一个index
        unordered_map<int, unordered_map<char, int>> index_to_next;
        index_to_next[source.size() - 1][source.back()] = 0;
        for (int i = source.size() - 2; i >= 0; --i) {
            index_to_next[i] = index_to_next[i + 1];
            index_to_next[i][source[i]] = i + 1;
        }
        int round = 0, i = 0;
        for (int j = 0; j < target.size(); ++j) {
            // 整个source中都没有target[j]，直接返回-1
            if (index_to_next[0].count(target[j]) == 0) {
                return -1;
            }
            // 当前source的位置i往后找不到target[j], 则应该将i归零重头开始找
            if (index_to_next[i].count(target[j]) == 0) {
                i = 0;
            }
            if (i == 0) {
                ++round;
            }
            i = index_to_next[i][target[j]];
        }
        return round;
    }
};
```

#### 示例代码 (java)
```java
public int shortestWay(String source, String target) {
    char[] cs = source.toCharArray(), ts = target.toCharArray();
    int[][] idx = new int[cs.length][26];
    idx[cs.length - 1][cs[cs.length - 1] - 'a'] = cs.length; 
    for (int i = cs.length - 2; i >= 0; i--) {
        idx[i] = Arrays.copyOf(idx[i + 1],26);
        idx[i][cs[i] - 'a'] = i + 1; 
    }
    int j = 0, res = 1;
    for (int i = 0; i < ts.length; i++) {
        if (j == cs.length) {
            j = 0;
            res++;
        }
        j = idx[j][ts[i] - 'a'];
        if (idx[0][ts[i] - 'a'] == 0) return -1;
        if (j == 0) {
            res++;
            i--;
        }
    }
    return res;
}
```

#### 示例代码 (python)
```python
# two pointer greedy O(MN)
class Solution:
    def shortestWay(self, source: str, target: str) -> int:
        num = 0
        t_p = 0
        while t_p < len(target):
            s_p = 0
            flag = False
            while s_p < len(source) and t_p < len(target):
                if source[s_p] == target[t_p]:
                    s_p += 1
                    t_p +=1
                    flag = True
                else:
                    s_p +=1
                    
            if flag == True:
                num +=1
            else:
                return -1
        return num 

# binary search O(NlogM)  
from collections import defaultdict
class Solution:
    
    def shortestWay(self, source: str, target: str) -> int:
        dic = defaultdict(list)
        for ind, char in enumerate(source):
            dic[char].append(ind)
        
        ind = 0
        ans = 1
        for char in target:
            if char not in dic:
                return -1
            else:
                ind, ans= self.binarysearch(source, char, ind, dic, ans)
                
        return ans
                    
    def binarysearch(self, source, char, ind, dic, ans):
        lis = dic[char]
        
        if lis[-1] < ind:
            ans += 1
            ind = 0
            
        l = 0
        r = len(lis)-1
        while l < r:
            mid = (l+r)//2
            if lis[mid] < ind:
                l = mid +1
            else:
                r = mid
    
        return lis[l]+1, ans

# O(N + M) char to index
class Solution:
    def shortestWay(self, source: str, target: str) -> int:
        source_set = set(source)
        
        lis = [[-1]*len(source) for _ in range(26)]
        for ind, char in enumerate(source):
            lis[ord(char)- ord('a')][ind] = ind
        
        for l in lis:
            pre = -1
            for i in range(len(l)-1,-1,-1):
                if l[i] != -1:
                    pre = l[i]
                else:
                    l[i] = pre
        ans = 1
        ind = 0
        for char in target:
            if char not in source_set:
                return -1
            if ind >= len(source):
                ind = 0
                ans += 1
            ind = lis[ord(char) - ord('a')][ind]
            if ind == -1:
                ind = lis[ord(char) - ord('a')][0]  
                ans += 1
            ind +=1

        return ans

# O(N + M)index to char
class Solution:
    def shortestWay(self, source: str, target: str) -> int:
        source_set = set(source)
        
        lis = [[-1]*26 for _ in range(len(source))]
        for i in range(len(lis)-1, -1, -1):
            if i == len(lis)-1:
                lis[i][ord(source[i]) - ord('a')] = i
            else:
                lis[i][:] = lis[i+1]
                lis[i][ord(source[i])-ord('a')] = i 
        
        ans = 1
        ind = 0
        for char in target:
            if char not in source_set:
                return -1
            if ind >= len(lis):
                ind = 0 
                ans +=1
                
            ind = lis[ind][ord(char)-ord('a')]
            if ind == -1:
                ans +=1
                ind = 0
                ind = lis[ind][ord(char)-ord('a')]
            
            ind +=1
            
        return ans
```

#### 复杂度分析
时间复杂度: `O(M + N)`
空间复杂度: `O(M)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/vxuKSdiu-8U)，欢迎关注！