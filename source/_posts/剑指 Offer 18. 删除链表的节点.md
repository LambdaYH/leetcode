---
title: 剑指 Offer 18. 删除链表的节点
date: 2021-06-25 16:21:47 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 18. 删除链表的节点](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/submissions/)

#####
```c++
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
    ListNode* deleteNode(ListNode* head, int val) {
        ListNode* pre = new ListNode();
        ListNode* ret = pre;
        pre->next = head;
        while(head)
        {
            if(head->val == val)
            {
                pre->next = head->next;
                return ret->next;
            }
            pre = head;
            head = head->next;
        }
        return ret->next;
    }
};
```
