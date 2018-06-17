---
title: '[Leetcode 3] Longest Substring Without Repeating Characters'
categories:
  - leetcode
author: '猩猩管理员'
date: 2018-06-17 00:32:02
tags: [Amazon, Bloomberg, Yelp, Adobe, Hash Table, Two Pointers, String]
keywords: [Two Pointers, Hash Table, String]
description:
---
#### 原题说明
Given a string, find the length of the **longest substring** without repeating characters.

**Examples**:
{% blockquote %}
Given `"abcabcbb"`, the answer is `"abc"`, which the length is 3.

Given `"bbbbb"`, the answer is `"b"`, with the length of 1.

Given `"pwwkew"`, the answer is `"wke"`, with the length of 3. 
{% endblockquote %}**Note** 
The answer must be a substring, `"pwke"` is a subsequence and not a substring.



#### 解题思路
这道题需要用一个`Hash Table`来记录当前字符上一次出现的`index`, 用一个变量`left`记录以当前字符结尾的符合题目条件的`substring`的左侧`index`. 注意`left`初始值为`-1`, 表示以当前字符结尾的符合题目条件的`substring`的起始位置等于`s`的起始位置 (`index`为`0`).

#### 示例代码 (cpp)
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> mapping;
        int ret = 0, left = -1;
        for (int i = 0; i < s.size(); ++i) {
            if (mapping.count(s[i])) {
                left = max(left, mapping[s[i]]);
            }
            mapping[s[i]] = i;
            ret = max(ret, i - left);
        }
        return ret;
    }
};
```

#### 复杂度分析
时间复杂度: `O(n)` 其中`n`为`s`的长度
空间复杂度: `O(1)` 因为不同字符的数量有限(一般来说为256), 所以`mapping`的大小是恒定的

#### 归纳总结
这道题中的`mapping`可以用`vector<int>`代替`unordered_map`, 但是作者倾向于使用后者, 因为更有普遍性, 不容易与面试官产生分歧(比如面试官默认`s`只有26个字母, 那么`hard code`字符数为`256`就容易产生分歧), 即使一定要`hard code`字符数, 也需要和面试官说明.

这道题的思路产生过程并不直接, 面试中如果一下子想不清楚, 建议可以带一个例子, 一步步手动推导结果, 从中或许能够找到一些灵感, 至少也可以让面试官看到思考过程.