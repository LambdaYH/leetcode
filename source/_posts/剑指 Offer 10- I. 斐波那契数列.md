---
title: 剑指 Offer 10- I. 斐波那契数列
date: 2021-06-15 17:49:30 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

##### 一个初级dp
```c++
class Solution {
public:
    int fib(int n) {
        if(n < 2)
            return n;
        int memo[2];
        memo[0] = 0;
        memo[1] = 1;
        for(int i = 2; i <= n; ++i)
        {
            auto tmp = memo[0];
            memo[0] += memo[1];
            memo[0] %= 1000000007;
            swap(memo[0], memo[1]);
        }
        return memo[1];
    }
};
```

##### 题解中的
```c++
class Solution {
public:
    int fib(int n) {
        int memo[2];
        memo[0] = 0;
        memo[1] = 1;
        for(int i = 2; i <= n + 1; ++i) // 为了少判断一下0和1的情况，他就多算一次，6的时候，保留5的计算结果，此时5的计算结果回到了memo[0]，但是多算了一次，没意思
        {
            auto tmp = memo[0];
            memo[0] += memo[1];
            memo[0] %= 1000000007;
            swap(memo[0], memo[1]);
        }
        return memo[0];
    }
};
```
