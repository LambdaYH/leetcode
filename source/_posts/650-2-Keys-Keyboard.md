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

```c++
class Solution {
public:
    int minSteps(int n) {
        vector<int> dp(n + 1);
        dp[1] = 0;
        for(int i = 2; i <= n; ++i)
        {
            dp[i] = i;
            // j 和 i / j必定有一个小于等于根号i
            for(int j = 2; j * j <= i; ++j)
            {
                if(i % j == 0)
                {
                    dp[i] = min(dp[j] + i / j, dp[i]);
                    dp[i] = min(dp[i / j] + j, dp[i]);
                }
            }
        }
        return dp.back();
    }
};
```
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
```
如果找到了一个更短的序列也能被整除，假设第一次找到的为j，第二次找到的为k，则j / k = m，设i / j = n，则i / k = m * n。则dp[j] = dp[k] + m，而dp[i] = dp[j] + n = dp[k] + m * n
则dp[i] = dp[j] + n = dp[k] + m * n = dp[k] + m + n，因为当m > 1 && n > 1时，m+n<mn(mn - (m + n) = (m - 1)(n - 1))，所以第一次遇到的就是最小的结果。
当然，如果不放心的话，也可以用min来遍历
```

##### solution数学方法 

[Prime Factorization 整数分解](https://zh.wikipedia.org/wiki/%E6%95%B4%E6%95%B0%E5%88%86%E8%A7%A3)

看[题解](https://leetcode-cn.com/problems/2-keys-keyboard/solution/zhi-you-liang-ge-jian-de-jian-pan-by-lee-ussa/#:~:text=%E9%9C%80%E8%A6%81%E7%9A%84%E7%A9%BA%E9%97%B4%E3%80%82-,%E6%96%B9%E6%B3%95%E4%BA%8C%EF%BC%9A%E5%88%86%E8%A7%A3%E8%B4%A8%E5%9B%A0%E6%95%B0,-%E6%80%9D%E8%B7%AF%E4%B8%8E%E7%AE%97%E6%B3%95)吧

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

