---
title: 剑指 Offer 41. 数据流中的中位数
date: 2021-06-27 17:36:22 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 41. 数据流中的中位数](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof//)

参考[295. Find Median from Data Stream](https://leetcode.cinte.cc/2021/05/04/295.%20Find%20Median%20from%20Data%20Stream/)

##### 两个优先级队列  

有点忘了

```c++
class MedianFinder {
public:
    /** initialize your data structure here. */
    MedianFinder() {
 
    }
    
    void addNum(int num) {
        if(q1.size() == q2.size())
        {
            q1.push(num);
            q2.push(q1.top());
            q1.pop();
        }else
        {
            q2.push(num);
            q1.push(q2.top());
            q2.pop();
        }
        
    }
    
    double findMedian() {
        if(q1.size() != q2.size())
            return q2.top();
        else
            return (q1.top() + q2.top()) / 2.0;
    }
private:
    priority_queue<int, vector<int>, std::greater<int>> q1;
    priority_queue<int> q2;
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
 ```
