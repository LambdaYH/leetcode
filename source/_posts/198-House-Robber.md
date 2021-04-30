---
title: 198. House Robber
date: 2021-04-09 17:17:44 +0800
categories: leetcode
tags: 
- Dynamic Programming
---
#### [198. House Robber](https://leetcode.com/problems/house-robber/)

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if(nums.size() == 1) return nums[0];
        vector<int> dp(nums.size());
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);
        for(int i = 2; i < nums.size(); ++i)
        {
            dp[i] = max(nums[i] + dp[i - 2], dp[i - 1]);
        }
        return dp.back();
    }
};
```
T(n) : O(n) <br>
S(n) : O(n)

##### 注意到每次只用到dp[i - 2]和dp[i - 1],用2变量优化
```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if(nums.size() == 1) return nums[0];
        int dp[2];
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);
        for(int i = 2; i < nums.size(); ++i)
        {
            dp[0] = max(nums[i] + dp[0], dp[1]);
            swap(dp[0], dp[1]);
        }
        return dp[1];
    }
};
```
T(n) : O(n) <br>
S(n) : O(1)


[dicussion中的动态规划推导步骤](https://leetcode.com/problems/house-robber/discuss/156523/From-good-to-great.-How-to-approach-most-of-DP-problems.)
