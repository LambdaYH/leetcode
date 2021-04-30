---
title: 139. Word Break
date: 2021-04-02 19:20:45 +0800
categories: leetcode
tags: Dynamic Programming
---
#### [139. Word Break](https://leetcode.com/problems/word-break/)

![](https://image.cinte.cc/2021/04/02/4e3d2b784323c.png)
##### dp
```c++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> dict;
        for(auto& word : wordDict)
        {
            dict.insert(word);
        }
        vector<bool> dp(s.size() + 1, false);
        dp[0] = true;
        for(size_t i = 1; i <= s.size(); ++i)
        {
            for(size_t j = 0; j < i; ++j)
            {
                if(dp[j] && (dict.find(s.substr(j, i - j)) != dict.end()))
                {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp.back();
    }
};
};
````
T(n) : O(n^2) ? <br>
S(n) : O(n)


动态规划 ： 用数组存储子问题的值，用子问题的值直接得到现在问题的值
