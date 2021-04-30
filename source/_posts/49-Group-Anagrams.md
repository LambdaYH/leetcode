---
title: 49. Group Anagrams
date: 2021-03-29 15:34:01 +0800
categories: leetcode
---
#### [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)
##### 按照排序后的字符串作为索引
```c++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> map;
        for(auto& str : strs)
        {
            string tmp{str};
            sort(str.begin(), str.end());
            map[str].push_back(tmp);                           
        }
        vector<vector<string>> ret;
        for(auto& v : map)
        {
            ret.push_back(v.second);
        }
        return ret;
    }
};
```
