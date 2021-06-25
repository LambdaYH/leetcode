---
title: 剑指 Offer 19. 正则表达式匹配
date: 2021-06-25 15:54:15 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 19. 正则表达式匹配](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/)

##### 虽然做过 但还是难
参考[10. Regular Expression Matching](https://leetcode.cinte.cc/2021/05/11/10.%20Regular%20Expression%20Matching/)

```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        vector<vector<bool>> dp(s.size() + 1, vector<bool>(p.size() + 1, false));
        dp.back().back() = true;
        for(int i = s.size(); i >= 0; --i)
        {
            for(int j = p.size() - 1; j >= 0; --j)
            {
                bool firstMatch = i < s.size() && (s[i] == p[j] || p[j] == '.');  // 空串是不可能和正则中的值匹配的，所以i==s.size()时匹配始终失败
                if(j <= p.size() - 2 && p[j + 1] == '*')
                    dp[i][j] = dp[i][j + 2] || (firstMatch && dp[i + 1][j]); // 这里可以处理到空串的情况
                else
                    dp[i][j] = firstMatch && dp[i + 1][j + 1];
            }
        }
        return dp[0][0];
    }
};
```
