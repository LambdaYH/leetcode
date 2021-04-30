---
title: 5. Longest Palindromic Substring
date: 2021-04-23 22:23:09 +0800
categories: leetcode
---
#### [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

##### Approach 3
```c++
class Solution {
public:
    string longestPalindrome(string s) {
        pair<int, int> maxp{0, 1};
        int maxlen = 1;
        vector<vector<bool>> dp(s.size(), vector<bool>(s.size(), false));
        for(int i = 0; i < s.size(); ++i)
            dp[i][i] = true;
        for(int i = 0; i < s.size() - 1; ++i)
        {
            dp[i][i + 1] = (s[i] == s[i + 1]);
            if(dp[i][i + 1] && maxlen < 2)
            {
                maxlen = 2;
                maxp = pair<int, int>{i, 2};
            }
        }
        
        // 此处循环先j再i 是由于以下j为j - 1 而 i 为 i + 1
        // 如果先i 再 j，则i + 1永远不是i的前一任
        // 先j后i，则可以用i,i+1的base来处理
        for(int j = 1; j < s.size(); ++j)
        {
            for(int i = 0; i < j; ++i)
            {
                if(i == j || j == i + 1)
                    continue;
                dp[i][j] = dp[i + 1][j - 1] && s[i] == s[j];
                if(dp[i][j])
                {
                    maxp = j - i + 1 > maxlen ? pair<int, int>{i, j - i + 1} : maxp;   
                    maxlen = max(maxlen, maxp.second);
                }
            }
        }
        return s.substr(maxp.first, maxp.second);
    }
};
```
T(n) : O(n^2) <br>
S(n) : O(n^2)

##### approach 4
```c++
class Solution {
public:
    string longestPalindrome(string s) {
        pair<int, int> maxP;
        int maxLen = 0;
        for (int i = 0; i < s.size(); ++i)
        {
            auto lenO = extract(s, i, i);
            auto lenS = extract(s, i, i + 1);
            if (max(lenO.second, lenS.second) > maxLen)
            {
                if (lenO.second > lenS.second)
                    maxP = lenO;
                else
                    maxP = lenS;
                maxLen = maxP.second;
            }
        }
        return s.substr(maxP.first, maxP.second);
    }
private:
    pair<int, int> extract(string& s, int left, int right)
    {
        while (left >= 0 && right <= s.size() && s[left] == s[right])
        {
            --left;
            ++right;
        }
        return pair<int, int>{left + 1, right - left - 1};
    }
};
```
T(n) : O(n^2) <br>
S(n) : O(1)

##### [Approach 5: Manacher's Algorithm](https://en.wikipedia.org/wiki/Longest_palindromic_substring#Manacher's_algorithm)

