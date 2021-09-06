---
title: 剑指 Offer 36. 二叉搜索树与双向链表
date: 2021-06-28 21:02:35 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 36. 二叉搜索树与双向链表](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

##### 中序遍历顺便产生双向链表，记录头
```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;

    Node() {}

    Node(int _val) {
        val = _val;
        left = NULL;
        right = NULL;
    }

    Node(int _val, Node* _left, Node* _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {
public:
    Node* treeToDoublyList(Node* root) {
        if(!root)
            return nullptr;
        Node* pre = nullptr;
        Node* cur = root;
        Node* head = nullptr;
        stack<Node*> s;
        while(!s.empty() || cur)
        {
            while(cur)
            {
                s.push(cur);
                cur = cur->left;
            }
            cur = s.top();
            s.pop();
            cur->left = pre;
            /*
            if(pre)
                pre->right = cur;
            if(!head)
                head = cur;
            */
            // 把2个判断变成一个，减少条件分支预测错误的惩罚？
            if(pre)
                pre->right = cur;
            else
                head = cur;
            pre = cur;
            cur = cur->right;
        }
        pre->right = head;
        head->left = pre;
        return head;
    }
};
```
