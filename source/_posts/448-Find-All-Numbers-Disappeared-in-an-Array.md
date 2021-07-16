---
title: 448. Find All Numbers Disappeared in an Array
date: 2021-04-12 21:17:46 +0800
categories: leetcode
tags: 
- Array
---
#### [448. Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)

##### 抄的discussion

使用原数列中的坐标是否为负来表征当前坐标所代表的值是否存在。由此使得S(n) = O(n)

聪明啊！

```c++
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        for(int i = 0; i < nums.size(); ++i)
        {
            // 下述操作也类似一个哈希表
            int m = abs(nums[i]) - 1; // 当前的数字，对应的角标，由于可能之前被操作为负的，所以要绝对值
            nums[m] = nums[m] > 0 ? -nums[m] : nums[m];  // 角标对应过去的为负，表示那个被记录到了
        }
        vector<int> ret;
        for(int i = 0; i < nums.size(); ++i)
        {
            if(nums[i] > 0)
                ret.push_back(i + 1);
        }
        return ret;
    }
};
```

##### review
```c++
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        int n = nums.size();
        vector<int> ret;
        for(int i = 0; i < n; ++i)
        {
            while(nums[i] >= 1 && nums[i] <= n && nums[i] != nums[nums[i] - 1])
                swap(nums[i], nums[nums[i] - 1]);
        }
        for(int i = 0; i < n; ++i)
            if(nums[i] != i + 1)
                ret.push_back(i + 1);
        return ret;
    }
};
```
