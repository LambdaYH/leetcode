---
title: 剑指 Offer 57. 和为s的两个数字
date: 2021-07-05 19:29:16 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 57. 和为s的两个数字](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

##### 借助two sum的思路
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_set<int> set;
        for(auto& num : nums)
        {
            if(set.find(target - num) != set.end())
                return {num, target - num};
            else
                set.insert(num);
        }  
        return {};
    }
};
```

T(n) : O(n)

S(n) : O(n)

##### 利用好递增顺序，双指针
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int lo = 0, hi = nums.size() - 1;
        while(lo < hi)
        {
            if(nums[lo] + nums[hi] > target)
                --hi;
            else if(nums[lo] + nums[hi] < target)
                ++lo;
            else
                return {nums[lo], nums[hi]};
        }
        return {};
    }
};
```
T(n) : O(n)

S(n) : O(1)

```
提醒一下，判断条件最好不要用相加后的结果，应该用target - nums[i] 跟 nums[j]比较，这样保证不会溢出。虽然这题中不会出错。同样的例子还有二分查找，(left + right) / 2 可以用left + ((rigth - left) >> 1))代替
```
