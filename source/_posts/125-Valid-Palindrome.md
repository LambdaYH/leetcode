---
title: 125. Valid Palindrome
date: 2021-04-01 20:03:46 +0800
categories: leetcode
---
#### [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
```c++
class Solution {
public:
    bool isPalindrome(string s) {
        auto lo = s.begin();
        auto hi = s.end() - 1;
        while(lo < hi)
        {
            if(*lo <= 'Z' && *lo >= 'A')
                *lo += 32;
            if(*hi <= 'Z' && *hi >= 'A')
                *hi += 32;
            if(!isDigitalOrAlphabet(*lo))
                ++lo;
            else if(!isDigitalOrAlphabet(*hi))
                --hi;
            else
            {
                if(*lo != *hi)
                    return false;
                ++lo;
                --hi;
            }
            
        }
        return true;
    }
private:
    bool isDigitalOrAlphabet(char& ch)
    {
        if((ch >= 'a' && ch < 'z') || (ch >= '0' && ch <= '9'))
            return true;
        else
            return false;
    }
};
```
T(n): O(n)

S(n): O(1)
