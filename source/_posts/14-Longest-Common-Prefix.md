---
title: 14. Longest Common Prefix
date: 2021-03-07 17:26:37 +0800
categories: leetcode
---
#### [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)
```c++
class Solution
{
public:
    string longestCommonPrefix(vector<string> &strs)
    {
        if (strs.empty())
        {
            return "";
        }
        int minSize = strs[0].size();
        int minSizeStrIndex = 0;
        for (std::size_t i = 0; i < strs.size(); ++i)
        {
            if (strs[i].size() < minSize)
            {
                minSize = strs[i].size();
                minSizeStrIndex = i;
            }
        }
        string chs = "";
        int bias = 0;
        for (const auto &ch : strs[minSizeStrIndex])
        {
            for (std::size_t i = 0;i < strs.size();++i)
            {
                if (i == minSizeStrIndex)
                    continue;
                if (ch != strs[i][bias])
                    return chs;
            }
            chs += ch;
            ++bias;
        }
        return chs;
    }
};
```
