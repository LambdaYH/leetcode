---
title: 剑指 Offer 25. 合并两个排序的链表
date: 2021-06-18 19:02:15 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 25. 合并两个排序的链表](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)


##### 递归
参考[21. Merge Two Sorted Lists](https://leetcode.cinte.cc/2021/03/14/21-Merge-Two-Sorted-Lists/)

##### 迭代
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* pesudoHead = new ListNode();
        ListNode* head = pesudoHead;
        while(l1 && l2)
        {
            if(l1->val > l2->val)
            {
                pesudoHead->next = l2;
                l2 = l2->next;
            }else
            {
                pesudoHead->next = l1;
                l1 = l1->next;
            }
            pesudoHead = pesudoHead->next;
        }
        pesudoHead->next = l1 ? l1 : l2;
        return head->next;
    }
};
```
