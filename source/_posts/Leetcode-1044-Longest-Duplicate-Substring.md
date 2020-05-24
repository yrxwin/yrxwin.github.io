---
title: '[Leetcode 1044] Longest Duplicate Substring'
categories:
  - leetcode
author: '大猩猩'
date: 2020-05-23 22:58:56
tags: ['Hash Table','Binary Search']
keywords:
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given a string&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S</code>, consider all&nbsp;<em>duplicated substrings</em>: (contiguous) substrings of S that occur 2 or more times.&nbsp; (The occurrences&nbsp;may overlap.)</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Return&nbsp;<span style="font-weight: bolder;">any</span>&nbsp;duplicated&nbsp;substring that has the longest possible length.&nbsp; (If&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S</code>&nbsp;does not have a duplicated substring, the answer is&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">""</code>.)</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-1-1">"banana"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">"ana"</span>
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span><span id="example-input-2-1">"abcd"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">""</span>
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">2 &lt;= S.length &lt;= 10^5</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">S</code>&nbsp;consists of lowercase English letters.</li></ol>
<!--more-->

#### 解题思路
题目要求给出一个字符串中，重复出现至少`2`次的最长子串。

首先，我们考虑如果采用暴力破解，若字符串长度是`n`，那么从`n`到`1`依次从大到小计算，第一次遇到重复出现两次的子串，就是我们的答案。

但是，暴力算法显然不是最优解，也不能AC。

显然，最长子串的长度最大至多是`n-1`，最小是`0`。也就提醒我们可以按照这个空间进行[`binary search`](/tags/Binary-Search/)。

然后，在每一次二分搜索中，我们判断在当前长度下有没有相同的子串重复出现至少2次。如果存在，那向上搜索；如果不存在，那向下搜索，直到找到答案。这里，用哈希表记录下每一次出现过的子串。但是，如果单纯用子串作为`key`,我们会发现`memory exceed`。显然，我们需要对字符串的存储做个优化。但如何优化一开始我也没想出来。提示中告诉我们，`To check whether an answer of length K exists, we can use Rabin-Karp 's algorithm.`。什么是`Rahin-karp`算法呢？根据`wiki` [https://en.wikipedia.org/wiki/Rabin%E2%80%93Karp_algorithm](https://en.wikipedia.org/wiki/Rabin%E2%80%93Karp_algorithm) 给我们的解释，它就是一种优化快速查询文本中出现给定子串的的方法。

简单来说，对于一个字符串，用一个哈希函数求出对应的哈希值。当两个哈希值不同时，这两个字符串一定不同，而当两个哈希值相同时，这两个字符串有大概率相同。因为查找子串的过程，可以高效利用之前求出的哈希值，不用太多的重复计算(`wiki`中称为`rolling hash function`)，因此能快速计算哈希值并且高效储存。

具体到哈希值的计算，我们举例说明：
首先需要确定一个`base`，也就是进制，这里我们选择`26`。然后我们选择一个`modulus`，比如`31`。按题目中给出的`banana`，我们计算长度是`3`的各个子串的哈希值。

`ban`: (1 \* 26 \* 26 + 0 \* 26 + 13) % 31 = 7
`ana`: (0 \* 26 \* 26 + 13 \* 26 + 0) % 31 = 28
`nan`: (13 \* 26 \* 26 + 0 \* 26 + 13) % 31 = 28
`ana`: (0 \* 26 \* 26 + 13 \* 26 + 0) % 31 = 28

我们可以观察到，`ana`与`nan`拥有相同的哈希值，但是它们确实是不同的字符串。因为这种哈希值的计算过程中，有重复计算的部分，所以我们可以`rolling`这部分的内容，优化时间。同时，哈希值的空间大小也是明显优于那些超长字符串的。

需要说明的是，这个方法会有`false positive`的可能，因为`hash function`有`collision`的产生。但当`modulus`很大时，概率是极低的。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    string longestDupSubstring(string S) {
        int n = S.length();
        int left = 1;
        int right = n;
        while(left<=right)
        {
            int len = left + (right-left) / 2;
            if(search(len, S, n) != -1)
                left = len + 1;
            else
                right = len - 1;
        }
        int start = search(left - 1, S, n);
        return S.substr(start, left - 1);
    }
    int search(int len, string s, int n)
    {
        long modulus = (long)pow(2, 34);
        long value = 0;
        unordered_set<long> sets;
        for(int i = 0; i < len; i++) {
            value = value * 26 + s[i] - 'a';
            value = value % modulus;
        }

        sets.insert(value);

        // prepass, cache the remainder
        long aL = 1;
        for (int i = 0; i < len; ++i) {
            aL = (aL * 26) % modulus;
        }
        
        for(int i = 1;i <= n-len; i++) {
            value = value * 26 - (s[i-1] - 'a') * aL + modulus + s[i+len-1] - 'a';
            value = value % modulus;
            if(sets.count(value)) {
                return i;
            }
            else {
                sets.insert(value);
            }
        }
        return -1;
    }
};

```

#### 示例代码 (java)
```java
class Solution {
    private static final long q = (1 << 31) - 1;
    private static final long R = 256;
        
    public String longestDupSubstring(String S) {      
        int left = 2;
        int right = S.length() - 1;
        int start = 0;
        int maxLen = 0;
        
        while (left <= right) {
            int len = left + (right - left) / 2;
            boolean found = false;
            
            Map<Long, List<Integer>> map = new HashMap<>();
            long hash = hash(S, len);
            map.put(hash, new ArrayList<>());
            map.get(hash).add(0);
            long RM = 1l;
            for (int i = 1; i < len; i++) RM = (R * RM) % q;
            
            loop:
            for (int i = 1; i + len <= S.length(); i++) {
                hash = (hash + q - RM * S.charAt(i - 1) % q) % q;
                hash = (hash * R + S.charAt(i + len - 1)) % q;
                if (!map.containsKey(hash)) {
                    map.put(hash, new ArrayList<>());
                } else {
                    for (int j : map.get(hash)) {
                        if (compare(S, i, j, len)) {
                            found = true;
                            start = i;
                            maxLen = len;
                            break loop;
                        }
                    }
                }
                map.get(hash).add(i);
            }
            if (found) left = len + 1;
            else right = len - 1;
        }
        
        return S.substring(start, start + maxLen);
    }
    
    private long hash(String S, int len) { 
        long h = 0;
        for (int j = 0; j < len; j++) h = (R * h + S.charAt(j)) % q;
        return h;
    }
    
    private boolean compare(String S, int i, int j, int len) {
        for (int count = 0; count < len; count++) {
            if (S.charAt(i++) != S.charAt(j++)) return false ; 
        }
        return true ; 
    }
}
```

#### 示例代码 (python)
```python
class Solution(object):
    def longestDupSubstring(self, S):
        A = [ord(c) - ord('a') for c in S]
        mod = 2**34

        def test(L):
            p = pow(26, L, mod)
            cur = reduce(lambda x, y: (x * 26 + y) % mod, A[:L], 0)
            seen = {cur}
            for i in xrange(L, len(S)):
                cur = (cur * 26 + A[i] - A[i - L] * p) % mod
                if cur in seen: return i - L + 1
                seen.add(cur)
        res, lo, hi = 0, 0, len(S)
        while lo < hi:
            mi = (lo + hi + 1) / 2
            pos = test(mi)
            if pos:
                lo = mi
                res = pos
            else:
                hi = mi - 1
        return S[res:res + lo]
```

#### 复杂度分析
时间复杂度: O(NlogN)，`N` 是字符串的长度。
空间复杂度: O(N)，`N` 是字符串的长度。

#### 归纳总结
`Rahin-karp`的算法，不知道的人在做题时不会想到。同样，也不大可能在面试的时候自己想出来。非常正常。但我们了解后，还是比较简单的。同时，用哈希的方法转化的思想值得我们注意。
我们在**Youtube**上更新了[视频讲解](https://youtu.be/TC4lW8XDYbg)，欢迎关注！