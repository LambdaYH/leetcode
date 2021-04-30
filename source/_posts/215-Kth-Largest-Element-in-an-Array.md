---
title: 215. Kth Largest Element in an Array
date: 2021-04-13 15:02:36 +0800
categories: leetcode
tags: 
- Array
---
#### [215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

##### ?直接用sort
```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        sort(nums.begin(), nums.end());
        return *(nums.end() - k);
    }
};
```
T(n) : O(nlogn) <br>

##### 手生了，写一下快速排序
```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        quickSort(nums, 0, nums.size() - 1);
        return *(nums.end() - k);
    }
private:
    void quickSort(vector<int>& nums, int lo, int hi)
    {
        if(lo >= hi) return;
        auto j = pa(nums, lo, hi);
        quickSort(nums, lo, j - 1);
        quickSort(nums, j + 1, hi);
    }
    
    int pa(vector<int>& nums, int lo, int hi)
    {
        int v = nums[lo];
        int i{ lo };
        int j { hi + 1};
        while(1)
        {
            while(i < hi && nums[++i] < v) {}
            while(j > lo && nums[--j] > v) {}
            if(i >= j) break;
            swap(nums[i], nums[j]);
        }
        swap(nums[j], nums[lo]);
        return j;
    }
};
```

##### 使用优先级队列
```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int> pq;
        for(auto& num : nums)
        {
            pq.push(num);
            
            if(pq.size() > nums.size() - k + 1)
                pq.pop();
        }
        return pq.top();
    }
};
```
T(n) : O(nlogn) <br>
S(n) : O(n) 

##### 
```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        k = nums.size() - k;
        int lo{ 0 };
        int hi = nums.size() - 1;
        while(lo < hi)
        {
            auto j = pa(nums, lo, hi);
            if(j > k)
                hi = j - 1;
            else if (j < k)
                lo = j + 1;
            else
                break;
        }
        return nums[k];
    }
private:
    int pa(vector<int>& nums, int lo, int hi)
    {
        int v = nums[lo];
        int i{ lo };
        int j { hi + 1};
        while(1)
        {
            while(i < hi && nums[++i] < v) {}
            while(j > lo && nums[--j] > v) {}
            if(i >= j) break;
            swap(nums[i], nums[j]);
        }
        swap(nums[j], nums[lo]);
        return j;
    }
};
```
最好的情况下时只进行一次partition， 为O(n) <br>
最坏的情况是对于每个元素都进行partition 为O(n^2)

将原数组进行洗牌后可以保证O(n)
