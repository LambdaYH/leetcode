---
title: 66. Plus One
date: 2021-04-07 21:19:51 +0800
categories: leetcode
---
#### [66. Plus One](https://leetcode.com/problems/plus-one/)

```c++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int i = digits.size() - 1;
        int c = 0;
        ++digits[i];
        while(digits[i] > 9 && i > 0)
        {
            c = digits[i] / 10;
            digits[i] %= 10;
            --i;
            digits[i] += c;
        }
        if(digits[i] > 9)
        {
            vector<int> ret(digits.size() + 1, 0);
            ret[0] = 1;
            return ret;
        }
        return digits;
    }
};
```
