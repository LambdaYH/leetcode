---
title: 13. Roman to Integer
date: 2021-03-07 16:17:52 +0800
categories: leetcode
---
#### [13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/)
```c++
class Solution
{
public:
    int romanToInt(string s)
    {
        unordered_map<string, int> map{{"I", 1}, {"IV", 4}, {"V", 5}, {"IX", 9}, {"X", 10}, {"XL", 40}, {"L", 50}, {"XC", 90}, {"C", 100}, {"CD", 400}, {"D", 500}, {"CM", 900}, {"M", 1000}};
        int size = s.size();
        int num = 0;

        for (int i = size - 1; i >= 0; --i)
        {
            string now(1, s[i]);
            if (i == 0)
            {
                return num + map[now];
            }
            string before(1, s[i - 1]);
            string sub = before + now;
            if (map.find(sub) != map.end())
            {
                num += map[sub];
                --i;
            }
            else
            {
                num += map[now];
            }
        }
        return num;
    }
};
```
