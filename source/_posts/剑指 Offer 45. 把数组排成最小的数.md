---
title: 剑指 Offer 45. 把数组排成最小的数
date: 2021-07-06 11:40:35 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 45. 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

##### 我可太太太太太菜了

本质上转换为一个排序问题，对于两个数字a1,b1。当`str(a1) + str(b1) < str(b1) + str(a1)`时，表示a1因当刚在b1左边，反之则表示a1应当放在b1右边。以此为判断条件对数组进行排序，排序后重新组合成字符串就是所需

```c++
class Solution {
public:
    string minNumber(vector<int>& nums) {
        sort(nums, 0, nums.size() - 1);
        string ret = "";
        for(auto& num : nums)
            ret += to_string(num);
        return ret;
    }
private:
    int partition(vector<int>& nums, int lo, int hi)
    {
        int i = lo, j = hi + 1;
        string c = to_string(nums[lo]);
        while(i < j)
        {
            while(i < hi && to_string(nums[++i]) + c < c + to_string(nums[i])) {}
            while(j > lo && to_string(nums[--j]) + c > c + to_string(nums[j])) {}
            if(i >= j)
                break;
            swap(nums[i], nums[j]);
        }
        swap(nums[j], nums[lo]);
        return j;
    }
    void sort(vector<int>& nums, int lo, int hi)
    {
        if(lo > hi)
            return;
        auto j = partition(nums, lo, hi);
        sort(nums, lo, j - 1);
        sort(nums, j + 1, hi);
    }
};
```

v2
```c++
class Solution {
public:
    string minNumber(vector<int>& nums) {
        string ret = "";
        vector<string> strs;
        for(auto& num : nums)
            strs.push_back(to_string(num));
        sort(strs, 0, nums.size() - 1);
        for(auto& str : strs)
            ret += str;
        return ret;
    }
private:
    int partition(vector<string>& nums, int lo, int hi)
    {
        int i = lo, j = hi + 1;
        string c = nums[lo];
        while(i < j)
        {
            while(i < hi && nums[++i] + c < c + nums[i]) {}
            while(j > lo && nums[--j] + c > c + nums[j]) {}
            if(i >= j)
                break;
            swap(nums[i], nums[j]);
        }
        swap(nums[j], nums[lo]);
        return j;
    }
    void sort(vector<string>& nums, int lo, int hi)
    {
        if(lo > hi)
            return;
        auto j = partition(nums, lo, hi);
        sort(nums, lo, j - 1);
        sort(nums, j + 1, hi);
    }
};
```

v3
```c++
class Solution {
public:
    string minNumber(vector<int>& nums) {
        vector<string> strs;
        for(auto& num : nums)
            strs.push_back(to_string(num));
        sort(strs.begin(), strs.end(), [](string& str1, string str2){ return str1 + str2 < str2 + str1; });
        string ret = "";
        for(auto& str : strs)
            ret.append(str);
        return ret;
    }
};
```

v4
```c++
class Solution {
public:
    string minNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end(), [](int a, int b)
        {
            long sa = 10;
            long sb = 10;
            while(sa <= a)
                sa *= 10;
            while(sb <= b)
                sb *= 10;
            return sb * a + b < sa * b + a;
        });
        string ret;
        for(auto& num : nums)
            ret += to_string(num);
        return ret;
    }
};
```

