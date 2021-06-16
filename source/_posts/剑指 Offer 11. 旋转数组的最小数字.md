---
title: 剑指 Offer 11. 旋转数组的最小数字
date: 2021-06-16 21:15:44 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

##### 
```c++
class Solution {
public:
    int minArray(vector<int>& numbers) {
        int lo = 0, hi = numbers.size() - 1;
        while(lo < hi)
        {
            int mid = (lo + hi) / 2;
            if(numbers[mid] > numbers[hi])
                lo = mid + 1;
            else if(numbers[mid] < numbers[hi])
                hi = mid;
            else
                --hi;   // 主要难点是这种情况，当相等时，无法判断最小点是在左半边还是右半边。此时--hi，当旋转点<hi时，易得--hi后旋转点依旧存在，当旋转点==hi时，因为中点值=旋转点值，因此即便删除了，和旋转点相等的值依旧流了下来，以后用得到。   ps: 碰到这种情况也可以直接遍历了
        }
        return numbers[hi];
    }
};
```
