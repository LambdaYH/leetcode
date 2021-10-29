---
title: 131. Palindrome Partitioning
date: 2021-04-01 20:47:13 +0800
categories: leetcode
---
#### [131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)
```c++
class Solution {
public:
    vector<vector<string>> partition(string s) {
        int size = s.size();
        vector<vector<string>> ret;
        vector<string> temp;
        backTrack(ret, temp, s, 0);
        return ret;
    }
private:
    void backTrack(vector<vector<string>>& ret, vector<string>& temp, string& s, size_t start)
    {
        if(start > s.size() - 1)
            ret.push_back(temp);
        
        for(size_t i = start; i < s.size(); ++i)
        {
            if(isPalindrome(s.substr(start, i - start + 1)))
            {
                temp.push_back(s.substr(start, i - start + 1));
                backTrack(ret, temp, s, i + 1);
                temp.pop_back();
            }
        }
    }
    bool isPalindrome(string s) {
        auto lo = s.begin();
        auto hi = s.end() - 1;
        while(lo < hi)
        {
            if(!isAlphabet(*lo))
                ++lo;
            else if(!isAlphabet(*hi))
                --hi;
            else
            {
                if(*lo != *hi)
                    return false;
                ++lo;
                --hi;
            }
            
        }
        return true;
    }
    bool isAlphabet(char& ch)
    {
        if(ch >= 'a' && ch < 'z')
            return true;
        else
            return false;
    }
};
```

##### review
```c++
class Solution {
public:
    vector<vector<string>> partition(string s) {
        vector<string> tmp;
        backTrack(s, s.size(), 0, tmp);
        return ret;
    }
private:
    vector<vector<string>> ret;
    void backTrack(string& s, int length, int index, vector<string>& tmp)
    {
        if(index == length)
        {
            ret.emplace_back(tmp);
            return;
        }
        for(int i = index; i < length; ++i)
        {
            if(isPalindorm(s, index, i))
            {
                tmp.push_back(s.substr(index, i - index + 1));
                backTrack(s, length, i + 1, tmp);
                tmp.pop_back();
            }
        }
    }
    inline bool isPalindorm(string& s, int i, int j)
    {
        while(i < j) {
            if(s[i++] != s[j--])
                return false;
        }
        return true;
    }
};
```

但是可以发现，回溯过程中会出现许多的重复的判断回文子串，所以有2种优化策略，一是预先判断回文子串，而是在回溯过程中进行记忆。

预先判断回文子串
```c++
class Solution {
public:
    vector<vector<string>> partition(string s) {
        vector<string> tmp;
        memo.assign(s.size(), vector<int>(s.size(), 1));
        int n = s.size();
        for(int i = n - 1; i >= 0; --i)
            for(int j = i + 1; j < n; ++j)
                memo[i][j] = s[i] == s[j] && memo[i + 1][j - 1];
        backTrack(s, s.size(), 0, tmp);
        return ret;
    }
private:
    vector<vector<string>> ret;
    vector<vector<int>> memo;
    void backTrack(string& s, int length, int index, vector<string>& tmp)
    {
        if(index == length)
        {
            ret.emplace_back(tmp);
            return;
        }
        for(int i = index; i < length; ++i)
        {
            if(memo[index][i])
            {
                tmp.push_back(s.substr(index, i - index + 1));
                backTrack(s, length, i + 1, tmp);
                tmp.pop_back();
            }
        }
    }
};
```

在回溯过程中记忆
```c++
class Solution {
public:
    vector<vector<string>> partition(string s) {
        vector<string> tmp;
        memo.assign(s.size(), vector<int>(s.size()));
        backTrack(s, s.size(), 0, tmp);
        return ret;
    }
private:
    vector<vector<string>> ret;
    vector<vector<int>> memo;
    void backTrack(string& s, int length, int index, vector<string>& tmp)
    {
        if(index == length)
        {
            ret.emplace_back(tmp);
            return;
        }
        for(int i = index; i < length; ++i)
        {
            if(isPalindorm(s, index, i) == 1)
            {
                tmp.push_back(s.substr(index, i - index + 1));
                backTrack(s, length, i + 1, tmp);
                tmp.pop_back();
            }
        }
    }
    // memo[i][j] == 0为未搜索，1为是回文子串，-1为不是
    inline int isPalindorm(string& s, int i, int j)
    {
        if(memo[i][j])
            return memo[i][j];
        if(i >= j)
            return memo[i][j] = 1;
        return s[i] == s[j] ? isPalindorm(s, i + 1, j - 1) : -1;
    }
};
```
