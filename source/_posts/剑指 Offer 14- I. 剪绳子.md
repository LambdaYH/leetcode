---
title: 剑指 Offer 14- I. 剪绳子
date: 2021-06-18 16:46:25 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 14- I. 剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/submissions/)

##### dp
参考[343. Integer Break](https://leetcode.cinte.cc/2021/05/19/343.%20Integer%20Break/)


##### 数学方法  TAIFUZALE
```C++
class Solution {
public:
    int cuttingRope(int n) {
        if(n <= 3) 
            return n - 1;
        int a = n / 3;
        int b = n % 3;
        int ret = 1;
        if(b == 1)
            return pow(3, a - 1) * 4;
        if(b == 0)
            return pow(3, a);
        return pow(3, a) * 2;
    }
};
```
