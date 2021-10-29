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

##### review
```c++
class Solution {
public:
    int romanToInt(string s) {
        string roman[]{"I", "IV", "V", "IX", "X", "XL", "L", "XC", "C", "CD", "D", "CM", "M"};
        int nums[]{1, 4, 5, 9, 10, 40, 50, 90, 100, 400, 500, 900, 1000};
        int ret = 0;
        int index = 12, length = s.size();
        for(int i = 0; i < length; ++i)
        {
            string si = s.substr(i, 1);
            string d = i < length - 1 ? s.substr(i, 2) : "";
            while(index >= 0)
            {
                if(roman[index] == d)
                {
                    ret += nums[index];
                    ++i;
                    break;
                }else if(roman[index] == si)
                {
                    ret += nums[index];
                    break;
                }else
                    --index;
            }
        }
        return ret;
    }
};
```

##### solution
```c++
class Solution {
public:
    int romanToInt(string s) {
        int ret = 0;
        for(int i = 0, sz = s.size(); i < sz; ++i)
        {
            int num = symbolValues[s[i]];
            if(i < sz - 1 && num < symbolValues[s[i + 1]])
                ret -= num;
            else
                ret += num;
        }
        return ret;
    }
private:
    unordered_map<char, int> symbolValues = {
        {'I', 1},
        {'V', 5},
        {'X', 10},
        {'L', 50},
        {'C', 100},
        {'D', 500},
        {'M', 1000},
    };
};
```
