---
title: 40. Combination Sum II
date: 2021-03-23 16:46:27 +0800
categories: leetcode
tags: BackTrack
---
#### [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)
```c++
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        vector<vector<int>> ret;
        sort(candidates.begin(), candidates.end());
        vector<int> temp;
        backTrack(ret, candidates, temp, target, 0);
        return ret;
    }
private:
    void backTrack(vector<vector<int>>& ret,vector<int>& candidates, vector<int>& temp, int remain, int start)
    {
        if(remain < 0)
            return;
        if(remain == 0)
        {
            ret.push_back(temp);
            return;
        }
        for(size_t i = start; i < candidates.size(); ++i)
        {
            temp.push_back(candidates[i]);
            backTrack(ret, candidates, temp, remain - candidates[i], i + 1);
            temp.pop_back();
            while(i+1 < candidates.size() && candidates[i] == candidates[i+1])
                ++i;
        }
    }
};
```
