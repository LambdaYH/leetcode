---
title: 322. Coin Change
date: 2021-04-21 21:39:13 +0800
categories: leetcode
tags: Dynamic Programming
---
#### [322. Coin Change](https://leetcode.com/problems/coin-change/)

##### DFS
```c++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount + 1, amount + 1);
        dp[0] = 0;
        for(int i = 1; i <= amount; ++i)
        {
            for(int j = 0; j < coins.size(); ++j)
            {
                if(coins[j] <= i)
                    dp[i] = min(dp[i], dp[i - coins[j]] + 1);
            }
        }
        return dp[amount] == amount + 1 ? -1 : dp[amount];
    }
};
```
