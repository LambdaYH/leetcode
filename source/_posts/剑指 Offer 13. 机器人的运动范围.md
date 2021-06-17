---
title: 剑指 Offer 13. 机器人的运动范围
date: 2021-06-17 21:12:35 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

##### DFS
```c++
class Solution {
public:
    int movingCount(int m, int n, int k) {
        int maxStep = 0;
        vector<vector<bool>> memo(m, vector<bool>(n, false));
        backTrack(m, n, k, maxStep, 0, 0, memo);
        return maxStep;
    }
private:
    void backTrack(int m, int n, int k, int& maxStep, int i, int j, vector<vector<bool>>& memo)
    {
        if(i >= m || i < 0 || j >= n || j < 0 || memo[i][j])
            return;
        memo[i][j] = true;
        int sum = 0;
        int it = i, ij = j;
        while(it)
        {
            sum += it % 10;
            it /= 10;
        }
        while(ij)
        {
            sum += ij % 10;
            ij /= 10;
        }
        if(sum > k)
            return;
        else
        {
            ++maxStep;
            backTrack(m, n, k, maxStep, i + 1, j, memo);
            backTrack(m, n, k, maxStep, i - 1, j, memo);
            backTrack(m, n, k, maxStep, i, j + 1, memo);
            backTrack(m, n, k, maxStep, i, j - 1, memo);
        }
    }
};
```

##### 优化sum的计算方法
```c++
class Solution {
public:
    int movingCount(int m, int n, int k) {
        int maxStep = 0;
        vector<vector<bool>> memo(m, vector<bool>(n, false));
        backTrack(m, n, k, maxStep, 0, 0, memo, 0);
        return maxStep;
    }
private:
    void backTrack(int m, int n, int k, int& maxStep, int i, int j, vector<vector<bool>>& memo,int sum)
    {
        if(i >= m || i < 0 || j >= n || j < 0 || memo[i][j] || sum > k)
            return;
        memo[i][j] = true;
        ++maxStep;
        backTrack(m, n, k, maxStep, i + 1, j, memo, ((i + 1) % 10 != 0 ? 1 : -8) + sum);
        backTrack(m, n, k, maxStep, i, j + 1, memo, ((j + 1) % 10 != 0 ? 1 : -8) + sum);
    }
};
```

![1623937126537.png](https://image.cinte.cc/2021/06/17/5f549df3dac5e.png)
