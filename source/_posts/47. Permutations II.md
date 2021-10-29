---
title: 47. Permutations II
date: 2021-03-26 12:16:13 +0800
categories: leetcode
tags: BackTrack
---
#### [47. Permutations II](https://leetcode.com/problems/permutations-ii/)
```c++
class Solution {
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<vector<int>> ret;
        sort(nums.begin(), nums.end());
        int num[8]{ 0 };
        vector<int> temp;
        backTrack(ret, nums, temp , num);
        return ret;
    }
private:
    void backTrack(vector<vector<int>>& ret, const vector<int>& nums, vector<int>& temp, int* num)
    {
        if(temp.size() == nums.size())
            ret.push_back(temp);
        for(size_t i = 0; i < nums.size(); ++i)
        {
            if(num[i]) continue;
            temp.push_back(nums[i]);
            num[i] = 1;
            backTrack(ret, nums, temp, num);
            temp.pop_back();
            num[i] = 0;
            while(i + 1 < nums.size() && nums[i] == nums[i + 1]) // 重点。从重复串的第一个元素搜索已经可以获得获得重复串的全排列结果了，所以防止后面重复得到，就跳过。也就是说，重复字符串的元素只会顺位取而不会掉头。也就是说，如果有重复的，那么搜索起点一样，肯定会重复，所以要剔除
            // 补充：他无法掉头取导致了如果他们在结果中连续，就必然只有一种排列方式。如果他们在结果被其他数字隔开来，那么必然隔开来的每段中的连续部分必然唯一，而且所有隔开来的段也必然唯一，因为如果要去后面的和前面相同的段的话，前面的段必然是已经使用过了，如果没使用，就说明被回溯了，就说明接下来的数字已经跳过了当前重复数字。
                ++i;
        }
    }
};
```

Another BackTrack
