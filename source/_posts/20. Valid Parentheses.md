---
title: 20. Valid Parentheses
date: 2021-03-19 14:19:03 +0800
categories: leetcode
---
#### [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
##### Solution 太强了
```c++
class Solution {
public:
    bool isValid(string s) {
        unordered_map<char, char> map{ {'(', ')'}, { '{', '}' }, { '[', ']' } };
        stack<char> st;
        if (s.size() % 2) return false;
        for (auto& ch : s)
        {
            if (ch == (st.size() ? map[st.top()] : '#'))
                st.pop();
            else
                st.push(ch);
        }
        if (st.size())
            return false;
        return true;

    }
};
```
