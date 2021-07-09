---
title: 剑指 Offer 65. 不用加减乘除做加法
date: 2021-07-09 15:43:08 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 65. 不用加减乘除做加法](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/submissions/)

##### 位运算
```c++
class Solution {
public:
    int add(int a, int b) {
        int c;
        while(b)
        {
            c = (unsigned int)(a & b) << 1; // leetcode的编译环境问题导致这里负数左移会报错，g++中则测试正常c = (a & b) << 1
            a ^= b;
            b = c;
        }
        return a;
    }
};
```

由于使用的是补码可以统一负数和正数运算，所以不用考虑正负数。

考察位运算，首先可以知道对于加法器，如果不考虑进位，那么值就是`a ^ b`，而进位为`a & b`。则将不考虑进位算出来的值加上进位最终就是考虑进位的值，由于当前计算结果的进位是用于下一位的，所以需要将计算所得的进位左移一位，再次加，获得新的进位，知道进位为0，停止计算。
