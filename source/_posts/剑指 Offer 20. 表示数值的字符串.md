---
title: 剑指 Offer 20. 表示数值的字符串
date: 2021-06-22 16:37:41 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 20. 表示数值的字符串](https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/)

##### 常规思路
```C++
class Solution {
public:
    bool isNumber(string s) {
        int start = 0, end = s.size() - 1;
        while(start < end && s[start] == ' ')
            ++start;
        while(end > start && s[end] == ' ')
            --end;
        if(start > end)
            return false;
        if(s[start] == '+' || s[start] == '-')
            ++start;
        bool isMeetDigital = false;
        bool isMeetDot = false;
        bool isMeetE = false;
        for(int i = start; i <= end; ++i)
        {
            if(isDigital(s[i]))
            {
                isMeetDigital = true;
            }
            else if(s[i] == '.' && !isMeetDot)
            {
                if(isMeetE)
                    return false;
                isMeetDot = true;
                if(!isMeetDigital)
                {
                    if(i >= end)
                        return false;
                    else if(!isDigital(s[++i]))
                        return false;
                    else
                        isMeetDigital = true;
                }
            }else if(s[i] == 'e' || s[i] == 'E')
            {
                if(!isMeetDigital)
                    return false;
                if(!isMeetE)
                {
                    bool isSigned = false;
                    while(i < end && (s[++i] == '+' || s[i] == '-'))
                    {
                        if(isSigned)
                            return false;
                        isSigned = true;
                    }
                    if(i <= end && isDigital(s[i]))
                    {
                        isMeetE = true;
                        isMeetDigital = true;
                    }
                    else
                        return false;
                }else
                    return false;
            }
            else
                return false;
        }
        return true;
    }
private:
    bool isDigital(char& ch)
    {
        return ch <= '9' && ch >= '0';
    }
};
```

##### 状态机

![1624440075950.png](https://image.cinte.cc/2021/06/23/13ee451ce60e5.png)
![1624440089788.png](https://image.cinte.cc/2021/06/23/c4e27f54b0503.png)

太烦了 不想做
