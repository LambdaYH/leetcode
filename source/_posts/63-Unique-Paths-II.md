---
title: 63. Unique Paths II
date: 2021-03-31 16:57:18 +0800
categories: leetcode
tags: Dynamic Programming
---
#### [63. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)
##### 动态规划
```c++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        if(obstacleGrid[0][0]) 
            return 0;
        else
            obstacleGrid[0][0] = 1;
        
        size_t m = obstacleGrid.size();
        size_t n = obstacleGrid[0].size();
        
        for(size_t i = 1; i < m; ++i)
        {
            obstacleGrid[i][0] = obstacleGrid[i][0] ? 0 : obstacleGrid[i - 1][0];
        }
        for(size_t i = 1; i < n; ++i)
        {
            obstacleGrid[0][i] = obstacleGrid[0][i] ? 0 : obstacleGrid[0][i - 1];
        }
        for(size_t i = 1; i < m; ++i)
        {
            for(size_t j = 1; j < n; ++j)
            {
                obstacleGrid[i][j] = obstacleGrid[i][j] ? 0 : obstacleGrid[i - 1][j] + obstacleGrid[i][j - 1];
            }
        }
        return obstacleGrid.back().back();
    }
};
```
T(n) : O(m * n)

S(n) : O(1)

动态规划问题可以归结为网格，此处网格中元素为每个块对路径的贡献度，当本块为障碍时则贡献为0，当本块无障碍，则上方和左方的方块可以走过来，贡献的路径就是上和左相加
