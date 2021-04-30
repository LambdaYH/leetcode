---
title: 650. 2 Keys Keyboard
date: 2021-04-04 15:01:35 +0800
categories: leetcode
tags: 
- Dynamic Programming
- Math
---
#### [650. 2 Keys Keyboard](https://leetcode.com/problems/2-keys-keyboard/)

##### dp
```c++
class Solution {
public:
    int minSteps(int n) {
        vector<int> dp(n + 1);
        dp[1] = 0;
        for(size_t i = 2; i <= n; ++i)
        {
            dp[i] = i;
            for(size_t j = i - 1; j > 1; --j)
            {
                if(!(i % j))
                {
                    dp[i] = dp[j] + i / j;
                    break;
                }
            }
        }
        return dp.back();
    }
};
````
T(n) : O(n^2) ? <br>
S(n) : O(n)

寻找当前的最大除以2...的数，然后将那个数对应的操作翻倍

##### solution数学方法 

[Prime Factorization 整数分解](https://zh.wikipedia.org/wiki/%E6%95%B4%E6%95%B0%E5%88%86%E8%A7%A3)

```c++
class Solution {
public:
    int minSteps(int n) {
        int ret = 0;
        int d = 2;
        while(n > 1)
        {
            while(!(n % d))
            {
                ret += d;
                n /= d;
            }
            ++d;
        }
        return ret;
    }
};
```
T(n) : O(n) worst <br>
S(n) : O(1)

