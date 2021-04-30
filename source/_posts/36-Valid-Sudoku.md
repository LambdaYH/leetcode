---
title: 36. Valid Sudoku
date: 2021-03-23 11:07:19 +0800
categories: leetcode
---
#### [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)
```c++
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        auto sz = board.size();
        int row[9][9]{0};
        int col[9][9]{0};
        int block[3][3][9]{0};
        for(size_t i = 0; i < 9; ++i)
        {
            for(size_t j = 0; j < 9; ++j)
            {
                auto num = board[i][j];
                if(num != '.')
                {
                    if(row[i][num - 49] == 1)
                        return false;
                    else
                        row[i][num - 49] += 1;
                    
                    if(col[num - 49][j] == 1)
                        return false;
                    else
                        col[num - 49][j] += 1;

                    if(block[i / 3][j / 3][num - 49] == 1)
                        return false;
                    else
                        block[i / 3][j / 3][num - 49] += 1;
                }
            }
        }
        return true;
    }
};
```
T : O(1)
S : O(1)

##### more
```c++
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        auto sz = board.size();
        int row[9][9]{0};
        int col[9][9]{0};
        int block[3][3][9]{0};
        for(size_t i = 0; i < 9; ++i)
        {
            for(size_t j = 0; j < 9; ++j)
            {
                auto num = board[i][j];
                if(num != '.')
                {
                    if(row[i][num - 49] || col[num - 49][j] || block[i / 3][j / 3][num - 49])
                        return false;
                    else
                        row[i][num - 49] = col[num - 49][j] = block[i / 3][j / 3][num - 49] =  1;
                }
            }
        }
        return true;
    }
};
```
