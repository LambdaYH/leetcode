---
title: 338. Counting Bits
date: 2021-04-14 20:36:04 +0800
categories: leetcode
---
#### [338. Counting Bits](https://leetcode.com/problems/counting-bits/)

##### O(32n) 解法
```c++
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> ret;
        for(int i = 0; i <= num; ++i)
        {
            int cur = i;
            int count = 0;
            while(cur)
            {
                int j = cur % 2;
                if(j == 1)
                    ++count;
                cur /= 2;
            }
            ret.push_back(count);
        }
        return ret;
    }
};
```

##### 使用库
```c++
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> ret;
        for(int i = 0; i <= num; ++i)
        {
            ret.push_back(__builtin_popcount(i));
        }
        return ret;
    }
};
```

##### 
```
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> ret(num + 1);
        for(int i = 0; i <= num; ++i)
        {
            ret[i] = ret[i >> 1] + (i & 1);
        }
        return ret;
    }
};
```

右移加上最后一位，类似动态规划的思想
