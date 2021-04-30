---
title: 22. Generate Parentheses
date: 2021-03-19 21:17:29 +0800
categories: leetcode
---
#### [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)
这道题很硬核的使用了多种递归的方法

##### 递归 Brute Force
```c++
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> ret;
        genrateAll(string(2*n, ' '), 0, ret);
        return ret;
    }
private:
    void genrateAll(string s, int pos, vector<string>& ret)
    {
        if(pos == s.size())
        {
            if(isValid(s))
                ret.push_back(s);
        }else
        {
            s[pos] = '(';
            genrateAll(s, pos + 1, ret);
            s[pos] = ')';
            genrateAll(s, pos + 1, ret);
        }
    }
    
    bool isValid(string s)
    {
        int count = 0;
        for(auto& ch : s)
        {
            if(ch == '(')
                ++count;
            else
                --count;
            
            if(count < 0) 
                return false;
        }
        return count == 0;
    }
};
```
枚举出所有情况，然后对每种情况判断是否是合法的括号对，用到了[20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)中的思路

##### BackTracking
```c++
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> ret;
        backTracking(ret, 0, 0, "", n);
        return ret;
    }
private:
    void backTracking(vector<string>& ret, int open, int close, string s, int n)
    {
        if(s.size() == n*2)
        {
            ret.push_back(s);
            return;
        }
        
        if(open < n)
        {
            backTracking(ret, open + 1, close, s + "(", n);
        }
        if(open > close)
        {
            backTracking(ret, open, close + 1, s + ")", n);
        }
    }
};
```
仅仅当括号符合添加的条件时才添加这个括号。

##### Closure Number
```c++
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> ret;
        if(n == 0) ret.push_back("");
        for(int c = 0; c < n; ++c)
        {
            for(auto& left : generateParenthesis(c))
                for(auto& right : generateParenthesis(n - c - 1))
                    ret.push_back("(" + left + ")" + right);
        }
        return ret;
    }
};
```
第一个
n == 0 时添加一个""是为了让他可以进入一次循环计算右边项而不是直接return <br>
c = (2c + 1 - 0 - 1）/2 <br>
n - c - 1 = (2n - 2c - 1 - 1)/2 <br>
