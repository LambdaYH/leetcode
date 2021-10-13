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
```
T(n) : O(n^2) ? <br>
S(n) : O(n)

寻找当前的最大除以2...的数，然后将那个数对应的操作翻倍
```
Elegant solution.
Allow me to explain what is being done here.
As per the keyboard operations:
to get AA from A we need 2 additional steps (copy-all and then paste)
to get AAA from A we need 3 additional steps (copy-all, then paste, then again paste)

For generating AAAA we need 2 additional steps from AA.
however, to get AAAAAAAA, the most optimal way would be from AAAA, with 2 additional steps (copy-all then paste)
Essentially, we find the next smaller length sequence (than the one under consideration) which can be copied and then pasted over multiple times to generate the desired sequence. The moment we find a length that divides our required sequence length perfectly, then we don't need to check for any smaller length sequences.

// if sequence of length 'j' can be pasted multiple times to get length 'i' sequence
if (i % j == 0) {
    // we just need to paste sequence j (i/j - 1) times, hence additional (i/j) times since we need to copy it first as well.
    // we don't need checking any smaller length sequences 
    dp[i] = dp[j] + (i/j);
    break;
}
```

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

