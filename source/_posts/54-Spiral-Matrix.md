---
title: 54. Spiral Matrix
date: 2021-04-08 19:55:40 +0800
categories: leetcode
tags: 
- Array
---
#### [54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> ret;
        int m = matrix.size();
        int n = matrix[0].size();
        int bL = 0, bR = n - 1, bU = 0, bB = m - 1;
        while(bL <= bR && bU <= bB)
        {
            for(int i = bL; i <= bR; ++i)
                ret.push_back(matrix[bU][i]);
            for(int i = bU + 1; i <= bB; ++i)
                ret.push_back(matrix[i][bR]);
            if(bU < bB && bL < bR)
            {
                for(int i = bR - 1; i > bL; --i)
                    ret.push_back(matrix[bB][i]);
                for(int i = bB; i > bU; --i)
                    ret.push_back(matrix[i][bL]);                
            }
            ++bL;
            --bR;
            ++bU;
            --bB;
        }
        return ret;
    }
};
```

螺旋

T(n) : O(n) <br>
S(n) : O(n)


还有一种思路是把走过的路都设为障碍，每次要撞过去了就改变方向。不管如何，就是直接撞过去，撞到就变向，四个方向依次变
```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if(matrix.empty())
            return {};
        int n = matrix.size(), m = matrix[0].size();
        vector<vector<int>> visisted(n, vector<int>(m, 0));
        int d[4][4]{{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        int dr = 0;
        vector<int> ret;
        int i = 0, j = 0;
        while(1)
        {
            int nexti = i + d[dr][0];
            int nextj = j + d[dr][1];
            if(nexti < 0 || nextj < 0 || nexti >= n || nextj >= m || visisted[nexti][nextj])
                dr = (dr + 1) % 4;
            ret.push_back(matrix[i][j]);
            visisted[i][j] = 1;
            i += d[dr][0];
            j += d[dr][1];
            if(ret.size() == m * n)
                break;
        }
        return ret;
    }
};
```
T(n) : O(n) <br>
S(n) : O(n * m)
