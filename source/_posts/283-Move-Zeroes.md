---
title: 283. Move Zeroes
date: 2021-04-14 16:51:52 +0800
categories: leetcode
tags: 
- Array
---
#### [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/)

两步：
1. 保持原顺序
2. 零在最后面
   
总体思路<br>
先实现1后实现2，需要认识到如下之点

The 2 requirements of the question are:

1. Move all the 0's to the end of array.

2. All the non-zero elements must retain their original order.

It's good to realize here that both the requirements are mutually exclusive, i.e., you can solve the individual sub-problems and then combine them for the final solution.

##### 很直观的方法，但有时也是非常好用的办法。
```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int sz = nums.size();
        int numOfZero = 0;
        for(auto& num : nums)
        {
            numOfZero += (num == 0);
        }
        vector<int> ans;
        for(auto& num :nums)
        {
            if(num != 0)
                ans.push_back(num);
        }
        
        for(int i = 0; i < sz - numOfZero; ++i)
        {
            nums[i] = ans[i];
        }
        fill(nums.begin() + sz - numOfZero, nums.end(), 0);
    }
};
```
T(n) : O(n) <br>
S(n) : O(n)

##### 对上述方法优化空间占用
```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int noZeroIndex = 0;
        for(auto& num :nums)
        {
            if(num != 0)
                nums[noZeroIndex++] = num;
        }
        fill(nums.begin() + noZeroIndex, nums.end(), 0);
    }
};
```
T(n) : O(n)
S(n) : O(1)

##### 再优化，由于上面需要执行完N次操作，还可以优化
```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int noZeroIndex = 0;
        for(auto& num :nums)
        {
            if(num != 0)
                swap(nums[noZeroIndex++], num);
        }
    }
};
```
T(n) : O(n) <br>
S(n) : O(1) <br>

这里仅需要执行非0的个数

由于noZeroIndex和num不同时，noZeroIndex指向的必定是0元素，这时与num进行交换就可以将0元素移动到后头，依次往复，所有的0都会跑到后面去
