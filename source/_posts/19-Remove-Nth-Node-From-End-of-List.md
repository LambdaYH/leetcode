---
title: 19. Remove Nth Node From End of List
date: 2021-03-14 11:29:05 +0800
categories: leetcode
---
#### [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* target = head;
        int size = 0;
        ListNode* iterator = head;
        while (iterator != nullptr)
        {
            ++size;
            iterator = iterator->next;
        }

        for (int i = 0; i < size - n - 1; ++i)
        {
            target = target->next;
        }
        if (size - n - 1 == -1)
        {
            head = head->next;
        }
        if (target->next != nullptr)
            target->next = target->next->next;
        return head;
    }
};
```
##### discussion
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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode *start = new ListNode();
        ListNode *fast = start, *slow = start;
        start->next = head;
        for (int i = 0; i < n + 1; ++i)
        {
            fast = fast->next;
        }
        while(fast != nullptr)
        {
            fast = fast->next;
            slow = slow->next;
        }
        slow->next = slow->next->next;
        return start->next;
    }
};
```
