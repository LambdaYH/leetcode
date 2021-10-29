---
title: 75. Sort Colors
date: 2021-04-06 14:54:16 +0800
categories: leetcode
tags: 
- sort
---
#### [75. Sort Colors](https://leetcode.com/problems/sort-colors/)

```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        sort(nums, 0, nums.size() - 1);
    }
private:
    void sort(vector<int>& nums, int lo, int hi)
    {
        if(lo >= hi) return;
        int j = partition(nums, lo, hi);
        sort(nums, lo, j - 1);
        sort(nums, j + 1, hi);
    }
    int partition(vector<int>& nums, int lo, int hi)
    {
        int i = lo, j = hi + 1;
        int v = nums[lo];
        while(true)
        {
            while(i < hi && nums[++i] < v) {}
            while(lo < j && nums[--j] > v) {}
            if(i >=j ) break;
            swap(nums[i], nums[j]);
        }
        swap(nums[lo], nums[j]);
        return j;
    }
};
```

快速排序算法，每次取一个数为v，将所有大于v的数放在v右边，小于V的数放在v左边，最后将选择的数放到正确位置上，再对剩下的2个进行分而治之

##### 针对具体问题的解决方法
```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int second = nums.size() - 1;
        int zero = 0;
        for(int i = 0; i < nums.size(); ++i)
        {
            while(nums[i] == 2 && i < second)
                swap(nums[i], nums[second--]);
            while(nums[i] == 0 && i > zero)
                swap(nums[i], nums[zero++]);
        }
    }
};
```
总体思路是将0移到最前面，将2移到最后面

这里`==2`必须放在`==0`之前，因为2为最大的，将2换到最后去，换回来的只可能比2小，会有可能是0，需要处理。若0在前，则2换完后的0得不到处理。
