---
title: '[Leetcode 809] Expressive Words'
categories:
  - leetcode
author: '猩猩管理员'
date: 2018-04-03 00:36:27
tags: [Google, String]
keywords: [Expressive words, String, two pointers]
description:
---
#### 原题说明
Sometimes people repeat letters to represent extra feeling, such as `"hello" -> "heeellooo"`, `"hi" -> "hiiii"`.  Here, we have groups, of adjacent letters that are all the same character, and adjacent characters to the group are different.  A group is extended if that group is length 3 or more, so "e" and "o" would be extended in the first example, and "i" would be extended in the second example.  As another example, the groups of "abbcccaaaa" would be "a", "bb", "ccc", and "aaaa"; and "ccc" and "aaaa" are the extended groups of that string.

For some given string S, a query word is stretchy if it can be made to be equal to S by extending some groups.  Formally, we are allowed to repeatedly choose a group (as defined above) of characters c, and add some number of the same character c to it so that the length of the group is 3 or more.  Note that we cannot extend a group of size one like "h" to a group of size two like "hh" - all extensions must leave the group extended - ie., at least 3 characters long.

Given a list of query words, return the number of words that are stretchy. 

{% blockquote %}
**Example**:
**Input**: 
S = "heeellooo"
words = ["hello", "hi", "helo"]
**Output**: 1
**Explanation**: 
We can extend "e" and "o" in the word "hello" to get "heeellooo".
We can't extend "helo" to get "heeellooo" because the group "ll" is not extended.
{% endblockquote %}

Notes:

- `0 <= len(S) <= 100`.
- `0 <= len(words) <= 100`.
- `0 <= len(words[i]) <= 100`.
- `S` and all `words` in words consist only of lowercase letters

#### 解题思路
这道题主要需要建立`isMatch()`方法判断`original word` (`o`)是否能够表述成`stretchy word` (`s`)
指针`i`和`j`分别指向`s`和`o`,需要判断如下条件:
- 如果当前的`s[i] != o[j]`, 直接返回`false`
- 统计当前连续相同的字符分别用`cntO`和`cntS`表示
- 如果`cntO == cntS`,说明是严格匹配,当然可以继续
- 如果`cntO < cntS && cntS >= 3`, 说明`S`extend了当前的字符,也可以继续匹配

需要注意的是,`"baac"`(original word)和`"baaac"`(strechy word)是可以匹配的, 但是`"baaaac"`(original word)和`"baaac"`(stretchy word)就不可以了, 也就是说原字符串中相同连续字符(例子中的字符`'a'`)长度一定要小于Stretchy word中对应的相同连续字符(`'a'`)长度才可能匹配, 这一点原题没有说的特别清楚, 面试的时候需要和面试官clarify清楚.

#### 示例代码 (cpp)
```cpp
class Solution {
    // s means strechy word, o means original word
    bool isMatch(const string& s, const string& o) {
        int i = 0, j = 0;
        while (i < s.size() && j < o.size()) {
            if (s[i++] != o[j++]) {
                return false;
            }
            // cntO means number of consecutive chars in O starting from i - 1
            // cntS means number of consecutive chars in S stargin from j - 1
            int cntO = 1, cntS = 1;
            while (i < s.size() && s[i] == s[i - 1]) {
                ++i;
                ++cntS;
            }
            while (j < o.size() && o[j] == o[j - 1]) {
                ++j;
                ++cntO;
            }
            if (cntS == cntO || (cntS >= 3 && cntS > cntO)) {
                continue;
            }
            return false;
        }
        return (i == s.size() && j == o.size());
    }
public:
    int expressiveWords(string S, vector<string>& words) {
        int ret = 0;
        for (auto& word : words) {
            if (isMatch(S, word)) {
                ++ret;
            }
        }
        return ret;
    }
};
```

#### 示例代码 (python)
```python
class Solution(object):
    def get_char_len_next_nondup_idx(self, word, curr_idx):
        """
        Get current character, continous length of this charactor
        and next character index
        """
        length = 1
        for idx in range(curr_idx + 1, len(word)):
            if word[idx] != word[curr_idx]:
                return word[curr_idx], length, idx
            length += 1
        return word[curr_idx], length, len(word)
    
    def check(self, S, word):
        sid = 0
        wid = 0
        while(sid < len(S) and wid < len(word)):
            curr_s_char, curr_s_len, sid = self.get_char_len_next_nondup_idx(S, sid)
            curr_w_char, curr_w_len, wid = self.get_char_len_next_nondup_idx(word, wid)
            if curr_s_char != curr_w_char:
                return 0
            if curr_s_len < curr_w_len:
                return 0
            if curr_s_len == 2 and curr_w_len == 1:
                return 0
        if sid == len(S) and wid == len(word):
            return 1
        return 0
                    
    def expressiveWords(self, S, words):
        """
        :type S: str
        :type words: List[str]
        :rtype: int
        """
        ret = 0
        for word in words:
            ret += self.check(S, word)
        return ret
```

#### 复杂度分析
时间复杂度: `O(len * (m + n))` 其中`len`为`words.size()`, `m`为`S.size()`, `n`为`word`中字符串的平均长度
空间复杂度: `O(1)` 

#### 归纳总结
这是一道经典的字符串题目,题目本身并不算很难,重要的是要理解清楚题意.
