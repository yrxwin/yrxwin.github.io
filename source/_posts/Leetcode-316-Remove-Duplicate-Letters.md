---
title: '[Leetcode 316] Remove Duplicate Letters'
categories:
  - leetcode
date: 2018-03-30 00:28:51
tags:
    - Google
    - Stack
    - Greedy
author: 猩猩管理员, 中猩猩
    
---
#### 原题说明
Given a string which contains only lowercase letters, remove duplicate letters so that every letter appear once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

Example:
Given `"bcabc"`
Return `"abc"`

Given `"cbacdcbc"`
Return `"acdb"`

#### 解题步骤
1.  建立哈希表（或者数组)`mapping`来统计字符串中每一个字母出现的频率
2.  建立哈希表（或者数组)`visited`来记录已经插入`ret` (**ret**urn string) 的字母
3.  将 `ret` 当作 **stack**，用 **Greedy** (贪心法）遍历字符串  `s`  ：
	-  若当前字符已经在 `visited` 中了，直接 continue
	-	当前字符 `ch`  与  `ret`  字符串的末尾元素（栈顶）比较，若  `ch` 靠前，并且 `mapping` 中栈顶元素大于0 (即之后遍历中还会出现栈顶元素)，则 pop `ret`末尾元素，如此反复，直到  `ret`  末尾元素靠前，或者 `ret` 为空
	-   在  `ret`  中插入当前字符 `ch`
	-   插入与 pop 过程都不要忘记更新 `visited`

#### 示例代码(CPP)

```cpp
class Solution {
public:
    string removeDuplicateLetters(string s) {
        unordered_map<char, int> mapping;
        unordered_set<char> visited;
        for (auto& ch : s) {
            mapping[ch]++;
        }
        string ret;
        for (auto& ch : s) {
            mapping[ch]--;
            if (visited.count(ch)) {
                continue;
            }
            while (ret.size() && ret.back() > ch && mapping[ret.back()] > 0) {
                visited.erase(ret.back());
                ret.pop_back();
            }
            ret += ch;
            visited.insert(ch);
        }
        return ret;
    }
};
```

#### 示例代码(PYTHON)

```python
from collections import Counter
class Solution(object):
    def removeDuplicateLetters(self, s):
        """
        :type s: str
        :rtype: str
        """
        map = Counter()
        stack = list()
        visited = set()
        for c in s:
            map[c] += 1
        for c in s:
            map[c] -= 1;
            if c in visited: continue
            else: visited.add(c)
            while(len(stack) > 0 and c < stack[-1] and map[stack[-1]] > 0):
                visited.remove(stack[-1])
                stack.pop()
            stack.append(c)
            visited.add(c)
        return ''.join(stack)
```
#### 复杂度分析
因为每个字符插入和pop出ret都是最多一次，所以：

- 时间复杂度：O(n)
- 空间复杂度：O(n)

#### 总结归纳：
运用Stack加贪心法的题目有很多，这类问题的做法是遍历输入数组，当前元素与栈顶元素比较，如果当前元素更优（不同题目条件不同，比如本题对应当前元素较小）则pop栈顶元素，直到栈顶元素更优为止，而后插入当前元素。

最近会着重介绍这类题目，之后会将链接贴在这里，尽请期待，吃香蕉去了：）