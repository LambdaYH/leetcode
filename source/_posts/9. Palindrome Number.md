---
title: 9. Palindrome Number
date: 2021-03-03 20:54:00 +0800
categories: leetcode
---
#### [9. Palindrome Number](https://leetcode.com/problems/palindrome-number/)
##### 第一次
```c++
class Solution
{
public:
    bool isPalindrome(int x)
    {
        if (x < 0)
            return false;
        else
        {
            if(reverse(x) == x)
            {
                return true;
            }else
            {
                return false;
            }
        }
    }

    int reverse(int x)
    {
        int rev = 0;
        while (x != 0)
        {
            int pop = x % 10;
            x /= 10;
            if (rev > INT_MAX / 10 || (rev == INT_MAX / 10) && (pop > INT_MAX % 10))
                return 0;
            if (rev < INT_MIN / 10 || (rev == INT_MIN / 10) && (pop < INT_MIN % 10))
                return 0;
            rev = rev * 10 + pop;
        }
        return rev;
    }
};
```
