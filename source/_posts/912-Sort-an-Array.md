---
title: 912. Sort an Array
date: 2021-03-15 16:07:30 +0800
categories: leetcode
---
#### [912. Sort an Array](https://leetcode.com/problems/sort-an-array/)
##### QuickSort
```c++
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        sort(nums, 0, nums.size() - 1);
        return nums;
    }
private:
    int partition(vector<int> &nums, int lo, int hi)
    {
        int i = lo, j = hi + 1;
        int v = nums[lo];
        while(true)
        {
            while(v > nums[++i] && i != hi);
            while(v < nums[--j] && j != lo);
            if(i >= j)
                break;
            swap(nums[i], nums[j]);
        }
        swap(nums[lo], nums[j]);
        return j;
    }

    void sort(vector<int> &nums, int lo, int hi)
    {
        if(lo >= hi)
            return;
        int j = partition(nums, lo, hi);
        sort(nums, lo, j - 1);
        sort(nums, j + 1, hi);
    }
};
```
