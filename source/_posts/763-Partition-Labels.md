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
            c[S[i] - 'a'] = i; // 记录每个元素最后出现的位置
        }
        int anchor = 0;
        int last = 0;
        for(int i = 0; i < S.size(); ++i)
        {
            last = max(last, c[S[i] - 'a']); // 计算当前字母出现的最后位置
            if(i == last) // 如果当前位置是最后出现的，就计算长度保存结果
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
