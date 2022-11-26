---
title: 剑指 Offer 14- II. 剪绳子 II
date: 2021-06-18 17:52:53 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 14- II. 剪绳子 II](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/)

这题由于n的范围加大
![1624010226494.png](https://image.cinte.cc/i/2021/06/18/0c502a5a8b2f5.png)

##### 数学方法  TAIFUZALE
循环求余
**这是使得中间值取余不影响结果取余的理论保证**
x^a % p = (x^(a-1) % p)*(x % p) = ((x^(a-1) % p) * x) % p

```c++
int ret = 1;
for(int i = 0; i < a; ++i)
    ret = ret * x % p
```

完整代码
```c++
class Solution {
public:
    int cuttingRope(int n) {
        if(n <= 3)
            return n - 1;
        int p = 1000000007;
        int a = n / 3;
        int b = n % 3;
        long ret = 1;
        for(int i = 0; i < (b == 1 ? a - 1 : a); ++i)
            ret = ret * 3 % p;
        if(b == 1)
            return ret * 4 % p;
        if(b == 2)
            return ret * 2 % p;
        return ret;

    }
};
```
