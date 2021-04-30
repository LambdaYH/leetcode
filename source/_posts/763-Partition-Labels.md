---
title: 763. Partition Labels
date: 2021-04-14 20:26:39 +0800
categories: leetcode
tags: 
- Greedy
---
#### [763. Partition Labels](https://leetcode.com/problems/partition-labels/)

##### 我好菜
```c++
class Solution {
public:
    vector<int> partitionLabels(string S) {
        int c[26];
        vector<int> ret;
        for(int i = 0; i < S.size(); ++i)
        {
            c[S[i] - 'a'] = i;
        }
        int anchor = 0;
        int last = 0;
        for(int i = 0; i < S.size(); ++i)
        {
            last = max(last, c[S[i] - 'a']);
            if(i == last)
            {
                ret.push_back(last + 1 - anchor);
                anchor = last + 1;
            }
        }
        return ret;
        
    }
};
```
每走到一步就判断他的最后一位，差不多就寻求一个最大区间
