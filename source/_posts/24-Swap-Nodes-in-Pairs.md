---
title: 24. Swap Nodes in Pairs
date: 2021-03-15 19:12:05 +0800
categories: leetcode
---
#### [24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(head == nullptr || head->next == nullptr) return head;
        ListNode* point = head;
        ListNode* pre = new ListNode();
        pre->next = head;
        ListNode* newHead = head->next;
        while(point != nullptr && point->next != nullptr)
        {
            ListNode* n2 = point->next;
            ListNode* next = n2->next;
            n2->next = point;
            point->next = next;
            pre->next = n2;
            pre = point;
            point = next;
        }
        return newHead;
    }
};
```
##### discussion 递归
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(head == nullptr || head->next ==nullptr) return head;
        ListNode* n = head->next;
        head->next = swapPairs(head->next->next);
        n->next = head;
        return n;
    }
};
```
