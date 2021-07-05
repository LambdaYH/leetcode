---
title: 剑指 Offer 56 - II. 数组中数字出现的次数 II
date: 2021-07-05 14:40:15 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 56 - II. 数组中数字出现的次数 II](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

##### hashmap
```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        unordered_map<int, int> map;
        for(auto& num : nums)
            map[num] += 1;
        for(auto& it : map)
            if(it.second == 1)
                return it.first;
        return 0;
    }
};
```
T(n) : O(n)

S(n) : O(n)

##### 位运算

因为其他数都出现三次，只有一个数出现一次，所以将所有数的每一位加起来后对3取余剩下的就是那个只出现一次的数字

对于每一位构建状态转换图，有三个状态0,1,2
![1625471528006.png](https://image.cinte.cc/2021/07/05/78efdf2acd2da.png)
其中三个状态为0,1,2表示除以3后的余数

求出来后的结果必然是00或01两个状态，因为所有出现三次的数都加完了取余完了，所以只剩下了这2种情况表示那个只出现一次的数的位为0或1，所以最后只需要返回one即可

对于每一位都是相同的方法，所以可以直接放到一起来用位运算


###### 根据状态转换图，构建卡诺图，化简
```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int one = 0, two = 0;
        for(auto& num : nums)
        {
            auto tmp = one;
            one = (one & ~num) | (~two & ~one & num);
            two = (two & ~num) | (tmp & num);
        }
        return one;
    }
};
```

###### 根据图观察获得

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int one = 0, two = 0;
        for(auto& num : nums)
        {
            one = ~two & (one ^ num);
            two = ~one & (two ^ num); // 注意此处的两个运算并不是同时进行的，所以这里的two需要根据变化后的one的结果来运算。根据计算后的one的结果，见下图（还是卡诺图来的直观）
        }
        return one;
    }
};
```

![1625471719640.png](https://image.cinte.cc/2021/07/05/b4ff9493e0303.png)

T(n) : O(n)

S(n) : O(1)
