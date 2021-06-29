---
title: 剑指 Offer 31. 栈的压入、弹出序列
date: 2021-06-29 11:39:08 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 31. 栈的压入、弹出序列](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/)

##### 最直观的方式
```c++
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        stack<int> s;
        int i = 0, j = 0;
        for(int i = 0; i < pushed.size(); ++i)
        {
            s.push(pushed[i]);
            while(j < popped.size() && !s.empty() && popped[j] == s.top())
            {
                s.pop();
                ++j;
            }
        }
        if(s.empty())
            return true;
        return false;
    }
};
```

T(n) : O(n)

S(n) : 0(N)
