---
title: 39. Combination Sum
date: 2021-03-23 11:54:32 +0800
categories: leetcode
tags: BackTrack
---
#### [39. Combination Sum](https://leetcode.com/problems/combination-sum/)
##### [backTrack](https://leetcode.com/problems/combination-sum/discuss/16502/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partitioning))
 > 摘自wiki: 回溯法采用试错的思想，它尝试分步的去解决一个问题。在分步解决问题的过程中，当它通过尝试发现，现有的分步答案不能得到有效的正确的解答的时候，它将取消上一步甚至是上几步的计算，再通过其它的可能的分步解答再次尝试寻找问题的答案
 
```c++
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> ret;
        vector<int> temp;
        backTrack(ret, candidates, temp, target, 0);
        return ret;
    }
private:
    void backTrack(vector<vector<int>>& ret, vector<int>& candidates, vector<int>& temp, int remain, int start) 
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
            backTrack(ret, candidates, temp, remain - candidates[i], i);
            temp.pop_back();
        }
    }
};
```
