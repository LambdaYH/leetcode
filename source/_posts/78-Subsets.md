---
title: 78. Subsets
date: 2021-03-24 10:35:34 +0800
categories: leetcode
tags: BackTrack
---
#### [78. Subsets](https://leetcode.com/problems/subsets/)
##### [backTrack](https://leetcode.com/problems/combination-sum/discuss/16502/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partitioning))
 > 摘自wiki: 回溯法采用试错的思想，它尝试分步的去解决一个问题。在分步解决问题的过程中，当它通过尝试发现，现有的分步答案不能得到有效的正确的解答的时候，它将取消上一步甚至是上几步的计算，再通过其它的可能的分步解答再次尝试寻找问题的答案

##### 原
```c++
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> ret;
        ret.push_back({});
        vector<int> temp;
        for(size_t i = 1; i <= nums.size(); ++i)
            backTrack(ret, temp, nums, i, 0);
        return ret;
    }
private:
    void backTrack(vector<vector<int>>& ret, vector<int>& temp, vector<int>& nums, int n, int start)
    {
        if(temp.size() == n)
            ret.push_back(temp);
        if(temp.size() > n)
            return;
        for(size_t i = start; i < nums.size(); ++i)
        {
            temp.push_back(nums[i]);
            backTrack(ret, temp, nums, n, i + 1);
            temp.pop_back();
        }
    }
};
```
##### 改
```c++
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> ret;
        vector<int> temp;
        backTrack(ret, temp, nums, 0);
        return ret;
    }
private:
    void backTrack(vector<vector<int>>& ret, vector<int>& temp, vector<int>& nums, int start)
    {
        ret.push_back(temp);
        for(size_t i = start; i < nums.size(); ++i)
        {
            temp.push_back(nums[i]);
            backTrack(ret, temp, nums, i + 1);
            temp.pop_back();
        }
    }
};
```
