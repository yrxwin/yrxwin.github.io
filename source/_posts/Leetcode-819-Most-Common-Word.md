---
title: '[Leetcode 819] Most Common Word'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-06-04 22:10:38
tags: [Amazon, String]
keywords: [Amazon, String, Most Common Word]
description:
---
#### 原题说明
Given a paragraph and a list of banned words, return the most frequent word that is not in the list of banned words.  It is guaranteed there is at least one word that isn't banned, and that the answer is unique.

Words in the list of banned words are given in lowercase, and free of punctuation.  Words in the paragraph are not case sensitive.  The answer is in lowercase.

{% blockquote %}
**Example**:
**Input**: 
paragraph = "Bob hit a ball, the hit BALL flew far after it was hit."
banned = ["hit"]
**Output**: "ball"
**Explanation**: 
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"), 
and that "hit" isn't the answer even though it occurs more because it is banned.
{% endblockquote %}
Note:
- `1 <= paragraph.length <= 1000`.
- `1 <= banned.length <= 100`.
- `1 <= banned[i].length <= 10`.
- The answer is unique, and written in lowercase (even if its occurrences in paragraph may have uppercase symbols, and even if it is a proper noun.)
- `paragraph` only consists of letters, spaces, or the punctuation symbols !?',;.
- Different words in `paragraph` are always separated by a space.
- There are no hyphens or hyphenated words.
- Words only consist of letters, never apostrophes or other punctuation symbols.
<!-- more -->

#### 解题思路
这道题可以通过`hash table`来建立每个单词与其出现频率的对应关系, 在遍历`paragraph`的时候统计单词出现的频率, 并更新当前的最高频单词.
由于题目相对简单, 面试的时候需要在较短的时间内想到建立怎样的对应关系, 存储结构应该如何设计 (比如用`map`还是`unordered_map`, `key`和`value`分别是什么, 两者能不能倒过来等等)
另外对于使用`cpp`的同学来说, 熟练掌握`istringstream`和`getline`这些基础的I/O interface还是比较加分的.

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    string mostCommonWord(string paragraph, vector<string>& banned) {
        istringstream iss(paragraph);
        unordered_set<string> banSet(banned.begin(), banned.end());
        unordered_map<string, int> mapping;
        string cur, ret;
        int curMax = 0;
        while (getline(iss, cur, ' ')) {
            string formatStr;
            for (int i = 0; i < cur.size(); ++i) {
                char ch = tolower(cur[i]);
                if (ch >= 'a' && ch <= 'z') {
                    formatStr += ch;
                }
            }
            mapping[formatStr]++;
            if (mapping[formatStr] > curMax && !banSet.count(formatStr)) {
                curMax = mapping[formatStr];
                ret = formatStr;
            }
        }
        return ret;
    }
};
```

#### 示例代码 (python)
```python
class Solution(object):
    def mostCommonWord(self, paragraph, banned):
        """
        :type paragraph: str
        :type banned: List[str]
        :rtype: str
        """
        words_dict = collections.Counter()
        top_word = None
        top_freq = 0
        words = re.split("[ !?',;.]+", paragraph)
        for word in words:
            if word.lower() not in banned:
                words_dict[word.lower()] += 1
                if words_dict[word.lower()] > top_freq:
                    top_word = word.lower()
                    top_freq = words_dict[word.lower()]
        
        return top_word
```

#### 复杂度分析
时间复杂度: `O(n)` (n为`paragraph`包含的单词数)
空间复杂度: `O(m + n)` (m为`banned`长度)

#### 归纳总结
像这样一道比较基础的算法设计题, 如果真正面试的时候遇到, 尽量不要一上来就写答案, 可以在白板上列举一下可能的数据结构及做法, 说明为什么最后选择这样做(比如只有这样才行得通或者效率更高). 通过这样的分析可以让面试官看到真实清晰的思路.
