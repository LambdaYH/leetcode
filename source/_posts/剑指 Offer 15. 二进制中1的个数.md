---
title: 剑指 Offer 15. 二进制中1的个数
date: 2021-06-23 19:23:49 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 15. 二进制中1的个数](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

#####
```C++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int ret = 0;
        while(n)
        {
            ret += n & 1;
            n >>= 1;
        }
        return ret;
    }
};
```

##### 骚方法（太优秀了
```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int ret = 0;
        while(n)
        {
            ++ret;
            n &= (n - 1);
        }
        return ret;
    }
};
```

![1624447689192.png](https://image.cinte.cc/2021/06/23/920f8c9f62526.png)
