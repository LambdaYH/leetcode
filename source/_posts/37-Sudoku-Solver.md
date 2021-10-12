---
title: 37. Sudoku Solver
date: 2021-03-25 21:25:23 +0800
categories: leetcode
tags: BackTrack
---
#### [37. Sudoku Solver](https://leetcode.com/problems/sudoku-solver/)
```c++
class Solution {
public:
    void solveSudoku(vector<vector<char>>& board) {
        for(size_t i = 0; i < 9; ++i)
        {
            for(size_t j = 0; j < 9; ++j)
            {
                auto& num = board[i][j];
                if(num != '.')
                {
                    col[num - 49][j] += 1;
                    row[i][num - 49] += 1;
                    block[i / 3][j / 3][num - 49] += 1;
                }
            }
        }
        solve(board, 0, 0);
        
    }
    
private:
    int col[9][9]{0};
    int row[9][9]{0};
    int block[3][3][9]{0};
    bool valid(size_t i, size_t j, int target)
    {
        if(col[target][j] || row[i][target] || block[i / 3 ][j /3][target])
            return false;
        else
            return true;
    }
    bool solve(vector<vector<char>>& board, int i, int j)
    {
        if(i == 9) return true;
        if(j == 9)
            return solve(board, i + 1, 0);
        if(board[i][j] != '.') 
            return solve(board, i, j + 1);
        
        for(char c = '1'; c <= '9'; ++c)
        {
            auto& num = board[i][j];
            if(valid(i, j, c - 49))
            {
                num = c;
                col[num - 49][j] = row[i][num - 49] = block[i / 3 ][j /3][num - 49] = 1;
                if(solve(board, i, j + 1))
                    return true;
                col[num - 49][j] = row[i][num - 49] = block[i / 3 ][j /3][num - 49] = 0;
                num = '.';
            }
        }
        return false;
    }
};
```
T(n) : O(N) 

也是一个回溯的问题，但与combined sum不同的是这个回溯只得使用return 来作为停止条件，而combined sum中则以添加到vector中为结束。

##### review
```c++
class Solution {
public:
    void solveSudoku(vector<vector<char>>& board) {
        for(int i = 0; i < 9; ++i)
            for(int j = 0; j < 9; ++j)
            {
                if(board[i][j] != '.')
                {
                    int num = board[i][j] - '0' - 1;
                    cols[j][num] = 1;
                    rows[i][num] = 1;
                    blocks[i / 3 + j / 3 * 3][num] = 1;
                }
            }
        backTrack(board, 0, 0);
    }
private:
    int cols[9][9]{};
    int rows[9][9]{};
    int blocks[9][9]{};
    bool backTrack(vector<vector<char>>& board, int i, int j)
    {
        if(j == 9)
            return backTrack(board, i + 1, 0);
        if(i == 9)
            return true;
        if(board[i][j] != '.')
            return backTrack(board, i, j + 1);
        for(int k = 1; k <= 9; ++k)
        {
            if(cols[j][k - 1] || rows[i][k - 1] || blocks[i / 3 + j / 3 * 3][k - 1])
                continue;
            board[i][j] = k + '0';
            cols[j][k - 1] = 1;
            rows[i][k - 1] = 1;
            blocks[i / 3 + j / 3 * 3][k - 1] = 1;
            if(backTrack(board, i, j + 1))
                return true;
            board[i][j] = '.';
            cols[j][k - 1] = 0;
            rows[i][k - 1] = 0;
            blocks[i / 3 + j / 3 * 3][k - 1] = 0;
        }
        // 当所有填法都不行时，说明这种出问题了，就得回溯取消上面的步骤
        return false;
    }
};
```
