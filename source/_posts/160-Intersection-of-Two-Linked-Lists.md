---
title: 160. Intersection of Two Linked Lists
date: 2021-04-12 20:05:29 +0800
categories: leetcode
tags: 
- Linked List
---
#### [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

##### 最直接法
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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        unordered_set<ListNode*> set;
        while(headA)
        {
            set.insert(headA);
            headA = headA->next;   
        }
        
        while(headB)
        {
            if(set.find(headB) != set.end())
                return headB;
            headB = headB->next;
        }
        return nullptr;
    }
};
```

##### 预先求差
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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        int lenA{ 0 };
        int lenB{ 0 };
        
        ListNode* a = headA;
        ListNode* b = headB;
        
        while(a)
        {
            ++lenA;
            a = a->next;
        }
        while(b)
        {
            ++lenB;
            b = b->next;
        }
        if(lenA < lenB)
        {
            for(int i = 0; i < lenB - lenA; ++i)
                headB = headB->next;
        }else
        {
            for(int i = 0; i < lenA - lenB; ++i)
                headA = headA->next;
        }
        
        while(headA && headB)
        {
            if(headA == headB)
                return headA;
            headA = headA->next;
            headB = headB->next;
        }
        
        return nullptr;
    }
};
```

##### 2次迭代
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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode *a = headA;
        ListNode *b = headB;
        
        while(a != b)
        {
            a = a == nullptr ? headB : a->next;
            b = b == nullptr ? headA : b->next;
        }
        return a;
    }
};
```

他们第一次跑会有一个长度的差，短的先跑到终点后，到长的端点。当长的指针跑到终点后，回到短的端点。此时先前一个刚好跑了他们的距离差，这是他们在距离上是处于同一个起点的。

设短的到交点距离x，长的到交点距离y，公共部分距离为z，则如果要求交点，那么让他们走到交点的路程一致即可，则让短的走到头后跳到长，长的走到头后跳到短，最后对于短头来说x+y+z,长头也是x+y+z，刚好在交点相交。

具体见[discussion](https://leetcode.com/problems/intersection-of-two-linked-lists/discuss/49785/Java-solution-without-knowing-the-difference-in-len!)中的评论第一条
