---
title: 10. sadasd
date: 2021-06-09 00:31:58 +0800
categories: leetcode
tags : Dynamic Programming
---
#### [10. Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)

题目:
```
Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*' where: 

'.' Matches any single character.​​​​
'*' Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).
```

这里的'*'表达有些含糊，改为Matches zero or more of the preceding character.较好

##### 递归

思路：

`.`可以匹配任何字符，因此当遇到了`.`那就是直接匹配成功，其余状况就是比较字符是否相等即可。`*`可以匹配之前的元素，0次或多次，当匹配0次的时候，那么就将原text和pattern除去这一匹配0次的模式后的部分再次进行匹配，当匹配一次或多次的时候，就在text中删去匹配成功的部分继续把剩下的和pattern匹配，由于每一都会有这2种抉择，所以采用递归，二者状况其一匹配成功即可。

当pattern为空时，当且仅到s为空才会匹配成功


```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        return helper(s, p, 0, 0);
    }
private:
    bool helper(string& s, string& p, int i, int j)
    {
        if(j >= p.size())
            return i >= s.size();
        bool firstMatch = i < s.size() && (s[i] == p[j] || p[j] == '.');
        if(j <= p.size() - 2 && p[j + 1] == '*')
            return helper(s, p, i, j + 2) || (firstMatch && helper(s, p, i + 1, j));
        else
            return firstMatch && helper(s, p, i + 1, j + 1);
    }
};
```


##### top-down dp
```c++
enum status {
    UNKNOWN,
    TRUE,
    FALSE
};
class Solution {
public:
    bool isMatch(string s, string p) {
        dp = vector<vector<status>>(s.size() + 1, vector<status>(p.size() + 1, UNKNOWN));
        return helper(0, 0, s, p);
    }
private:
    vector<vector<status>> dp;
    bool helper(int i, int j, const string& s, const  string& p)
    {
        if(dp[i][j] != UNKNOWN)
            return dp[i][j] == TRUE;
        else
        {
            if(j >= p.size())
                return i >= s.size();
            bool firstMatch = i < s.size() && (p[j] == s[i] || p[j] == '.');
            bool ret;
            if(j <= p.size() - 2 && p[j + 1] == '*')
                ret = helper(i, j + 2, s, p) || (firstMatch && helper(i + 1, j, s, p));
            else
                ret = firstMatch && helper(i + 1, j + 1, s, p);
            dp[i][j] = ret ? TRUE : FALSE;
            return ret;
        }
    }
};
```

由于递归检索过程中会出现许多的交叠，因此自然而然想到避免这种重复，所以通过dp保存起来以供后续读取，其中vector的size全都+1是防止溢出。

而且将substr的工作转为有i,j表示，避免了多次创建string

**但是这种仅仅可以避免交叠，top-down，顾名思义，从大往下走，分为一个个小问题从而解决，转而使用bottom-up，一个个小问题进行组合合成大问题**

##### bottom-up dp
```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        vector<vector<bool>> dp(s.size() + 1, vector<bool>(p.size() + 1, false)); // +1 表示了空
        dp[s.size()][p.size()] = true;
        for(int i = s.size(); i >= 0; --i) // s从空串开始匹配，因为对于*a,是可以匹配到空串的
        {
            for(int j = p.size() - 1; j >=0; --j) // 这里不用，因为当p为空时候，当且仅当s为空才为真，其他为假，而这种情况已经包含在了base中
            {
                bool firstMatch = i < s.size() && (p[j] == '.' || p[j] == s[i]);
                if(j + 1 < p.size() && p[j + 1] == '*')
                    dp[i][j] = dp[i][j + 2] || (firstMatch && dp[i + 1][j]);
                else
                    dp[i][j] = firstMatch && dp[i + 1][j + 1];
            }
        }
        return dp[0][0];
    }
};
```

base为当两者全为空的时候，匹配结果为true。

从后面往前走，当`i == 0 && j == 0`时，表示匹配了整个字符串和pattern

然后分解成小问题，对于当前dp[i][j]来说，从递归的思想引过来

1. 如果`p[j] == '.'`或`p[j] == s[i]`，那么`dp[i][j] == dp[i + 1][j + 1]`，说明当前匹配可以正常走，结果=除了这个位之后的匹配结果
2. 如果`p[j + 1] == '*'`，那么`dp[i][j] == dp[i][j + 2] || s[i] == p[j] || p[j] == '.' &&dp[i + 1][j]，这是可以匹配s[i]的0个或多个，当0个时候，这匹配没有生效，所以取后两位继续匹配的结果，当匹配多个，那么p[j]被使用了，结果就是当p[j]匹配成功后，结合后面串的匹配结果得出当前的结果。
3. 当2个长度都只有1个时候，直接比对当前的字母再结合之前的匹配结果。
