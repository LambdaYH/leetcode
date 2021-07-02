---
title: 剑指 Offer 44. 数字序列中某一位的数字
date: 2021-07-02 17:36:33 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 44. 数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

##### 又是一道数学的找规律类型的题，好烦
```c++
class Solution {
public:
    int findNthDigit(int n) {
        long digit = 1, count = 9, start = 1;
        while(count < n)
        {
            n -= count;
            start *= 10;
            ++digit;
            count = 9 * digit * start;
        }
        int num = (n - 1) / digit + start;
        return to_string(num)[(n - 1) % digit] - '0';
    }
};
```

![1625218647824.png](https://image.cinte.cc/2021/07/02/e8c38b67f4a9f.png)
![1625218657922.png](https://image.cinte.cc/2021/07/02/8e35c23ecca2e.png)
![1625218664563.png](https://image.cinte.cc/2021/07/02/bb1f38fce087f.png)
