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
