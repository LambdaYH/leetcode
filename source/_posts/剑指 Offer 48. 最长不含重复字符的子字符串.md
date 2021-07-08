---
title: 剑指 Offer 48. 最长不含重复字符的子字符串
date: 2021-07-08 18:10:40 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 48. 最长不含重复字符的子字符串](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

##### 滑动窗口
```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_set<char> set;
        int begin = 0, end = 0;
        int ret = 0;
        while(end < s.size())
        {
            if(set.find(s[end]) == set.end())
                set.insert(s[end]);
            else
            {
                while(s[begin] != s[end])
                    set.erase(s[begin++]);
                ++begin;
            }          
            ret = max(ret, end - begin + 1);
            ++end;
        }
        return ret;
    }
};
```

##### 动态规划
```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> map;
        int ret = 0;
        int now = 0;
        for(int i = 0; i < s.size(); ++i)
        {
            if(map.find(s[i]) != map.end() && map[s[i]] >= i - now)
                now = i - map[s[i]];
            else
                now = now + 1;
            map[s[i]] = i;
            ret = max(now, ret);
        }
        return ret;
    }
};
```
