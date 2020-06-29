---
title: '[Leetcode 1061] Lexicographically Smallest Equivalent String'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-06-29 00:25:36
tags: ['Depth-first Search', 'Union Find']
keywords: ['Depth-first Search', 'Union Find']
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given strings&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">B</code>&nbsp;of the same length, we say A[i] and B[i] are equivalent characters. For example, if&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A = "abc"</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">B = "cde"</code>, then we have&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">'a' == 'c', 'b' == 'd', 'c' == 'e'</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Equivalent characters follow the usual rules of any equivalence relation:</p><ul style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li>Reflexivity: 'a' == 'a'</li><li>Symmetry: 'a' == 'b' implies 'b' == 'a'</li><li>Transitivity: 'a' == 'b' and 'b' == 'c' implies 'a' == 'c'</li></ul><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">For example, given the equivalency information from&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">B</code>&nbsp;above,&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S = "eed"</code>,&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">"acd"</code>, and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">"aab"</code>&nbsp;are equivalent strings, and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">"aab"</code>&nbsp;is the lexicographically smallest equivalent string of&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Return the lexicographically smallest equivalent string of&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S</code>&nbsp;by using the equivalency information from&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">B</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>A = <span id="example-input-1-1">"parker"</span>, B = <span id="example-input-1-2">"morris"</span>, S = <span id="example-input-1-3">"parser"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">"makkek"</span>
<span style="font-weight: bolder;">Explanation:</span> Based on the equivalency information in <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">A</code> and <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">B</code>, we can group their characters as <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">[m,p]</code>, <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">[a,o]</code>, <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">[k,r,s]</code>, <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">[e,i]</code>. The characters in each group are equivalent and sorted in lexicographical order. So the answer is <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">"makkek"</code>.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>A = <span id="example-input-2-1">"hello"</span>, B = <span id="example-input-2-2">"world"</span>, S = <span id="example-input-2-3">"hold"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">"hdld"</span>
<span style="font-weight: bolder;">Explanation: </span> Based on the equivalency information in <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">A</code> and <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">B</code>, we can group their characters as <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">[h,w]</code>, <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">[d,e,o]</code>, <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">[l,r]</code>. So only the second letter <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">'o'</code> in <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">S</code> is changed to <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">'d'</code>, the answer is <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">"hdld"</code>.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 3:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>A = <span id="example-input-3-1">"leetcode"</span>, B = <span id="example-input-3-2">"programs"</span>, S = <span id="example-input-3-3">"sourcecode"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-3">"aauaaaaada"</span>
<span style="font-weight: bolder;">Explanation: </span> We group the equivalent characters in <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">A</code> and <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">B</code> as <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">[a,o,e,r,s,c]</code>, <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">[l,p]</code>, <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">[g,t]</code> and <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">[d,m]</code>, thus all letters in <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">S</code> except <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">'u'</code> and <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">'d'</code> are transformed to <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">'a'</code>, the answer is <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">"aauaaaaada"</code>.</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li>String&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A</code>,&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">B</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S</code>&nbsp;consist of only lowercase English letters from&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">'a'</code>&nbsp;-&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">'z'</code>.</li><li>The lengths of string&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A</code>,&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">B</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S</code>&nbsp;are between&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1000</code>.</li><li>String&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">A</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">B</code>&nbsp;are of the same length.</li></ol>
<!--more-->

#### 解题思路
这道题很多网上解答是用了Union find，实际上并不是最好的方法。
Union find比较适合union与find操作交错的情况，比如Number of Islands II.
但是这里的话，如果使用Union find，需要先进行一系列union操作，然后进行一系列find操作，时间复杂度是`O((M + N)log*(M))`，近似于`O(M + N)`. 但是实际上直接使用DFS或者BFS遍历，也可以达到`O(M + N)`的时间复杂度：
1. 首先遍历`A`和`B`，创建一个字母间关联的无向图`mapping`
2. 遍历`S`，对于`S`中的每一个字母`s`，在无向图中进行一次DFS（BFS也可以），找寻关联字母中最小的字母，同时用一个`unordered_set visited`记录遍历到的点。
3. `visited`中的点都是与当前字母`s`关联的，因此对应的最小字母是一样的，用一个`unordered_map memo`来记录`visited`中的点与最小字母的对应关系，这样下次遍历到这些点，就不用再做dfs了，直接从`memo`中查到对应的最小字母即可。

假设`A`和`B`的长度是`M`，`S`的长度是`N`，由于`mapping`中每一个字母（节点）和每一条边遍历了一遍，这是一个`O(M)`的时间复杂度，创建`mapping`是`O(M)`的时间复杂度，遍历`S`的时间复杂度为`O(N)`
所以总的时间复杂度是`O(2M + N)`也是近似于`O(M + N)`

#### 示例代码 (cpp)
```cpp
class Solution {
    char dfs(unordered_map<char, vector<char>>& mapping, char input, unordered_set<char>& visited) {
        if (visited.count(input) > 0) {
            return input;
        }
        visited.insert(input);
        char ret = input;
        for (const auto ch : mapping[input]) {
            ret = min(ret, dfs(mapping, ch, visited));
        }
        return ret;
    }
public:
    string smallestEquivalentString(string A, string B, string S) {
        unordered_map<char, vector<char>> mapping;
        for (int i = 0; i < A.size(); ++i) {
            mapping[A[i]].push_back(B[i]);
            mapping[B[i]].push_back(A[i]);
        }
        string ret;
        unordered_map<char, char> memo;
        for (const auto s : S) {
            if (memo.count(s) > 0) {
                ret += memo[s];
                continue;
            }
            unordered_set<char> visited;
            const auto min_char = dfs(mapping, s, visited);
            for (const auto ch : visited) {
                memo[ch] = min_char;
            }
            ret += min_char;
        }
        return ret;
    }
};
```

#### 示例代码 (java)
```java
// Union Find
class Solution {
    public String smallestEquivalentString(String A, String B, String S) {
        int[] graph = new int[26];
        for(int i = 0; i < 26; i++) {
            graph[i] = i;
        }
        for(int i = 0; i < A.length(); i++) {
            int a = A.charAt(i) - 'a';
            int b = B.charAt(i) - 'a';
            int end1 = find(graph, b);
            int end2 = find(graph, a);
            if(end1 < end2) {
                graph[end2] = end1;
            } else {
                graph[end1] = end2;
            }
        }
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < S.length(); i++) {
            char c = S.charAt(i);
            sb.append((char)('a' + find(graph, c - 'a')));
        }
        return sb.toString();
    }
    
    private int find(int[] graph, int idx) {
        while(graph[idx] != idx) {
            idx = graph[idx];
        }
        return idx;
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def smallestEquivalentString(self, A: str, B: str, S: str) -> str:
        neighbors = collections.defaultdict(set)
        for a, b in zip(A, B):
            neighbors[a].add(b)
            neighbors[b].add(a)

        memo = {}

        def bfs(ch):
            if ch in memo: return memo[ch]
            res = ch
            seen = set()
            queue = {ch}

            while queue:
                c = queue.pop()
                if c in seen: continue
                seen.add(c)
                res = min(res, c)
                queue |= neighbors[c]

            for v in seen:
                memo[v] = res

            return res
        return ''.join(bfs(c) for c  in S)
```

#### 复杂度分析
时间复杂度: `O(M + N)`, 假设`A`和`B`的长度是`M`，`S`的长度是`N`
空间复杂度: `O(M)`, 即`mapping`占用的空间

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/if1m4y5ZnVQ)，欢迎关注！