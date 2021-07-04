---
title: 剑指 Offer 51. 数组中的逆序对
date: 2021-07-03 18:43:06 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 51. 数组中的逆序对](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

##### 用归并排序，顺便计算逆序对（tnl)
```c++
class Solution {
public:
    int reversePairs(vector<int>& nums) {
        merge(nums, 0, nums.size() - 1);
        return ret;
    }
private:
    int ret = 0;
    void merge(vector<int>& nums, int l, int r)
    {
        if(l >= r)
            return;
        int m = (l + r) >> 1; // 从中间截开来，划分
        merge(nums, l, m); // 递归排序左半边归并，排完后是从小到大的顺序
        merge(nums, m + 1, r); // 递归排序右半边归并，排完后是从小到大的顺序
        vector<int> tmp(nums.begin() + l, nums.begin() + r + 1); // 生成一个临时字符串，将排序区间内的内容复制进去
        int i = 0, j = m + 1 - l;
        for(int k = l; k <= r; ++k)
        {
            if(i == m + 1 - l) // 当i，也就是左半边的指针超过了中位数后，也就是说左半边元素用完了。那么把剩下的元素全都用右半边剩下的元素填充
                nums[k] = tmp[j++];
            else if(j == r + 1 - l) // 当右半边元素用完后，把剩下的空位全都用右半边元素填充
                nums[k] = tmp[i++];
            else if(tmp[i] <= tmp[j]) // 进行大小盘带按，填充较小的元素
                nums[k] = tmp[i++];
            else
            {
                nums[k] = tmp[j++]; // 填充较大的元素
                ret += m - i + 1 - l; // 当左边某个数>右边某个数时，由于左边序列是从小到大排列，那么左边从这个数到结尾的所有数与右边那个数都构成了逆序对，依次遍历。将所有逆序对加上。
            }
        }
    }
};
```

