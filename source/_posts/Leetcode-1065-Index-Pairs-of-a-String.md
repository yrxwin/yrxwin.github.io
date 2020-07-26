---
title: '[Leetcode 1065] Index Pairs of a String'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-07-26 19:14:42
tags: ['Amazon', 'String', 'Trie']
keywords: ['Amazon', 'String', 'Trie']
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given a&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">text</code>&nbsp;string and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">words</code>&nbsp;(a list of strings), return all index pairs&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">[i, j]</code>&nbsp;so that the substring&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">text[i]...text[j]</code>&nbsp;is in the list of&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">words</code>.&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>text = <span id="example-input-1-1">"thestoryofleetcodeandme"</span>, words = <span id="example-input-1-2">["story","fleet","leetcode"]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">[[3,7],[9,13],[10,17]]</span>
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>text = <span id="example-input-2-1">"ababa"</span>, words = <span id="example-input-2-2">["aba","ab"]</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">[[0,1],[0,2],[2,3],[2,4]]</span>
<span style="font-weight: bolder;">Explanation: </span>
Notice that matches can overlap, see "aba" is found in [0,2] and [2,4].</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><li>All strings contains only lowercase English letters.</li><li>It's guaranteed that all strings in&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">words</code>&nbsp;are different.</li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= text.length &lt;= 100</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= words.length &lt;= 20</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= words[i].length &lt;= 50</code></li><li>Return the pairs&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">[i,j]</code>&nbsp;in sorted order (i.e. sort them by their first coordinate in case of ties sort them by their second coordinate).</li></ol>
<!--more-->

#### 解题思路
这道题可以直接用string find函数来做，但是需要分析一下时间复杂度。取决于具体的函数实现，比如CPP的find函数
没有用KMP实现，所以最坏的情况复杂度是`O(M * N)`，这样带入本题，时间复杂度是`O(M * sum(len(word)))`. 其中`M`是`text`的长度，`sum(len(word))`是`words`中`word`的长度之和。
如果用字典树Trie来实现，则当`M < sum(len(word))`时，时间复杂度可以优化。
首先建立基于`words`的字典树trie，然后在`text`中以每一个位置`i`为起点向后遍历，并判断往后每一个位置`j`是否在字典树中，若在则加入要返回的结果`rets`中。

#### 示例代码 (cpp)
```cpp
struct Trie {
    vector<Trie*> children = vector<Trie*>(26, nullptr);
    bool is_find = false;
};
class Solution {
    Trie* constructTrie(const vector<string>& words) {
        Trie* trie = new Trie();
        for (const auto& word : words) {
            Trie* cur = trie;
            for (const auto ch : word) {
                if (cur->children[ch - 'a'] == nullptr) {
                    cur->children[ch - 'a'] = new Trie();
                }
                cur = cur->children[ch - 'a'];
            }
            cur->is_find = true;
        }
        return trie;
    }
public:
    vector<vector<int>> indexPairs(string text, vector<string>& words) {
        const Trie* const trie = constructTrie(words);
        vector<vector<int>> rets;
        for (int i = 0; i < text.size(); ++i) {
            const Trie* cur = trie;           
            for (int j = i; j < text.size() && cur != nullptr; ++j) {
                cur = cur->children[text[j] - 'a'];
                if (cur && cur->is_find) {
                    rets.push_back({i, j});
                }
            }
        }
        return rets;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public int[][] indexPairs(String text, String[] words) {
        /*initializing tire and put all word from words into Trie.*/
        Trie trie=new Trie();
        for(String s:words){
            Trie cur=trie;
            for(char c:s.toCharArray()){
                if(cur.children[c-'a']==null){
                    cur.children[c-'a']=new Trie();
                }
                cur=cur.children[c-'a'];
            }
            cur.end=true;       /*mark there is a word*/
        }
        
        /*if text is "ababa", check "ababa","baba","aba","ba","a" individually.*/
        int len=text.length();
        List<int[]> list=new ArrayList<>();
        for(int i=0;i<len;i++){
            Trie cur=trie;
            char cc=text.charAt(i);
            int j=i;   /*j is our moving index*/
            
            while(cur.children[cc-'a']!=null){ 
                cur=cur.children[cc-'a'];
                if(cur.end){   /*there is a word ending here, put into our list*/
                    list.add(new int[]{i,j});
                }
                j++;
                if(j==len){  /*reach the end of the text, we stop*/
                    break;
                }
                else{
                    cc=text.charAt(j);  
                }
            }
        }
        /*put all the pairs from list into array*/
        int size=list.size();
        int[][] res=new int[size][2];
        int i=0;
        for(int[] r:list){
            res[i]=r;
            i++;
        }
        return res;
    }
}
class Trie{
    Trie[] children;
    boolean end;   /*indicate whether there is a word*/
    public Trie(){
        end=false;
        children=new Trie[26];
    }
}
```

#### 示例代码 (python)
```python
class Solution:
    def indexPairs(self, text: str, words: List[str]) -> List[List[int]]:
        trie={}
        for w in words:
            cur=trie
            for c in w:
                if c not in cur.keys():
                    cur[c]={}
                cur=cur[c]
            cur['#']=True
        
        res=[]
        lens=len(text)
        for i in range(lens):
            cur=trie
            cc=text[i]
            j=i
            while cc in cur.keys():
                cur=cur[cc]
                if '#' in cur.keys():
                    res.append([i,j])
                j+=1
                if j==lens:
                    break
                else:
                    cc=text[j]
        return res
```

#### 复杂度分析
时间复杂度: `O(M^2 + sum(len(word)))`, `M`为`text`的长度
空间复杂度: `O(26^max(len(words)))`

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/-A34A6dMYEA)，欢迎关注！