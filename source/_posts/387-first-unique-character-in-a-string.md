---
title: 387. First Unique Character in a String
date: 2021-03-16 13:24:21 +0800
categories: leetcode
---
#### [387. First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)
##### First Time
```c++
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<char, int> map;
        for(int i = 0; i < s.size(); ++i)
        {
            if(!map.emplace(s[i], i).second)
                map[s[i]] = -1; 
        }
        for(auto& ch : s)
        {
            if(map[ch] != -1)
                return map[ch];
        }
        return -1;
    }
};
```
##### Second Time
数组由于直接获取内存地址而不需要散列，是更快的O(N)
```
class Solution {
public:
    int firstUniqChar(string s) {
        int eng[26]{0};
        for(auto& ch : s)
        {
            eng[ch - 'a'] += 1;
        }
        int i = 0;
        for(auto& ch : s)
        {
            if(eng[ch - 'a'] == 1)
                return i;
            ++i;
        }
        return -1;
    }
};
```
##### 尝试只进入一次(还是很慢)
```c++
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<char, int> map;
        unordered_set<char> set;
        for(int i = 0; i < s.size(); ++i)
        {
            if(!set.emplace(s[i]).second)
            {
                map.erase(s[i]);
            }else
            {
                map[s[i]] = i;
            }
        }
        int j = map.size() ? map.begin()->second : -1;
        for (auto i = map.begin(); i != map.end(); ++i)
        {
            j = min(j, i->second);
        }
        return j;
    }
};
```
