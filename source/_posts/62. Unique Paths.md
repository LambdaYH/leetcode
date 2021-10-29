---
title: 62. Unique Paths
date: 2021-03-27 10:05:04 +0800
categories: leetcode
tags: Dynamic Programming
---
#### [62. Unique Paths](https://leetcode.com/problems/unique-paths/)
```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        return path(m, n);
    }
private:
    int path(int m, int n)
    {
        if(m == 1 || n == 1)
            return 1;
        
        return path(m - 1, n) + path(m, n - 1);
    }
};
```

Time Limit Exceeded

##### 动态规划，划分为子路径
```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n, 1));
        for(size_t i = 1; i < m; ++i)
        {
            for(size_t j = 1; j < n; ++j)
            {
                dp[i][j] = dp[i][j - 1] + dp[i - 1][j];
            }
        }
        return dp[m - 1][n - 1];
    }
};
```

