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
```
T(n) : O(nlogn) <br>
S(n) : O(n)


动态规划 ： 用数组存储子问题的值，用子问题的值直接得到现在问题的值

##### BFS
```C++
class Solution {
public:
    int numSquares(int n) {
        // 整体转化为对一个图的BFS
        // 当且仅当节点I和节点J相差一个perfect square number的时候，两点连线
        int depth = 1;
        vector<bool> visited(n, false); // 访问过的点 
        vector<int> prefectNumber; 
        // 先计算低于n的所有完全平方数
        for(int i = 1; i * i <= n; ++i)
        {
            prefectNumber.push_back(i * i);
            visited[i * i - 1] = true;
        }
        // 如果n本身就是完全平方数，那就直接返回
        if(prefectNumber.back() == n)
            return 1;
        queue<int> q;
        // 这是第一圈，先把所有完全平方数push进去
        for(auto& num : prefectNumber)
            q.push(num);
        // 开始往外扩圈
        while(!q.empty())
        {
            ++depth;
            for(int i = 0, j = q.size(); i < j; ++i)
            {
                auto p = q.front();
                q.pop();
                for(auto& num : prefectNumber)
                {
                    // 首次碰到等于n的那一圈就是所要求的最小值
                    if(num + p == n)
                        return depth;
                    // 访问过的点不需要再去访问，反之去访问并把这个点加入到下一圈要访问的候选
                    else if(num + p < n && !visited[num + p - 1])
                    {
                        visited[num + p - 1] = true;
                        q.push(num + p);
                    // 大于n的节点无需访问，由于存着的完全平方数是递增的，所以可以直接跳出循环。
                    }else if(num + p > n)
                        break;
                }
            }
        }
        return 0;
    }
};
```

一圈一圈地往外找

##### math，借助[Legendre's three-square theorem](https://en.wikipedia.org/wiki/Legendre%27s_three-square_theorem)

摸了
