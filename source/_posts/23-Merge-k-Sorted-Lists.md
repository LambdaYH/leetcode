---
title: 23. Merge k Sorted Lists
date: 2021-03-21 13:38:23 +0800
categories: 
- leetcode
---
#### [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
##### Solution 1
思路![](https://image.cinte.cc/2021/03/21/71cece659332e.png)
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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.empty()) return nullptr;
        vector<ListNode*> newLists;   
        for(size_t i = 0; i < lists.size(); i = i + 2)
        {
            if(i != lists.size() - 1)
            {
                newLists.push_back(mergeTwoLists(lists[i], lists[i + 1]));
            }else
            {
                newLists.push_back(lists[i]);
            }
        }
        if(newLists.size() == 1)
            return newLists[0];
        
        return mergeKLists(newLists);
    }
private:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2)
    {
        if(!l1) return l2;
        if(!l2) return l1;
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
Time complexity: O(NlogK) <br>
Space complexity: O(logK)

**优化后**
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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        int stride = 1;
        int sz = lists.size();
        while(stride < sz)
        {
            for(size_t i = 0; i < sz - stride; i = i + 2 * stride)
            {
                lists[i] = mergeTwoLists(lists[i], lists[i + stride]);
            }
            stride *= 2;
        }   
        return lists.empty() ? nullptr : lists[0];
    }
private:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2)
    {
        if(!l1) return l2;
        if(!l2) return l1;
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
Time complexity: O(NlogK) <br>
Space complexity: O(1)

##### Solution 2 use priority_queue
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
class cuscomp
{
public:
    bool operator()(pair<int, ListNode *> p1, pair<int, ListNode *> p2)
    {
        return p1.first > p2.first;
    }
};
class Solution
{
public:
    ListNode *mergeKLists(vector<ListNode *> &lists)
    {
        std::priority_queue<pair<int, ListNode *>, std::vector<pair<int, ListNode *>>, cuscomp> q;
        ListNode *point = new ListNode();
        ListNode *head = point;
        for (auto &list : lists)
        {
            if(list)
                q.push(make_pair(list->val, list));
        }
        while (!q.empty())
        {
            auto node = q.top().second;
            q.pop();
            point->next = new ListNode(node->val);
            point = point->next;
            node = node->next;
            if (node)
                q.push(make_pair(node->val, node));
        }
        return head->next;
    }
};
```
Time complexity: O(NlogK) <br>
Space complexity: O(N)
