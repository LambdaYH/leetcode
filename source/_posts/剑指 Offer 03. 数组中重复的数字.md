---
title: 剑指 Offer 03. 数组中重复的数字
date: 2021-06-15 17:57:41 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 03. 数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

##### 记录
```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        vector<int> memo(nums.size());
        for(auto& num : nums)
        {
            if(memo[num])
                return num;
            else
                memo[num] = 1;
        }
        return 0;
    }
};
```
T(n) : O(n)

S(n) : O(n)

##### 排序
```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        for(int i = 1; i < nums.size(); ++i)
            if(nums[i] == nums[i - 1])
                return nums[i];
        return 0;
    }
};
```
T(n) : O(nlogn)

S(n) : O(1)

##### 用swap
```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        for(int i = 0; i < nums.size(); ++i)
        {
            while(nums[i] != i)
            {
                if(nums[i] == nums[nums[i]])
                    return nums[i];
                swap(nums[i], nums[nums[i]]);
            }
        }
        return -1;
    }
};
```

对于当走到i时，如果i处的数字不是i的话，就把这个数字移动到正确的位置nums[nums[i]]，然后对交换过来的数字继续判断是不是==i。

这样一来所有的数字都会被交换到正确的位置，当碰到重复数字时，那他一定不在正确的位置，这时候想把它交换过去的话，就会发现，唉！交换过去的位置已经有他了，那么就可以判断出来时重复了
