---
title: 剑指 Offer 16. 数值的整数次方
date: 2021-06-24 17:20:22 +0800
categories: 剑指 Offer
mathjax: true
---
#### [剑指 Offer 16. 数值的整数次方](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

##### 二分法O(logn)
```c++
class Solution {
public:
    double myPow(double x, int n) {
        double ret = 1;
        long b = static_cast<long>(n);
        if(b < 0)
        {
            b = -b;   // 先反转成全是正数
            x = 1/x;  // 基准
        }
        while(b)
        {
            if(b & 1)
                ret *= x;  // 如果次数为奇数 那么先乘一个x
            x *= x; // 转为x^2
            b >>= 1; // 转为n/2
            // 操作过后 基准变为x^2，x^2成为了下一个x，而n/2成为了下一个n，由此迭代
        }
        return ret;
    }
};
```


当输入的次数n为**奇数**时

$$ X^n=X*(X^2)^{n/2}$$

当输入的次数n为**偶数**时

$$ X^n=(X^2)^{n/2}$$
