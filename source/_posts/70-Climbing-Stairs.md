---
title: 70. Climbing Stairs
date: 2021-03-26 21:05:23 +0800
categories: leetcode
tags: Dynamic Programming
---
#### [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
##### 动态规划，每一步都可分为1 + 剩余n-1 + 2 + 剩余n-2
```c++
class Solution {
public:
    int climbStairs(int n) {
        if(n == 1) return 1;
        vector<int> dp;
        dp.push_back(1);
        dp.push_back(2);
        for(size_t i = 2; i < n; ++i)
        {
            dp.push_back(dp[i - 1] + dp[i - 2]);
        }
        return dp.back();
    }
};
```
