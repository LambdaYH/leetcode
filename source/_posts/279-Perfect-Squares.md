---
title: 279. Perfect Squares
date: 2021-04-02 16:31:59 +0800
categories: leetcode
tags: Dynamic Programming
---
#### [279. Perfect Squares](https://leetcode.com/problems/perfect-squares/)

##### backTrack 超时了，虽然可以运行但是太慢了
```c++
class Solution {
public:
    int numSquares(int n) {
        int count = INT_MAX;
        int temp = 0;
        backTrack(n, count, temp);
        return count;
        
    }
private:
    void backTrack(int n, int& count, int& temp)
    {
        if(n == 0)
            count = min(count, temp);
        
        for(size_t i = sqrt(n); i > 0; --i)
        {
            ++temp;
            backTrack(n - i * i, count, temp);
            --temp;
        }
    }
};
```

##### dp
```c++
class Solution {
public:
    int numSquares(int n) {
        vector<int> cnt(n + 1, INT_MAX - 1);
        cnt[0] = 0;
        for(size_t i = 1; i <= n; ++i)
        {
            for(size_t j = 1; j * j <= i; ++j)
            {
                cnt[i] = min(cnt[i - j * j] + 1, cnt[i]);
            }
        }
        return cnt[n];
    }
};
````
T(n) : O(nlogn) <br>
S(n) : O(n)


动态规划 ： 用数组存储子问题的值，用子问题的值直接得到现在问题的值
