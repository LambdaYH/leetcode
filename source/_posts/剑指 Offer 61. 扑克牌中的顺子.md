---
title: 剑指 Offer 61. 扑克牌中的顺子
date: 2021-07-11 16:27:03 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 61. 扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

#####
两个条件

1. 最大值减去最小值<5

2. 没有重复的数字

```c++
class Solution {
public:
    bool isStraight(vector<int>& nums) {
        int ma = 0, mi = 14;
        unordered_set<int> set;
        for(auto& num : nums)
        {
            if(num == 0)
                continue;
            if(!set.emplace(num).second)
                return false;
            ma = max(ma, num);
            mi = min(mi, num);
        }
        return ma - mi < 5;
    }
};
```

法2

```c++
class Solution {
public:
    bool isStraight(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int nz = 0;
        while(nums[nz] == 0)
            ++nz;
        for(int i = nz + 1; i < nums.size(); ++i)
            if(nums[i] == nums[i - 1])
                return false;
        return nums.back() - nums[nz] < 5;
    }
};
```
