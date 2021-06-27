---
title: 剑指 Offer 30. 包含min函数的栈
date: 2021-06-27 17:18:41 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 30. 包含min函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

##### 
参考[155. Min Stack](https://leetcode.cinte.cc/2021/04/09/155-Min-Stack/)

自建链表节点，节点中加入min属性

```c++
class MinStack {
public:
    /** initialize your data structure here. */
    MinStack() : head(new node(0)) {

    }
    
    void push(int x) {
        auto n = new node(x, head->next);
        if((n->next && n->next->min > x) || !n->next)
            n->min = x;
        else
            n->min = n->next->min;
        head->next = n;
        
    }
    
    void pop() {
        if(head->next)
        {
            auto p = head->next;
            head->next = head->next->next;
            delete p;
        }
    }
    
    int top() {
        if(head->next)
            return head->next->val;
        return 0;
    }
    
    int min() {
        if(head->next)
            return head->next->min;
        return 0;
    }
private:
    struct node {
        node* next = nullptr;
        int val;
        int min = 0;
        node() = default;
        node(int val) : val(val) {}
        node(int val, node* next) : val(val), next(next) {}
    };
    node* head;
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->min();
 */
```

##### 辅助堆
```c++
class MinStack {
public:
    /** initialize your data structure here. */
    MinStack() {

    }
    
    void push(int x) {
        s1.push(x);
        if(s2.empty() || s2.top() >= x)
            s2.push(x);
    }
    
    void pop() {
        if(s2.top() == s1.top())
            s2.pop();
        s1.pop();
    }
    
    int top() {
        return s1.top();
    }
    
    int min() {
        return s2.top();
    }
private:
    stack<int> s1;
    stack<int> s2;
};
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->min();
 */
 ```
