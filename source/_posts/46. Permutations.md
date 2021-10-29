---
title: 46. Permutations
date: 2021-03-25 22:03:18 +0800
categories: leetcode
tags: BackTrack
---
#### [46. Permutations](https://leetcode.com/problems/permutations/)
```c++
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> ret;
        vector<int> temp;
        int num [6]{ 0 };
        backTrack(nums, ret, temp, num);
        return ret;
    }
private:
    void backTrack(vector<int>& nums, vector<vector<int>>& ret, vector<int>& temp, int* num)
    {
        if(temp.size() == nums.size())
            ret.push_back(temp);
        for(size_t i = 0; i < nums.size(); ++i)
        {
            if(num[i]) continue;
            num[i] = 1;
            temp.push_back(nums[i]);
            backTrack(nums, ret, temp, num);
            temp.pop_back();
            num[i] = 0;
        }
    }
};
```
