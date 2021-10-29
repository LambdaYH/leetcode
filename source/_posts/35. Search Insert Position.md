---
title: 35. Search Insert Position
date: 2021-03-22 15:19:26 +0800
categories: leetcode
---
#### [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)
```c++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        size_t lo = 0, hi = nums.size();
        while(lo < hi)
        {
            size_t mid = (lo + hi) / 2;
            if(nums[mid] < target)
            {
                lo = mid + 1;
            }else
            {
                hi = mid;
            }
        }
        return hi;
    }
};
```
T(n) : O(logN) <br>
S(n) : O(1)

