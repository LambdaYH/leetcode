---
title: 79. Word Search
date: 2021-04-07 16:55:11 +0800
categories: leetcode
tags: 
- BackTrack
---
#### [79. Word Search](https://leetcode.com/problems/word-search/)

##### backtrack
```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        for(int i = 0; i < board.size(); ++i)
        {
            for(int j = 0; j < board[0].size(); ++j)
            {
                if(word[0] == board[i][j])
                {
                    board[i][j] -= 65;
                    if(backTrack(board, word.substr(1), i ,j))
                        return true;
                    board[i][j] += 65;
                }     
            }
        }
        return false;
    }
private:
    bool backTrack(vector<vector<char>>& board, string word, int i, int j)
    {
        if(word == "")
            return true;
        if(i > 0 && word[0] == board[i - 1][j])
        {
            board[i - 1][j] -= 65;
            if(backTrack(board, word.substr(1), i - 1, j))
                return true;
            board[i - 1][j] += 65;
        }
        if(j > 0 && word[0] == board[i][j - 1])
        {
            board[i][j - 1] -= 65;
            if(backTrack(board, word.substr(1), i, j - 1))
                return true;
            board[i][j - 1] += 65;
        }
        if(i < board.size() - 1 && word[0] == board[i + 1][j])
        {
            board[i + 1][j] -= 65;
            if(backTrack(board, word.substr(1), i + 1, j))
                return true;
            board[i + 1][j] += 65;
        }
        if(j < board[0].size() - 1 && word[0] == board[i][j + 1])
        {
            board[i][j + 1] -= 65;
            if(backTrack(board, word.substr(1), i, j + 1))
                return true;
            board[i][j + 1] += 65;
        }
        return false;
    }
};
```
T(n) : O(n^2)<br>
S(n) : O(1)

一点开始搜索其周围

##### 优化
```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        for(int i = 0; i < board.size(); ++i)
        {
            for(int j = 0; j < board[0].size(); ++j)
            {
                if(word[0] == board[i][j])
                    if(backTrack(board, word, i ,j, 1))
                        return true;   
            }
        }
        return false;
    }
private:
    bool backTrack(vector<vector<char>>& board, string& word, int i, int j, int index)
    {
        if(index == word.size())
            return true;
        board[i][j] -= 65;
        if(i > 0 && word[index] == board[i - 1][j])
        {
            if(backTrack(board, word, i - 1, j, index + 1))
                return true;
        }
        if(j > 0 && word[index] == board[i][j - 1])
        {
            if(backTrack(board, word, i, j - 1, index + 1))
                return true;
        }
        if(i < board.size() - 1 && word[index] == board[i + 1][j])
        {
            if(backTrack(board, word, i + 1, j, index + 1))
                return true;
        }
        if(j < board[0].size() - 1 && word[index] == board[i][j + 1])
        {
            if(backTrack(board, word, i, j + 1, index + 1))
                return true;
        }
        board[i][j] += 65;
        return false;
    }
};
```

##### review
```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        for(int i = 0; i < board.size(); ++i)
            for(int j = 0; j < board[0].size(); ++j)
            {
                if(backTrack(board, i, j, word, 0))
                    return true;
            }
        return false;
    }
private:
    bool backTrack(vector<vector<char>>& board,int i, int j, string& word, int index)
    {
        if(board[i][j] < 'A')
            return false;
        if(board[i][j] == word[index])
        {
            board[i][j] -= 'A';
            bool ret = (i > 0 && backTrack(board, i - 1, j, word, index + 1))
                    || (i < board.size() - 1 && backTrack(board, i + 1, j, word, index + 1))
                    || (j > 0 && backTrack(board, i, j - 1, word, index + 1))
                    || (j < board[0].size() - 1 && backTrack(board, i, j + 1, word, index + 1))
                    || (index == word.size() - 1);
            board[i][j] += 'A';
            return ret;
        }else
            return false;
    }
};
```

##### review again
```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        int m = board.size(), n = board[0].size();
        for(int i = 0; i < m; ++i)
            for(int j = 0; j < n; ++j)
                if(search(board, i, j, m, n, word, 0))
                    return true;
        return false;
    }
private:
    bool search(vector<vector<char>>& board,int i, int j, const int& m, const int& n, string& word, int index)
    {
        if(index >= word.size())
            return true;
        if(i >= m || i < 0 || j >= n || j < 0 || board[i][j] < 'A' || word[index] != board[i][j])
            return false;
        board[i][j] -= 'A';
        auto ret = search(board, i + 1, j, m, n, word, index + 1)
                || search(board, i - 1, j, m, n, word, index + 1)
                || search(board, i, j + 1, m, n, word, index + 1)
                || search(board, i, j - 1, m, n, word, index + 1);
        board[i][j] += 'A';
        return ret;
    }
};
```
