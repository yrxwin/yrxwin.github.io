---
title: '[Leetcode 1023] Camelcase Matching'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-04-14 02:39:40
tags: ['Google', 'String', 'Trie']
keywords: ['Google', 'String', 'Trie']
description:
---
#### 原题说明
A query word matches a given `pattern` if we can insert lowercase letters to the pattern word so that it equals the `query`. (We may insert each character at any position, and may insert 0 characters.)

Given a list of `queries`, and a `pattern`, return an `answer` list of booleans, where `answer[i]` is true if and only if `queries[i]` matches the pattern.

 
**Example 1:**
{% blockquote %}
**Input:** `queries = ["FooBar","FooBarTest","FootBall","FrameBuffer","ForceFeedBack"], pattern = "FB"`
**Output:** `[true,false,true,true,false]`
**Explanation:** 
`"FooBar"` can be generated like this `"F" + "oo" + "B" + "ar"`.
`"FootBall"` can be generated like this `"F" + "oot" + "B" + "all"`.
`"FrameBuffer"` can be generated like this `"F" + "rame" + "B" + "uffer"`.
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** `queries = ["FooBar","FooBarTest","FootBall","FrameBuffer","ForceFeedBack"], pattern = "FoBa"`
**Output:** `[true,false,true,false,false]`
**Explanation:** 
`"FooBar"` can be generated like this `"Fo" + "o" + "Ba" + "r"`.
`"FootBall"` can be generated like this `"Fo" + "ot" + "Ba" + "ll"`.
{% endblockquote %}

**Example 3:**
{% blockquote %}
**Input:** `queries = ["FooBar","FooBarTest","FootBall","FrameBuffer","ForceFeedBack"], pattern = "FoBaT"`
**Output:** `[false,true,false,false,false]`
**Explanation:** 
`"FooBarTest"` can be generated like this `"Fo" + "o" + "Ba" + "r" + "T" + "est"`.
{% endblockquote %}

**Note:**
1. `1 <= queries.length <= 100`
2. `1 <= queries[i].length <= 100`
3. `1 <= pattern.length <= 100`
All strings consists only of lower and upper case English letters.

<!--more-->
#### 解题思路
判断每一条`query`与`pattern`是否match：
用`i`和`j`两个`index`分别指向`query`和`pattern`，遍历`query`
 1）当`query[i] == pattern[j]`时，`++j`
 2）如果不等且`query[i]`为大写字母，`return false`
遍历`query`结束后，判断`j`是否走到`pattern`末尾

#### 示例代码 (cpp)
```cpp
class Solution {
    bool isMatch(const string& query, const string& pattern) {
        int j = 0;
        for (int i = 0; i < query.size(); ++i) {
            if (j < pattern.size() && query[i] == pattern[j]) {
                ++j;
            } else if (query[i] < 'a' || query[i] > 'z') {
                return false;
            }
        }
        return j == pattern.size();
    }
public:
    vector<bool> camelMatch(vector<string>& queries, string pattern) {
        vector<bool> res;
        for (auto& query : queries) {
            res.push_back(isMatch(query, pattern));
        }
        return res;
    }
};
```

#### 示例代码 (java)
```java
class Solution {
    public List<Boolean> camelMatch(String[] queries, String pattern) {
        List<Boolean> res = new ArrayList<>();
        for (String query : queries)
            res.add(isMatch(query, pattern));
        return res;
    }

    private boolean isMatch(String query, String pattern) {
        int i = 0;
        for (char c: query.toCharArray()) {
            if (i < pattern.length() && c == pattern.charAt(i))
                i++;
            else if (c < 'a')
                return false;
        }
        return i == pattern.length();
    }
}
```

#### 示例代码 (python)
```python
class Solution(object):
    def camelMatch(self, queries, pattern):
        """
        :type queries: List[str]
        :type pattern: str
        :rtype: List[bool]
        """
        def u(s):
            return [c for c in s if c.isupper()]

        def issup(s, t):
            it = iter(t)
            return all(c in it for c in s)
        
        return [u(pattern) == u(query) and issup(pattern, query) for query in queries]
```

#### 复杂度分析
时间复杂度: `O(m * n)`, `n` is the size of `queries`, `m` is the length of each query
空间复杂度: `O(n)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/keHhIMAauP8)，欢迎关注！