---
title: 21. Merge Two Sorted Lists
date: 2021-03-14 20:18:51 +0800
categories: leetcode
---
#### [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(!l1)
            return l2;
        if(!l2)
            return l1;

        while(l1 && l2)
        {
            if(l1->val > l2->val)
            {
                l2->next = mergeTwoLists(l1, l2->next);
                return l2;
            }else
            {
                l1->next = mergeTwoLists(l1->next, l2);
                return l1;
            }
        }
        return nullptr;
    }
};
```

迭代

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode ret;
        ListNode* head = &ret;
        while(l1 && l2)
        {
            if(l1->val > l2->val)
            {
                head->next = l2;
                l2 = l2->next;
            }
            else
            {
                head->next = l1;
                l1 = l1->next;
            }
            head = head->next;
        }
        head->next = l1 ? l1 : l2;
        return ret.next;
    }
};
```
