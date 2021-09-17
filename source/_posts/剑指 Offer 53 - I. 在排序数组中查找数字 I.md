---
title: 剑指 Offer 53 - I. 在排序数组中查找数字 I
date: 2021-07-07 16:36:57 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

参考[34. Find First and Last Position of Element in Sorted Array](https://leetcode.cinte.cc/2021/03/14/34.-Find-First-and-Last-Position-of-Element-in-Sorted-Array/)

#####  直接遍历
```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int ret = 0;
        for(auto& num : nums)
            ret += num == target ? 1 : 0;
        return ret;
    }
};
```

O(n)

##### 二分
```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        if(nums.empty())
            return 0;
        int lo = 0, hi = nums.size(), mid;
        int ret = 0;
        while(lo < hi)
        {
            mid = lo + ((hi - lo) >> 1);
            if(nums[mid] == target)
            {
                ++ret;
                break;
            }
            else if(nums[mid] > target)
                hi = mid - 1;
            else
                lo = mid + 1;
        }
        int i = mid - 1;
        while(i >= 0 && nums[i--] == target)
            ++ret;
        i = mid + 1;
        while(i <= nums.size() - 1 && nums[i++] == target)
            ++ret;
        return ret;
    }
};
```

优化
```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        if(nums.empty())
            return 0;
        int lo = 0, hi = nums.size() - 1;
        while(lo < hi)
        {
            int mid = (lo + hi) >> 1;
            if(nums[mid] < target)
                lo = mid + 1;
            else
                hi = mid;
        }
        int left = hi; // 最后保留一个等于目标的左边界
        if(nums[lo] != target)
            return 0;
        hi = nums.size() - 1;
        while(lo < hi)
        {
            int mid = ((lo + hi) >> 1) + 1; // 偏向右边
            if(nums[mid] <= target)
                lo = mid;
            else
                hi = mid - 1;
        }
        // 保留一个等于左边的左边界
        return lo - left + 1;
    }
};
```

v.2
```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        if(nums.empty())
            return 0;
        int lo = 0, hi = nums.size() - 1;
        while(lo <= hi)
        {
            int mid = (lo + hi) >> 1;
            if(nums[mid] < target)
                lo = mid + 1;
            else
                hi = mid - 1;
        }
        // 当他们相等时候，进入会出现hi在lo的前面一位，即hi是左边界而lo是左边界右边一个，hi!=target而lo==target
        int left = hi;
        if(lo <= nums.size() - 1 && nums[lo] != target) // lo如果不等于的话，那就直接跳出
            return 0;
        hi = nums.size() - 1;
        while(lo <= hi)
        {
            int mid = (lo + hi) >> 1;
            if(nums[mid] <= target)
                lo = mid + 1;
            else
                hi = mid - 1;
        }
        // lo是右边界
        return lo - left - 1;
    }
};
```
