---
title: 剑指 Offer 22. 链表中倒数第k个节点
date: 2021-06-24 16:25:34 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

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
    ListNode* getKthFromEnd(ListNode* head, int k) {
        ListNode* runner = head, *walker = head;
        for(int i = 0; i < k; ++i)
            runner = runner->next;
        while(runner)
        {
            walker = walker->next;
            runner = runner->next;
        }
        return walker;
    }
};
```
