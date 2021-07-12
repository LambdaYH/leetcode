---
title: 剑指 Offer 64. 求1+2+…+n
date: 2021-07-12 15:22:44 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 64. 求1+2+…+n](https://leetcode-cn.com/problems/qiu-12n-lcof/)

##### shuai
```c++
class Solution {
public:
    int sumNums(int n) {
        bool x = n > 1 && sumNums(n - 1); // n == 1时候终止递归，递归栈返回，从ret从n=1开始加上去。 此处使用逻辑符短路，代替了原本if(n <= 1) return 1;
        ret += n;
        return ret;
    }
private:
    int ret = 0;
};
```

如果没题目限制使用递归

```c++
class Solution {
public:
    int sumNums(int n) {
        if(n == 1)
            return 1;
        n += sumNums(n - 1);
        return n;
    }
};
```
