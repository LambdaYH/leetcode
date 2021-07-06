---
title: 剑指 Offer 57 - II. 和为s的连续正数序列
date: 2021-07-06 11:10:45 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 57 - II. 和为s的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

##### 暴力
```c++
class Solution {
public:
    vector<vector<int>> findContinuousSequence(int target) {
        vector<vector<int>> ret;
        for(int i = 1; i <= target >> 1; ++i)
        {
            int sum = i;
            vector<int> tmp;
            tmp.push_back(i);
            for(int j = i + 1; j < target; ++j)
            {
                tmp.push_back(j);
                sum += j;
                if(sum > target)
                    break;
                else if(sum == target)
                    ret.push_back(tmp);
            }
        }
        return ret;
    }
};
```

T(n) : O(n^2)

##### sliding window
```c++
class Solution {
public:
    vector<vector<int>> findContinuousSequence(int target) {
        int begin = 1, end = 1, sum = 0;
        vector<vector<int>> ret;
        while(begin < (target >> 1))
        {
            sum += end;
            while(sum >= target)
            {
                if(sum == target)
                {
                    vector<int> tmp;
                    for(int i = begin; i <= end; ++i)
                        tmp.push_back(i);
                    ret.push_back(tmp);
                }
                sum -= begin;
                ++begin;
            }
            ++end;
        }
        return ret;
    }
};
```

T(n) : O(n)
