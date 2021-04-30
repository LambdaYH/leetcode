---
title: 12. Integer to Roman
date: 2021-03-04 07:11:00 +0800
categories: leetcode
---
#### [12. Integer to Roman](https://leetcode.com/problems/integer-to-roman/)
```c++
class Solution {
public:
    string intToRoman(int num) {
        string roman[]{"I", "IV", "V", "IX", "X", "XL", "L", "XC", "C", "CD", "D", "CM", "M"};
        int nums[]{1, 4, 5, 9, 10, 40, 50, 90, 100, 400, 500, 900, 1000};
        string result = "";
        int i = size(nums) - 1;
        while ( num > 0 )
        {
            while ( num >= nums[i] )
            {
                num -= nums[i];
                result += roman[i];
            }
            --i;
        }
        return result;
    }
};
```
