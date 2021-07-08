---
title: 剑指 Offer 53 - II. 0～n-1中缺失的数字
date: 2021-07-08 16:35:31 +0800
categories: leetcode
mathjax: false
---
#### [剑指 Offer 53 - II. 0～n-1中缺失的数字](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)

##### 遍历
```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        for(int i = 0; i < n; ++i)
            if(nums[i] != i)
                return i;
        return n;
    }
};
```

排序数组中的搜索问题，首先想到 二分法 解决。

##### 二分
```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        int lo = 0, hi = n;
        while(lo < hi)
        {
            int mid = lo + ((hi - lo) >> 1);
            if(nums[mid] != mid)
                hi = mid;
            else
                lo = mid + 1;
        }
        return hi;
    }
};
```
