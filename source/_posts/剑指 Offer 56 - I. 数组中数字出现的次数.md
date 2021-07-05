---
title: 剑指 Offer 56 - I. 数组中数字出现的次数
date: 2021-07-05 11:47:54 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 56 - I. 数组中数字出现的次数](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

##### 
```c++
class Solution {
public:
    vector<int> singleNumbers(vector<int>& nums) {
        int x = 0, m = 1, n = 0;
        // 对于只有一个只出现一次的数字的情况，异或后结果就是那个值，而有两个的话，假设2个数字是x,y，则异或后结果为x^y
        for(auto& num : nums)
            n ^= num;
        // 设m为1，寻找x与y从左往右数不相同的第一个数字，异或中是相异为1，所以当m&n==1时，表示n的这位为1了，于是就找到了这个不相同的第一个数字，并保存到m
        while((m & n) == 0) // 注意 == 的优先级比 & 高
            m <<= 1;
        for(auto& num : nums)
        {
            if((num & m) == 0) // 当且仅当m为1的这一位的数字为1时，与的结果才为1，因此那两个单独的数字必定不可能同时通过这个if条件，所以将原数列分成了两个子序列
                x ^= num;
        }
        return {x, x ^ n}; // x ^ n = x ^ x ^ y = 0 ^ y = y
    }
};
```

优化技巧
```c++
while((m & n) == 0)
    m <<= 1;
```
可以优化为
```c++
m = n & (~n + 1);
```

`~n`将n的所有位取反，`~n + 1`则可以将`~n`的最低一个0变1，也就是把`n`的最低一个1标记出来，而其他的位`~n`保持与`n`相反，因此他们`与`之后的结果就是最低位的1保留，剩下全是0。

