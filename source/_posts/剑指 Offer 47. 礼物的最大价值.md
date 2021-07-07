---
title: 剑指 Offer 47. 礼物的最大价值
date: 2021-07-07 16:09:23 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 47. 礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)

最简单的dp

##### 
```c++
class Solution {
public:
    int maxValue(vector<vector<int>>& grid) {
        for(int i = 1; i < grid.size(); ++i)
            grid[i][0] += grid[i - 1][0];
        for(int i = 1; i < grid[0].size(); ++i)
            grid[0][i] += grid[0][i - 1];
        for(int i = 1; i < grid.size(); ++i)
            for(int j = 1; j < grid[0].size(); ++j)
                grid[i][j] += max(grid[i - 1][j], grid[i][j - 1]); 
        return grid.back().back();
    }
};
```
