---
title: 剑指 Offer 35. 复杂链表的复制
date: 2021-06-25 16:40:22 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

参考[138. Copy List with Random Pointer](https://leetcode.cinte.cc/2021/04/28/138.%20Copy%20List%20with%20Random%20Pointer/)

##### 建立新节点和老节点的映射
```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/
class Solution {
public:
    Node* copyRandomList(Node* head) {
        unordered_map<Node*, Node*> map;
        Node* pre = new Node(0);
        Node* pseudoHead = pre;
        while(head)
        {
            auto node = new Node(head->val);
            pre->next = node;
            map[head] = node;
            pre = node;
            head = head->next;
        }
        for(auto& it : map)
        {
            if(it.first->random)
                it.second->random = map[it.first->random];
            else
                it.second->random = nullptr;
        }
        return pseudoHead->next;
    }
};
```

换个写法

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/
class Solution {
public:
    Node* copyRandomList(Node* head) {
        Node* cur = head;
        unordered_map<Node*, Node*> map;
        while(cur)
        {
            map[cur] = new Node(cur->val);
            cur = cur->next;
        }
        cur = head;
        while(cur)
        {
            map[cur]->next = map[cur->next];
            map[cur]->random = map[cur->random];
            cur = cur->next;
        }
        return map[head];
    }
};
```

##### 拼+拆
```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/
class Solution {
public:
    Node* copyRandomList(Node* head) {
        if(!head)
            return nullptr;
        auto cur = head;
        while(cur)
        {
            auto next = cur->next;
            cur->next = new Node(cur->val);
            cur->next->next = next;
            cur = next;
        }
        cur = head;
        while(cur)
        {
            if(cur->random)
                cur->next->random = cur->random->next;
            cur = cur->next->next;
        }
        cur = head;
        auto newL = head->next;
        auto ret = newL;
        while(newL->next)
        {
            cur->next = cur->next->next;
            newL->next = newL->next->next;
            cur = cur->next;
            newL = newL->next;
        }
        cur->next = nullptr;
        return ret;
    }
};
```
