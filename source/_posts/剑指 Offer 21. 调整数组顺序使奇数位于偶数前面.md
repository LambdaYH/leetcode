---
title: 剑指 Offer 21. 调整数组顺序使奇数位于偶数前面
date: 2021-06-23 17:33:07 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

##### 首尾
```C++
class Solution {
public:
    vector<int> exchange(vector<int>& nums) {
        int end = nums.size() - 1;
        for(int i = 0; i < end; ++i)
        {
            while(i < end && nums[i] % 2 == 0)
                swap(nums[i], nums[end--]);
        }
        return nums;
    }
};
```

```c++
class Solution {
public:
    vector<int> exchange(vector<int>& nums) {
        int begin = 0, end = nums.size() - 1;
        while(begin < end)
        {
            if(nums[begin] & 1)
                ++begin;
            else if(!(nums[end] & 1))
                --end;
            else
                swap(nums[begin], nums[end]);
        }
        return nums;
    }
};
```

##### 快慢
```c++
class Solution {
public:
    vector<int> exchange(vector<int>& nums) {
        int walker = 0, runner = 0;
        while(runner < nums.size())
        {
            if(nums[runner] & 1)
                swap(nums[walker++], nums[runner]);
            ++runner;
        }
        return nums;
    }
};
```
