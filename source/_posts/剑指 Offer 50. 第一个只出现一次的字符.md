---
title: 剑指 Offer 50. 第一个只出现一次的字符
date: 2021-07-03 16:04:36 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 50. 第一个只出现一次的字符](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

##### 遍历两次
```c++
class Solution {
public:
    char firstUniqChar(string s) {
        int memo[26]{ 0 };
        for(auto& ch : s)
            memo[ch - 'a'] += 1;
        for(auto& ch : s)
            if(memo[ch - 'a'] == 1)
                return ch;
        return ' ';
    }
};
```

##### 用vector记录插入的数据，在有大量重复的情况下会笔第一种快
```c++
class Solution {
public:
    char firstUniqChar(string s) {
        int memo[26]{ 0 };
        vector<char> v;
        for(auto& ch : s)
        {
            if(!memo[ch - 'a'])
                v.push_back(ch);
            memo[ch - 'a'] += 1;
        }
        for(auto& ch : v)
            if(memo[ch - 'a'] == 1)
                return ch;
        return ' ';
    }
};
```

