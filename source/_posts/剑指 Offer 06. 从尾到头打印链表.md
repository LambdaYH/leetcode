---
title: 剑指 Offer 06. 从尾到头打印链表
date: 2021-06-17 21:46:23 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

##### 先反转链表再打印
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
    vector<int> reversePrint(ListNode* head) {
        vector<int> ret;
        auto node = reverse(head);
        while(node)
        {
            ret.push_back(node->val);
            node = node->next;
        }
        return ret;
    }
private:
    ListNode* reverse(ListNode* node)
    {
        ListNode* newNext = nullptr;
        while(node)
        {
            auto next = node->next;
            node->next = newNext;
            newNext = node;
            node = next;
        }
        return newNext;
    }
};
```

T(n) = O(n)

##### 遍历获取大小再倒着来
```c++
不想写
```

##### 递归时候返回
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
    vector<int> reversePrint(ListNode* head) {
        vector<int> ret;
        re(ret, head);
        return ret;
    }
private:
    void re(vector<int>& ret, ListNode* node)
    {
        if(!node)
            return;
        re(ret, node->next);
        ret.push_back(node->val);
    }
};
```

##### 用堆栈
不想写
