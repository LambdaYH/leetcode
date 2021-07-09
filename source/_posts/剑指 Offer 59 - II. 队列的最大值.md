---
title: 剑指 Offer 59 - II. 队列的最大值
date: 2021-07-09 16:09:08 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 59 - II. 队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

##### 维护一个辅助队列
```c++
class MaxQueue {
public:
    MaxQueue() {

    }
    
    int max_value() {
        if(nodes.empty())
            return -1;
        return helper.front();
    }
    
    void push_back(int value) {
        while(!helper.empty() && value > helper.back())
            helper.pop_back();
        helper.push_back(value);
        nodes.push_back(value);
    }
    
    int pop_front() {
        if(nodes.empty())
            return -1;
        if(helper.front() == nodes.front())
            helper.pop_front();
        auto ret = nodes.front();
        nodes.pop_front();
        return ret;
    }
private:
    deque<int> nodes; // 其实这个直接用queue也行
    deque<int> helper;
};

/**
 * Your MaxQueue object will be instantiated and called as such:
 * MaxQueue* obj = new MaxQueue();
 * int param_1 = obj->max_value();
 * obj->push_back(value);
 * int param_3 = obj->pop_front();
 */
```

