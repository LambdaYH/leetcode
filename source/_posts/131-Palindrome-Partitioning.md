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
