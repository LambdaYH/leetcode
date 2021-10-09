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
    int patition(vector<int>& nums, int i, int j)
    {
        int pivot = rand() % (j - i + 1) + i;
        int c = nums[pivot];
        swap(nums[pivot], nums[i]);
        int lo = i, hi = j + 1;
        while(lo < hi)
        {
            while(lo < j && nums[++lo] < c) {}
            while(hi > i && nums[--hi] > c) {}
            if(lo >= hi)
                break;
            swap(nums[lo], nums[hi]);
        }
        swap(nums[hi], nums[i]);
        return hi;
    }
    void sort(vector<int>& nums, int i, int j)
    {
        if(i >= j)
            return;
        int m = patition(nums, i, j);
        sort(nums, i, m - 1);
        sort(nums, m + 1, j);
    }
};
```

##### mergeSort
```C++
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        tmp.resize(nums.size());
        mergeSort(nums, 0, nums.size() - 1);
        return nums;
    }
private:
    vector<int> tmp;
    void mergeSort(vector<int>& nums, int lo, int hi)
    {
        if(lo >= hi)
            return;
        int mid = lo + (hi - lo) / 2;
        mergeSort(nums, lo, mid);
        mergeSort(nums, mid + 1, hi);
        copy(nums.begin() + lo, nums.begin() + hi + 1, tmp.begin() + lo);
        int i = lo, j = mid + 1;
        int k = lo;
        while(i <= mid || j <= hi)
        {
            if(i == mid + 1)
                nums[k++] = tmp[j++];
            else if(j == hi + 1)
                nums[k++] = tmp[i++];
            else if(tmp[i] < tmp[j])
                nums[k++] = tmp[i++];
            else
                nums[k++] = tmp[j++];
        }
    }
};
```

##### heapSort
```c++
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        heapSort(nums);
        return nums;
    }
private:
    void adjustHeap(vector<int>& nums, int s, int m)
    {
        int tmp = nums[s];
        while((s << 1) + 1 <= m) // 如果左孩子存在，也就是这个点不是叶子节点
        {
            int lson = (s << 1) + 1; // 左孩子是当前节点*2+1
            int rson = (s << 1) + 2; // 右孩子是当前节点*2+2
            int large;
            if(nums[lson] > nums[s]) // 如果左孩子>父亲，large为左孩子
                large = lson;
            else                    // 反之，large为父亲
                large = s;
            if(rson <= m && nums[rson] > nums[large]) // 如果右孩子>父亲，large为右孩子
                large = rson;
            if(large != s) // 当large不是当前的点是，说明下面的树需要调整
            {
                swap(nums[large], nums[s]);
                s = large; // 将s调整为孩子，然后继续调整下面
            }else
                break;
        }
    }
    void heapSort(vector<int>& nums)
    {
        int sz = nums.size() - 1;
        for(int i = sz / 2; i >= 0; --i)
            adjustHeap(nums, i, sz);
        for(int i = sz; i >= 0; --i)
        {
            swap(nums[i], nums[0]);
            adjustHeap(nums, 0, --sz);
        }
    }
};
```
