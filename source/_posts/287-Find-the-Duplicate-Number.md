---
title: 287. Find the Duplicate Number
date: 2021-04-15 15:30:41 +0800
categories: leetcode
---
#### [287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)

#####
```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int lo = 0, hi = nums.size() - 1;
        while(lo < hi)
        {
            int mid = (lo + hi) / 2;
            if(mid + 1 <= nums[mid])
                lo = mid + 1;
            else if(mid + 1 > nums[mid])
                hi = mid;
        }
        return hi;
    }
};
```
T(N) : O(nlogn)

S(n) : O(1)


还有种方法可以使用哈希表

##### 使用cycle，有点静态链表的思想，其中的链表组成如图

![image.png](https://image.cinte.cc/2021/04/15/5dfe75d8ed3ce.png)

```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int walker = nums[0];
        int runner = nums[0];
        
        do
        {
            walker = nums[walker];
            runner = nums[nums[runner]];
        }while(walker != runner);
        
        walker = nums[0];
        while(walker != runner)
        {
            walker = nums[walker];
            runner = nums[runner];
        }
        return runner;
    }
};
```
