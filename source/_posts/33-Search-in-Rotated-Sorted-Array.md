---
title: 33. Search in Rotated Sorted Array
date: 2021-03-20 21:27:57 +0800
categories: leetcode
---
#### [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
##### First Time
```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int sz = nums.size();
        auto bias = binarySearch(nums, 0, sz - 1);
        int lo = 0, hi = sz;
        int mid;
        while(lo < hi)
        {
            mid = (lo + hi) / 2;
            if(nums[(mid + bias) % sz] < target)
            {
                lo = mid + 1;
            }else
            {
                hi = mid;
            }
        }
        return (nums[(hi + bias) % sz] == target) ? (hi + bias) % sz : -1;

    }
private:
    int binarySearch(vector<int>& nums, size_t lo, size_t hi)
    {
        int mid;
        while (lo < hi)
        {
            mid = (lo + hi) / 2;
            if (nums[mid] > nums[hi])
            {
                lo = mid + 1;
            }
            else
            {
                hi = mid;
            }
        }
        return hi;
    }
};
```
O(logN)
