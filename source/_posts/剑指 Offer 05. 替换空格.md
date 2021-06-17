---
title: 剑指 Offer 05. 替换空格
date: 2021-06-17 17:32:40 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 05. 替换空格](2021-06-17 17:32:37 +0800)

##### 遍历替换
```c++
class Solution {
public:
    string replaceSpace(string s) {
        string ret = "";
        for(auto& ch : s)
            if(ch == ' ')
                ret += "%20";
            else
                ret += ch;
        return ret;
    }
};
```

##### 原地替换
```c++
class Solution {
public:
    string replaceSpace(string s) {
        int len = s.size();
        int spaceCount = 0;
        for(auto& ch : s)
            if(ch == ' ')
                ++spaceCount;
        s.resize(s.size() + 2 * spaceCount);
        for(int i = len - 1,j = s.size() - 1; i >= 0; --i, --j)
        {
            if(s[i] != ' ')
                s[j] = s[i];
            else
            {
                s[j] = '0';
                s[j - 1] = '2';
                s[j - 2] = '%';
                j -= 2;
            }
        }
        return s;
    }
};
```
