---
title: 64. Minimum Path Sum
date: 2021-03-30 10:10:42 +0800
categories: leetcode
tags: Dynamic Programming
---
#### [64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)
##### 动态规划
```c++
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        size_t m = grid.size(), n = grid[0].size();
        vector<vector<int>> dp(m, vector<int>(n, 0));
        dp[0][0] = grid[0][0];      
        for(size_t i = 0; i < m; ++i)
        {
            for(size_t j = 0; j < n; ++j)
            {
                if(i == 0 && j == 0)
                    continue;
                if(i == 0)
                    dp[i][j] = dp[i][j - 1] + grid[i][j];
                else if(j == 0)
                    dp[i][j] = dp[i - 1][j] + grid[i][j];
                else
                    dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
            }
        }
        return dp[m - 1][n - 1];
    }
};
```
T(n) : O(m * n)

S(n) : O(m * n)

##### 尝试对S(n) 优化

观察代码，发现每次用到的数据只有dp[i][j], dp[i][j - 1]和dp[i - 1][j]，考虑dp[i][j], dp[i][j - 1]合并到一个一维数组，剩下的再生产一个一维数组。

参考[unique path](https://leetcode.com/problems/unique-paths/discuss/22954/C%2B%2B-DP)中的方法
```c++
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        size_t m = grid.size(), n = grid[0].size();
        int* cur = new int[n];
        int* pre = new int[n];
        for (size_t i = 0; i < m; ++i)
        {
            for (size_t j = 0; j < n; ++j)
            {
                if (i == 0 && j == 0)
                    cur[j] = grid[i][j];
                else if (i == 0)
                    cur[j] = cur[j - 1] + grid[i][j];
                else if (j == 0)
                    cur[j] = pre[j] + grid[i][j];
                else
                    cur[j] = min(pre[j], cur[j - 1]) + grid[i][j];
            }
            swap(cur, pre);
        }
        return pre[n - 1];
    }
};
```
T(n) : O(m * n)

S(n) : O(2 * n)

##### 再优化

pre[j] 与 cur[j] 可以合并

```c++
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        size_t m = grid.size(), n = grid[0].size();
        int* cur = new int[n];
        for (size_t i = 0; i < m; ++i)
        {
            for (size_t j = 0; j < n; ++j)
            {
                if (i == 0 && j == 0)
                    cur[j] = grid[i][j];
                else if (i == 0)
                    cur[j] = cur[j - 1] + grid[i][j];
                else if (j == 0)
                    cur[j] = cur[j] + grid[i][j];
                else
                    cur[j] = min(cur[j], cur[j - 1]) + grid[i][j];
            }
        }
        return cur[n - 1];
    }
};
```
T(n) : O(m * n)

S(n) : O(n)
