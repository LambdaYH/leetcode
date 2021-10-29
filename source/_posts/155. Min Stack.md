---
title: 155. Min Stack
date: 2021-04-09 20:40:31 +0800
categories: leetcode
tags: 
- Stack
---
#### [155. Min Stack](https://leetcode.com/problems/min-stack/)

抄的dicussion中的[一种实现方法](https://leetcode.com/problems/min-stack/discuss/49010/Clean-6ms-Java-solution)，真的帅

```c++
class MinStack {
public:
    /** initialize your data structure here. */
    MinStack() {
        topEle = nullptr;
    }    
    void push(int val) {
        if(!topEle)
            topEle = new Node(val, val);
        else
            topEle = new Node(val, min(topEle->min, val), topEle);
    }
    
    void pop() {
        auto tmp = topEle;
        topEle = tmp->next;
        delete tmp;
    }
    
    int top() {
        return topEle->val;
    }
    
    int getMin() {
        return topEle->min;
    }
private:
    struct Node {
        int val;
        int min;
        Node* next;
        Node () : val(0), min(INT_MAX), next(nullptr) {}
        Node (int val, int min) : val(val), min(min), next(nullptr) {}
        Node (int val, int min, Node* next) : val(val), min(min), next(next) {}
    };
    Node* topEle;
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```
