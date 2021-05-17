---
title: 17. Letter Combinations of a Phone Number
date: 2021-03-10 21:24:42 +0800
categories: leetcode
---
#### [17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)
```c++
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        if(digits.size())
        {
            backtrack("", digits);
        }else
        {
            return {};
        }
    }

private:
    vector<string> ret;
    unordered_map<char, vector<char>> phone{{'2', {'a', 'b', 'c'}}, {'3', {'d', 'e', 'f'}}, {'4', {'g', 'h', 'i'}}, {'5', {'j', 'k', 'l'}}, {'6', {'m', 'n', 'o'}}, {'7', {'p', 'q', 'r', 's'}}, {'8', {'t', 'u', 'v'}}, {'9', {'w', 'x', 'y', 'z'}}};
    void backtrack(string comb, string digit)
    {
        if(!digit.size())
        {
            ret.push_back(comb);
        }

        for(auto& ch : phone[digit[0]])
        {
            backtrack(comb + ch, digit.substr(1));
        }
    }
};
```

还有一种

先把一个字母依次添加，然后再依次网上衔接各种情况
