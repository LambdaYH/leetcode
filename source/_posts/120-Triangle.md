---
title: 120. Triangle
date: 2021-04-01 11:36:54 +0800
categories: leetcode
tags: Dynamic Programming
---
#### [120. Triangle](https://leetcode.com/problems/triangle/)
##### 动态规划
```c++
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
        for(size_t layer = 1; layer < n; ++layer)
        {
            triangle[layer][0] += triangle[layer - 1][0];
            triangle[layer].back() += triangle[layer - 1].back();
            for(size_t i = 1; i < triangle[layer].size() - 1; ++i)
            {
                triangle[layer][i] += min(triangle[layer - 1][i], triangle[layer - 1][i - 1]);
            }
        }
        sort(triangle.back().begin(), triangle.back().end());
        return triangle.back().front();
    }
};
```
T(n): O(n)

S(n): O(1)
