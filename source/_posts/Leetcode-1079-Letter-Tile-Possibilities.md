---
title: '[Leetcode 1079] Letter Tile Possibilities'
categories:
  - leetcode
author: '猩猩管理员'
date: 2020-08-09 17:22:00
tags: ['Microsoft', 'Backtracking']
keywords: ['Microsoft', 'Backtracking']
description:
---
#### 原题说明
<div class="sql-schema-wrapper__3VBi" style="margin-bottom: 15px; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56);">You have a set of&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">tiles</code>, where each tile has one letter&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">tiles[i]</code>&nbsp;printed on it.&nbsp; Return the number of possible non-empty sequences of letters you can make.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56);">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56);"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-1-1">"AAB"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">8</span>
<span style="font-weight: bolder;">Explanation: </span>The possible sequences are "A", "B", "AA", "AB", "BA", "AAB", "ABA", "BAA".
</pre><div><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-2-1">"AAABBC"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">188</span></pre></div><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56);"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= tiles.length &lt;= 7</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">tiles</code>&nbsp;consists of uppercase English letters.</li></ol></div>
<!--more-->

#### 解题思路
采用递归的方式。用一个长度为26的`vector<int> ch_count`来记录当前剩余的每一个字母及对应的个数。
在递归函数`dfsCount`中，用`int count`表示当前`ch_count`能够组成的序列数，
遍历`ch_count`，每一个对应个数不为零的字母可以加入组合中，`count++`，对应的字母个数减一，然后调用递归函数。
调用完毕后，不要忘记backtracing，对应字母的个数应当恢复原样（加一）。

#### 示例代码 (cpp)
```cpp
class Solution {
    int dfsCount(vector<int>& ch_count) {
        int count = 0;
        for (int i = 0; i < ch_count.size(); ++i) {
            if (ch_count[i] == 0) {
                continue;
            }
            ++count;
            ch_count[i]--;
            count += dfsCount(ch_count);
            ch_count[i]++;
        }
        return count;
    }
public:
    int numTilePossibilities(string tiles) {
        vector<int> ch_count(26, 0);
        for (const auto tile : tiles) {
            ch_count[tile - 'A']++;
        }
        return dfsCount(ch_count);
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int numTilePossibilities(String tiles) {
        int[] count = new int[26];
        for (char c : tiles.toCharArray()) count[c - 'A']++;
        return dfs(count);
    }
    
    int dfs(int[] arr) {
        int sum = 0;
        for (int i = 0; i < 26; i++) {
            if (arr[i] == 0) continue;
            sum++;
            arr[i]--;
            sum += dfs(arr);
            arr[i]++;
        }
        return sum;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def numTilePossibilities(self, tiles: str) -> int:
        freq = collections.Counter(tiles)
        prod = 1
        for f in freq.values():
            prod *= f + 1
        res = 0
        for i in range(1, prod):
            digits = []
            for f in freq.values():
                digits.append(i % (f + 1))
                i = i // (f + 1)
            tmp = math.factorial(sum(digits))
            for d in digits:
                tmp //= math.factorial(d)
            res += tmp
        return res
```

#### 复杂度分析
时间复杂度: `O(26^N)`, `N`为`tiles`的长度
空间复杂度: `O(1)`, 栈的深度为`O(N)`

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/My9FkIGAPos)，欢迎关注！