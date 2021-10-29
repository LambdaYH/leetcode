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

##### review

IAMSVEG

```c++
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int sz = triangle.size();
        for(int i = 1; i < sz; ++i)
        {
            triangle[i].front() += triangle[i - 1].front();
            triangle[i].back() += triangle[i - 1].back();
            for(int j = 1, l = triangle[i].size(); j < l - 1; ++j)
                triangle[i][j] += min(triangle[i - 1][j], triangle[i - 1][j - 1]);
        }
        return *min_element(triangle.back().begin(), triangle.back().end());
    }
};
```

不修改原数组的O(n)空间复杂度的解法
```c++
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int sz = triangle.size();
        vector<int> dp(sz);
        dp[0] = triangle[0][0];
        for(int i = 1; i < sz; ++i)
        {
            dp[i] = dp[i - 1] + triangle[i][i]; // 第i行有i+1个元素，所以dp[i]就表示最后一个，这里需要上面一行的前一个元素加上当前元素
            for(int j = i - 1; j > 0; --j)
                dp[j] = min(dp[j], dp[j - 1]) + triangle[i][j];
            dp[0] += triangle[i][0];
        }
        return *min_element(dp.begin(), dp.end());
    }
};
```

从下往上走
```c++
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int sz = triangle.size();
        vector<int> dp;
        copy(triangle.back().begin(), triangle.back().end(), back_inserter(dp));
        for(int i = sz - 2; i >= 0; --i)
            for(int j = 0; j <= i; ++j)
                dp[j] = min(dp[j], dp[j + 1]) + triangle[i][j];
        return dp[0];
    }
};
```
