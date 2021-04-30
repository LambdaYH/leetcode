---
title: 152. Maximum Product Subarray
date: 2021-04-13 11:53:48 +0800
categories: leetcode
tags: 
- Array
- Dynamic Programming
---
#### [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)

##### 仿kadane算法
```c++
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int maxSoFar = nums[0];
        
        int maxEndHere = nums[0];
        int minEndHere = nums[0];
        for(auto i = nums.begin() + 1; i != nums.end(); ++i)
        {
            int num = *i;
            if(num < 0)
                swap(maxEndHere, minEndHere);
            
            maxEndHere = max(num, maxEndHere * num);
            minEndHere = min(num, minEndHere * num);
            
            maxSoFar = max(maxEndHere, maxSoFar);
        }
        return maxSoFar;
    }
};
```

##### 另一种思路
```c++
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int maxNum{ nums[0] };
        int product{ 1 };
        for(auto i = nums.begin(); i != nums.end(); ++i)
        {
            maxNum = max(maxNum, product *= *i);
            if(!*i) product = 1;
        }
        product = 1;
        for(auto i = nums.end() - 1; i != nums.begin(); --i)
        {
            maxNum = max(maxNum, product *= *i);
            if(!*i) product = 1;
        }
        return maxNum;
    }
};
```

当负数的个数为偶数时，全乘起来就是最大，为奇数时，需要抛弃一个 <br>
每次的乘法，最大的乘积受到最后一个负数的限制
