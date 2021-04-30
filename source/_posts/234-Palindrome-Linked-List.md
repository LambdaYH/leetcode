---
title: 234. Palindrome Linked List
date: 2021-04-13 19:57:40 +0800
categories: leetcode
tags: 
- Linked List
---
#### [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

##### 很慢的two Point
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
    bool isPalindrome(ListNode* head) {
        ListNode* walker = head;
        ListNode* runner = head;
        stack<int> s;
        while(walker)
        {
            if(runner)
            {
                if(runner->next)
                {
                    s.push(walker->val);
                    runner = runner->next->next;
                }else
                    runner = nullptr;
                
            }else
            {
                if(s.top() != walker->val)
                    return false;
                s.pop();
            }
            walker = walker->next;
        }
        return true;
    }
};
```

##### 使用链表反转


##### two point 法2
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
    bool isPalindrome(ListNode* head) {
        ListNode* rev = nullptr;
        ListNode* runner = head;
        ListNode* walker = head;
        while(runner && runner->next)
        {
            runner = runner->next->next;
            ListNode *tmp = rev;
            rev = walker;
            walker = walker->next;
            rev->next = tmp;
        }
        if(runner)
            walker = walker->next;
        while(rev && rev->val == walker->val)
        {
            rev = rev->next;
            walker = walker->next;
        }
        return rev ? false : true;
    }
};
```
