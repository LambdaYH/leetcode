---
title: 剑指 Offer 40. 最小的k个数
date: 2021-06-27 15:52:42 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 40. 最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

##### 用优先队列
```c++
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        priority_queue<int> q;
        for(auto& num : arr)
        {
            q.push(num);
            if(q.size() > k)
                q.pop();
        }
        vector<int> ret;
        while(!q.empty())
        {
            ret.push_back(q.top());
            q.pop();
        }
        return ret;
    }
};
```
O(nlogk)?

##### 排序
```c++
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        sort(arr.begin(), arr.end());
        vector<int> ret(arr.begin(), arr.begin() + k); // 可以避免空间多次分配带来的开销
        return ret;
    }
};
```

但是这里不用排所有，只需要排k个数
```c++
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        quickSort(arr, 0, arr.size() - 1, k);
        vector<int> ret;
        for(int i = 0; i < k; ++i)
            ret.push_back(arr[i]);
        return ret;
    }
private:
    int partition(vector<int>& nums, int begin, int end)
    {
        auto c = nums[begin];
        auto i = begin, j = end + 1;
        while(true)
        {
            while(i < end && nums[++i] < c) {}
            while(j > begin && nums[--j] > c) {}
            if(i >= j)  // 这里关键，这个条件过后要防止交换了
                break;
            swap(nums[i], nums[j]);
        }
        swap(nums[j], nums[begin]);
        return j;
    }
    void quickSort(vector<int>& arr, int begin, int end, int& k)
    {
        if(begin >= end)
            return;
        auto j = partition(arr, begin, end);
        if(j == k)
            return;
        if(j > k)
            quickSort(arr, begin, j - 1, k);
        else
            quickSort(arr, j + 1, end, k);
    }
};
```
