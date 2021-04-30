---
title: 16. 3Sum Closest
date: 2021-03-17 21:05:24 +0800
categories: leetcode
---
#### [16. 3Sum Closest](https://leetcode.com/problems/3sum-closest/)
##### refer [3sum](https://blog.cinte.cc/2021/03/11/15-3Sum/)
##### Solution 1( 2 points)
```c++
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());
        int diff = INT_MAX;
        for(size_t i = 0; i < nums.size() && diff != 0; ++i)
        {
            int lo = i + 1, hi = nums.size() - 1;
            while(lo < hi)
            {
                int sum = nums[i] + nums[lo] + nums[hi];
                if(abs(sum - target) < abs(diff))
                {
                    diff = sum - target;
                }
                if(sum < target)
                    ++lo;
                else
                    --hi;
            }
        }
        return diff + target;
    }
};
```
