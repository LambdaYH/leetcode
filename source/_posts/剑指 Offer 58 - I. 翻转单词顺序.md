---
title: 剑指 Offer 58 - I. 翻转单词顺序
date: 2021-07-07 16:26:51 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 58 - I. 翻转单词顺序](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/submissions/)

##### 
```c++
class Solution {
public:
    string reverseWords(string s) {
        if(s.empty())
            return "";
        string ret = "";
        int end = s.size() - 1;
        while(end >= 0 && s[end] == ' ')
            --end;
        if(end < 0)
            return "";
        for(int i = end; i >= -1; --i)
        {
            if(i == -1 || s[i] == ' ')
            {
                ret.append(s.substr(i + 1, end - i));
                while(i >= 0 && s[i] == ' ')
                    --i;
                end = i;
                if(end < 0)
                    break;
                ret.append(" ");
            }
        }
        return ret;
    }
};
```

T(n) : O(n)

S(n) : O(n)
