---
title: 53. Maximum Subarray
date: 2021-03-26 17:55:01 +0800
categories: leetcode
tags: Dynamic Programming
---
#### [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
##### [Kadane算法](https://en.wikipedia.org/wiki/Maximum_subarray_problem#Kadane's_algorithm)
> Whenever you see a question that asks for the maximum or minimum of something, consider Dynamic Programming as a possibility


```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int maxNum = nums[0];
        int maxCur = nums[0];
        for(size_t i = 1; i < nums.size(); ++i)
        {
            maxCur = max(nums[i], maxCur + nums[i]);
            maxNum = max(maxNum, maxCur);
        }
        return maxNum;
    }
};
```

##### 分而知之D&Q
```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        return find(0, nums.size() - 1, nums);
    }
private:
    int find(int left, int right, vector<int>& nums)
    {
        if(left > right) return INT_MIN;
        
        int mid = (left + right) / 2;
        int cur = 0;
        int maxLeft = 0; // 如果都小于0，那就不采用那边，那么那边的和就是0
        int maxRight = 0;
        
        for(int i = mid - 1; i >= left ; --i)
        {
            cur += nums[i];
            maxLeft = max(maxLeft, cur);
        }
        
        cur = 0;
        
        for(int i = mid + 1; i <= right; ++i)
        {
            cur += nums[i];
            maxRight = max(maxRight, cur);
        }
        
        int bestCombined = nums[mid] + maxLeft + maxRight;
        int leftHalf = find(left, mid - 1, nums);
        int rightHalf = find(mid + 1, right, nums);
        
        return max(bestCombined, max(leftHalf, rightHalf));
    }
};
```

取中点，往左计算和，往右计算和，这时候有三种情况，中点是最长子串之中的元素，最长子串在中点右边，最长子串在中点左边。对于第一种情况，那就是左+右+中，对于后两种，那么再对左右子串进行同样的查找(DQ)
