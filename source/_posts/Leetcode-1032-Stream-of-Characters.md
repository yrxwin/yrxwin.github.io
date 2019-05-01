---
title: '[Leetcode 1032] Stream of Characters'
categories:
  - leetcode
author: '大猩猩'
date: 2019-04-27 23:04:03
tags: ['Google','Trie']
keywords: ['Google','Trie']
description: 
---
#### 原题说明
Implement the StreamChecker class as follows:

  *StreamChecker(words):* Constructor, init the data structure with the given words.
  *query(letter):* returns true if and only if for some k >= 1, the last k characters queried (in order from oldest to newest, including this letter just queried) spell one of the words in the given list.

**Example**
{% blockquote %}
StreamChecker streamChecker = new StreamChecker(["cd","f","kl"]); // init the dictionary.
streamChecker.query('a');          // return false
streamChecker.query('b');          // return false
streamChecker.query('c');          // return false
streamChecker.query('d');          // return true, because 'cd' is in the wordlist
streamChecker.query('e');          // return false
streamChecker.query('f');          // return true, because 'f' is in the wordlist
streamChecker.query('g');          // return false
streamChecker.query('h');          // return false
streamChecker.query('i');          // return false
streamChecker.query('j');          // return false
streamChecker.query('k');          // return false
streamChecker.query('l');          // return true, because 'kl' is in the wordlist
{% endblockquote %}

**Note**
1. `1 <= words.length <= 2000`
2. `1 <= words[i].length <= 2000`
3. Words will only consist of lowercase English letters.
4. Queries will only consist of lowercase English letters.
5. The number of queries is at most 40000.
<!--more-->

#### 解题思路
题目要求输入一个字符串数组作为字典， 然后不断查询字符，如果最近的`k`个字符构成一个完整的字典单词的话，返回`true`，否则返回`false`。

这个题目可以使用字典树(`Trie`)求解。 对每个字符查询，当返回`true`时，一定是一个完整的单词。值得注意的技巧是，反向查询可以节省很多开销。因为正向查询的话要保存很多上次访问到的节点，因为开始的地方可能会很多，所以这个`Trie`可以反过来建， 这样每次查询的时候都可以从最后面开始查询起。

建`Trie`的过程是对每个单词逆序插入`Trie`， 从最后一个字符开始到第一个字符插入建立`Trie`。
查询的时候，因为接受的是一个`stream`，我们需要的`stream`的长度不应该超过`Trie`的最大深度。这样保证了我们的空间复杂度不会过大。

每次查询从`stream`的最后一个字符开始向前查询，查到一个完整的单词就返回`true`，否则就返回`false`。

#### 示例代码 (cpp)
```cpp
class TrieNode {
public:
    bool isWord;
    vector<TrieNode*> next;
    TrieNode(): isWord(false), next(vector<TrieNode*>(26, nullptr)) {}
};


class Trie {
public:
    TrieNode* root;
    
    Trie() {
        root = new TrieNode();
    }
    
    void insert(string& word) {
        TrieNode* cur = root;
        for (int i = word.size() - 1; i >= 0; --i) {
            int pos = word[i] - 'a';
            if (cur -> next[pos] == nullptr) {
                cur -> next[pos] = new TrieNode();
            }
            cur = cur -> next[pos]; 
        }
        cur -> isWord = true;
    }
  
    bool findWord(string& word) {
        TrieNode* cur = root;
        for (int i = word.size() - 1; i >= 0; --i) {
            int pos = word[i] - 'a';
            cur = cur->next[pos];
            if (cur == nullptr) {
                return false;
            }
            if (cur -> isWord) {
                return true;
            }
        }
        return false;
    }
    
};

class StreamChecker {
private:
    string stream = "";
    Trie trie = Trie();
    size_t maxLen = 0;
public:
    StreamChecker(vector<string>& words) {
        for (auto word : words) {
            trie.insert(word);
            maxLen = max(maxLen, word.size());
        }
    }
    
    bool query(char letter) {
        stream += letter;
        if (stream.size() > maxLen) {
            stream.erase(stream.begin());
        }
        return trie.findWord(stream);
    }
};

/**
 * Your StreamChecker object will be instantiated and called as such:
 * StreamChecker* obj = new StreamChecker(words);
 * bool param_1 = obj->query(letter);
 */
```

#### 示例代码 (java)
```java
class StreamChecker {
    
    class TrieNode {
        boolean isWord;
        TrieNode[] next = new TrieNode[26];
    }

    TrieNode root = new TrieNode();
    StringBuilder sb = new StringBuilder();

    public StreamChecker(String[] words) {
        createTrie(words);
    }

    public boolean query(char letter) {
        sb.append(letter);
        TrieNode node = root;
        for (int i = sb.length() - 1; i >= 0 && node != null; i--) {
            char c = sb.charAt(i);
            node = node.next[c - 'a'];
            if (node != null && node.isWord) {
                return true;
            }
        }
        return false;
    }

    private void createTrie(String[] words) {
        for (String s : words) {
            TrieNode node = root;
            int len = s.length();
            for (int i = len - 1; i >= 0; i--) {
                char c = s.charAt(i);
                if (node.next[c - 'a'] == null) {
                    node.next[c - 'a'] = new TrieNode();
                }
                node = node.next[c - 'a'];
            }
            node.isWord = true;
        }
    }
}
```

#### 示例代码 (python)
```python
from collections import deque
class StreamChecker(object):

    def __init__(self, words):
        """
        :type words: List[str]
        """
        self.n = 0
        self.root = self.createTrie(words)
        self.window = deque()
        
    def createTrie(self, words):
        root = {}
        for word in words:
            if len(word) > self.n:
                self.n = len(word)
            node = root
            for char in word[::-1]:
                if char not in node:
                    node[char] = {}
                node = node[char]
            node['#'] = True
        return root

    def search(self):
        
        word = self.window
        root = self.root
        for i in range(len(word)-1, -1, -1):
            if '#' in root:
                return True
            if word[i] in root:
                root = root[word[i]]
            else:
                return False
        
        return True if '#' in root else False 
        
    
    def query(self, letter):
        """
        :type letter: str
        :rtype: bool
        """
        self.window.append(letter)
        if len(self.window) > self.n:
            self.window.popleft()
        return self.search()

# Your StreamChecker object will be instantiated and called as such:
# obj = StreamChecker(words)
# param_1 = obj.query(letter)
```

#### 复杂度分析
时间复杂度: O(d \* (# of query))
空间复杂度: O(d \* (# of dictionary))
d是dictionary中最长单词的长度。

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/VaRsfAZwEqI)，欢迎关注！