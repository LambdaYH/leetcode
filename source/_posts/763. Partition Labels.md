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
            last = max(last, c[S[i] - 'a']); // 计算之前子串中出现的字母的最后的位置
            if(i == last) // 如果这个条件成立了，表示当前子串(anchor - i)中的所有字母都只出现过了一次，并且之后不会再出现了，所以开始i计算并保存结果。
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
