---
title: 2. Add Two Numbers
date: 2021-02-01 23:46:00 +0800
categories: leetcode
---
#### [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
##### 第一次
```c++
class Solution
{
public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2)
    {
        ListNode *result = new ListNode();
        ListNode *point = result;
        unsigned int c = 0;
        do
        {
            int sum;
            try
            {
                if (l1 != 0 && l2 != 0)
                {
                    sum = l1->val + l2->val + c;
                    l1 = l1->next;
                    l2 = l2->next;
                    throw "case 1";
                }
                else if (l1 != 0 && l2 == 0)
                {
                    sum = l1->val + c;
                    l1 = l1->next;
                    throw "case 2";
                }
                else if (l1 == 0 && l2 != 0)
                {
                    sum = l2->val + c;
                    l2 = l2->next;
                    throw "case 3";
                }
                else
                {
                    sum = 0;
                }
            }
            catch (...)
            {
                point->val = sum % 10;
                c = sum / 10;
                if (l1 != 0 || l2 != 0)
                {
                    point->next = new ListNode();
                    point = point->next;
                }
                else
                {
                    if (c != 0)
                    {
                        point->next = new ListNode(c);
                    }
                }
            }
        } while (l1 != 0 || l2 != 0);

        return result;
    }
};
```
![第一次结果](https://image.cinte.cc/2021/02/01/5634aa76486d6.png)
<!-- more -->

##### 第二次
```c++
class Solution
{
public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2)
    {
        ListNode *result = new ListNode();
        ListNode *point = result;
        unsigned int c = 0;
        do
        {
            int sum;

            if (l1 != 0 && l2 != 0)
            {
                sum = l1->val + l2->val + c;
                l1 = l1->next;
                l2 = l2->next;
            }
            else if (l1 != 0 && l2 == 0)
            {
                sum = l1->val + c;
                l1 = l1->next;
            }
            else if (l1 == 0 && l2 != 0)
            {
                sum = l2->val + c;
                l2 = l2->next;
            }
            else
            {
                sum = 0 + c;
            }

            point->val = sum % 10;
            c = sum / 10;
            if (l1 != 0 || l2 != 0 || c != 0)
            {
                point->next = new ListNode();
                point = point->next;
            }

        } while (l1 != 0 || l2 != 0 || c != 0);

        return result;
    }
};
```
![](https://image.cinte.cc/2021/02/02/dcab1942c9d21.png)

##### 复习
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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        auto pseudoL1 = l1;
        auto pseudoL2 = l2;
        int l1Length = 0;
        int l2Length = 0;
        while(pseudoL1)
        {
            ++l1Length;
            pseudoL1 = pseudoL1->next;
        }
        while(pseudoL2)
        {
            ++l2Length;
            pseudoL2 = pseudoL2->next;
        }
        
        if(l1Length > l2Length)
            swap(l1, l2);
        auto ret = l2;
        auto pre = l2;
        int c = 0;
        while(l1)
        {
            auto sum = l2->val + l1->val + c;
            c = sum / 10;
            l2->val = sum % 10;
            pre = l2;
            l1 = l1->next;
            l2 = l2->next;
        }
        while(c)
        {
            if(!l2)
            {
                pre->next = new ListNode(c);
                break;
            }
            else
            {
                auto sum = l2->val + c;
                l2->val = sum % 10;
                c = sum / 10;
                pre = l2;
                l2 = l2->next;
            }
        }
        return ret;
    }
};
```

![1621148746599.png](https://image.cinte.cc/2021/05/16/7355ecdb33a0c.png)
