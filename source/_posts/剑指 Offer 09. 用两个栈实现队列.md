---
title: 剑指 Offer 09. 用两个栈实现队列
date: 2021-06-15 17:34:08 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

##### 倒来倒去
```c++
class CQueue {
public:
    CQueue() {

    }
    
    void appendTail(int value) {
        s1.push(value);
    }
    
    int deleteHead() {  // s2中的最上面必定为最后的，如果s2空 把s2倒过去
        if(s2.empty())
        {
            while(!s1.empty())
            {
                s2.push(s1.top());
                s1.pop();
            }
        }
        if(s2.empty())
            return -1;
        auto tmp = s2.top();
        s2.pop();
        return tmp;
    }
private:
    stack<int> s1, s2;
};

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue* obj = new CQueue();
 * obj->appendTail(value);
 * int param_2 = obj->deleteHead();
 */
```
