---
title: '[Leetcode 1002] Find Common Characters'
categories:
  - leetcode
author: '猩猩管理员'
date: 2019-03-09 22:35:18
tags: ['TripAdvisor', 'Array', 'Hash Table']
keywords: ['TripAdvisor', 'Array', 'Hash Table']
description:
---
#### 原题说明
Given an array `A` of strings made only from lowercase letters, return a list of all characters that show up in all strings within the list (including duplicates).  For example, if a character occurs `3` times in all strings but not `4` times, you need to include that character three times in the final answer.

You may return the answer in any order.

**Example 1:**
{% blockquote %}
**Input:** `["bella","label","roller"]`
**Output:** `["e","l","l"]`
{% endblockquote %}

**Example 2:**
{% blockquote %}
**Input:** `["cool","lock","cook"]`
**Output:** `["c","o"]`
{% endblockquote %}

**Note:**
- `1 <= A.length <= 100`
- `1 <= A[i].length <= 100`
- `A[i][j]` is a lowercase letter

#### 解题思路
用哈希表`ansMap`记录当前可能字符以及其出现次数，也就是把字符作为`key`，频率作为`value`
用哈希表`midMap`记录当前字符串的字符以及出现次数，同样把字符作为`key`，频率作为`value`

**核心思想**:
1. 用第一个字符串初始化`ansMap`
2. 遍历剩余字符串，每次遍历前，先清空`midMap`，再遍历当前字符串，更新`midMap`；
   将`ansMap`中的`key`与`midMap`做比较：
   - 如果不在`midMap`中，直接在`ansMap`中删除这个`key`； 
   - 否则更新`ansMap`中`key`对应的`value`，取为`midMap`和`ansMap`中值较小的那个
3. 遍历`ansMap`，确定返回的`vector<string>`


#### 示例代码 (cpp)
```cpp
class Solution {
public:
    vector<string> commonChars(vector<string>& A) {
        if (A.size() == 0)
            return vector<string>();
        unordered_map<char, int> ansMap;
        unordered_map<char, int> midMap;
        vector<string> ans;
        for(auto c : A[0]) {
            ansMap[c]++;
        }
        for (auto i = 1; i < A.size() ; ++i) {
            midMap.clear();
            for (auto c : A[i]) {
                midMap[c]++;
            }
            if (ansMap.size() == 0) {
                return ans;
            }
            for (auto iter = ansMap.begin(); iter != ansMap.end(); ) {
                if (midMap.count(iter->first)) { 
                    ansMap[iter->first] = min(ansMap[iter->first], midMap[iter->first]);
                    iter++;
                }
                else {
                    iter = ansMap.erase(iter);
                }
            }
        }
        for (auto iter = ansMap.begin(); iter != ansMap.end(); iter++) {
            for (auto i = 0; i < ansMap[iter->first]; ++i) {
                ans.push_back(string(1, iter->first));
            }
        }
        return ans;
    }
};
```

#### 复杂度分析
时间复杂度: `O(n)`
空间复杂度: `O(1)`

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/ldnAFjkS22k)，欢迎关注！