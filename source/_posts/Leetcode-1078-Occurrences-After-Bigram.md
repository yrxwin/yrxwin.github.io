---
title: '[Leetcode 1078] Occurrences After Bigram'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-08-12 17:57:39
tags: ['Google', 'Hash Table']
keywords:
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Given words&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">first</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">second</code>, consider occurrences in some&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">text</code>&nbsp;of the form "<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">first second third</code>", where&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">second</code>&nbsp;comes immediately after&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">first</code>, and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">third</code>&nbsp;comes immediately after&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">second</code>.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">For each such occurrence, add "<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">third</code>" to the answer, and return the answer.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><span style="font-weight: bolder;">Example 1:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>text = <span id="example-input-1-1">"alice is a good girl she is a good student"</span>, first = <span id="example-input-1-2">"a"</span>, second = <span id="example-input-1-3">"good"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-1">["girl","student"]</span>
</pre><div style="color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example 2:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><span style="font-weight: bolder;">Input: </span>text = <span id="example-input-2-1">"we will we will rock you"</span>, first = <span id="example-input-2-2">"we"</span>, second = <span id="example-input-2-3">"will"</span>
<span style="font-weight: bolder;">Output: </span><span id="example-output-2">["we","rock"]</span>
</pre><p style="font-size: inherit; margin-bottom: 1em;">&nbsp;</p><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Note:</span></p><ol style="margin-bottom: 1em;"><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= text.length &lt;= 1000</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">text</code>&nbsp;consists of space separated words, where each word consists of lowercase English letters.</li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">1 &lt;= first.length, second.length &lt;= 10</code></li><li><code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">first</code>&nbsp;and&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">second</code>&nbsp;consist of lowercase English letters.</li></ol></div>
<!--more-->

#### 解题思路
题目的要求很简单，找出在`first`、`second`出现后紧跟着的第三个单词，而整句话是由空格和单词组成的。我们直接利用`istringstream`这个类处理串流，切分整句话，如果数组的当前元素的上一个元素等于`second`，且当前元素的上上一个元素等于`first`，就将当前元素添加进答案`vector`，最后返回记录答案的`vector`即可。

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    vector<string> findOcurrences(string text, string first, string second) {
        istringstream ss(text);
        string firstStr = "";
        string secondStr = "";
        string cur;
        vector<string> ans;
        while (ss >> cur) {
            if (firstStr == first && secondStr == second) {
                ans.emplace_back(cur);
            }
            firstStr = secondStr;
            secondStr = cur;
        }
        return ans;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public String[] findOcurrences(String text, String first, String second) {
        String a[]=text.split(" ");
       List<String> res=new ArrayList();int k=0;
        for(int i=0;i<a.length-2;)
        {
            if(a[i].equals(first) && a[i+1].equals(second))
            {
                res.add(a[i+2]);
               i=i+2;
            }
            else
                i++;
        }
        String temp[]=new String[res.size()];
        int i=0;
        for(String t: res)
        {
            temp[i]=t;i++;
        }
        return temp;
    }
}

```

#### 示例代码 (python)
```python
class Solution:
    def findOcurrences(self, text: str, first: str, second: str) -> List[str]:
        third = []
        sen = list(text.split())
        for i in range(1, len(sen)-1):
            if sen[i-1] == first and sen[i] == second:
                third.append(sen[i+1])
        return third
```

#### 复杂度分析
时间复杂度: O(n)
空间复杂度: O(n)

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/Ehu5LK_7Nu0)，欢迎关注！