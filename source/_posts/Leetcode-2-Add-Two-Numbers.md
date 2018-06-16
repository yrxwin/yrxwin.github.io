---
title: '[Leetcode 2] Add Two Numbers'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2018-06-16 15:56:56
tags: [Microsoft, Amazon, Bloomberg, Airbnb, Adobe, Linked List, Math]
keywords: [Add Two Numbers, Microsoft, Amazon, Linked List, Math]
description:
---
#### 原题说明
You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example**:
{% blockquote %}
Input: `(2 -> 4 -> 3) + (5 -> 6 -> 4)`
Output: `7 -> 0 -> 8`
Explanation: `342 + 465 = 807`.
{% endblockquote %}

#### 解题思路
这道题考察对链表的熟练使用, 以及对边界条件的处理能力. 实际上Leetcode上有很多类似的题目, 同学们可以总结一套自己的模板, 这样面试中比较容易和面试官说清楚思路, 也可以避免出错. 

本文的模板主要有以下几个需要注意的地方:
- 用一个`dummy node`来指向返回节点
- 用一个变量`carry`来记住进位
- `while`循环有三个, 第一个是两个链表都没有走完的情况, 另两个是其中一个没有走完的情况
- 最后要记得判断一下`carry`不为零的情况, 这样还要再加一个节点

#### 示例代码 (cpp)
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int carry = 0;
        ListNode* dummy = new ListNode(-1);
        ListNode* node = dummy;
        while (l1 && l2) {
            int tmp = l1->val + l2->val + carry;
            int val = tmp % 10;
            carry = tmp / 10;
            node->next = new ListNode(val);
            node = node->next;
            l1 = l1->next;
            l2 = l2->next;
        }
        while (l1) {
            int tmp = l1->val + carry;
            int val = tmp % 10;
            carry = tmp / 10;
            node->next = new ListNode(val);
            node = node->next;
            l1 = l1->next;
        }
        while (l2) {
            int tmp = l2->val + carry;
            int val = tmp % 10;
            carry = tmp / 10;
            node->next = new ListNode(val);
            node = node->next;
            l2 = l2->next;
        }
        if (carry) {
            node->next = new ListNode(carry);
        }
        return dummy->next;
    }
};
```

#### 复杂度分析
时间复杂度: `O(max(m, n))`, `m`和`n`分别是链表`l1`和`l2`的长度
空间复杂度: `O(max(m, n))`

#### 归纳总结
面试中遇到这道题, 写完一定要用特殊例子检查一下. 因为本题思路很直接, 但是边界条件较多, 如果有边界条件没有考虑到会减分.

本文提供的模板思路清晰, 但代码量稍多, 同学们也可以只用一个`while`循环, 截止条件替换为`l1 || l2`, 然后在循环中判断`l1`和`l2`是否为`NULL`, 同学们选择比较顺手的作为模板即可, 没有必要来回切换.