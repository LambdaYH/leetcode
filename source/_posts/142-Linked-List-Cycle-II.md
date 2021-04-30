---
title: 142. Linked List Cycle II
date: 2021-04-12 19:48:59 +0800
categories: leetcode
tags: 
- Linked List
---
#### [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)
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
    ListNode *detectCycle(ListNode *head) {
        unordered_set<ListNode*> set;
        int i = 0;
        while(head)
        {
            if(!(set.emplace(head).second))
            {
                return head;
            }
            head = head->next;
        }
        return nullptr;
    }
};
```
T(n) : O(n) <br>
S(n) : O(n)

##### 使用linked cycle中的two point 方法
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
    ListNode *detectCycle(ListNode *head) {
        if(!head) return nullptr;
        ListNode* walker = head;
        ListNode* runner = head;
        
        bool isMeet = false;
        while(runner->next && runner->next->next)
        {
            walker = walker->next;
            runner = runner->next->next;
            if(walker == runner)
            {
                isMeet = true;
                break;
            }
        }
        
        if(isMeet)
        {
            walker = head;
            while(walker != runner)
            {
                walker = walker->next;
                runner = runner->next;
            }
            return runner;
        }
        return nullptr;
    }
};
```

![image.png](https://image.cinte.cc/2021/04/12/fe23f299564ba.png)
即当一个点从第一次遇见的点开始，走r-m步，走到环的起始点时，另一个点刚好从起点走到环的起始点
