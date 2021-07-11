---
title: 剑指 Offer 67. 把字符串转换成整数
date: 2021-07-11 16:27:03 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 67. 把字符串转换成整数](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/)

#####
```c++
class Solution {
public:
    int strToInt(string str) {
        int start = 0;
        while(str[start] == ' ')
            ++start;
        bool positive = true;
        if(str[start] == '+' || str[start] == '-')
            positive = str[start++] == '+' ? true : false;
        int ret = 0;;
        for(int i = start; i < str.size(); ++i)
        {
            int num = str[i] - '0';
            if(isValid(str[i]))
            {
                if(positive)
                {
                    if(ret > INT_MAX / 10 || (ret == INT_MAX / 10 && num >= INT_MAX % 10))
                        return INT_MAX;
                }else
                {
                    if(-ret < INT_MIN / 10 || (-ret == INT_MIN / 10 && -num <= INT_MIN % 10))
                        return INT_MIN;
                }
                ret = ret * 10 + num;
            }
            else
                break; 
        }
        return positive ? ret : -ret;
    }
private:
    bool isValid(char ch)
    {
        return ch >= '0' && ch <= '9';
    }
};
```

稍微优化一下
```C++
class Solution {
public:
    int strToInt(string str) {
        int start = 0;
        while(str[start] == ' ')
            ++start;
        bool positive = true;
        if(str[start] == '+' || str[start] == '-')
            positive = str[start++] == '+' ? true : false;
        int ret = 0;;
        for(int i = start; i < str.size(); ++i)
        {
            int num = str[i] - '0';
            if(isValid(str[i]))
            {
                if(ret > 214748364 || (ret == 214748364 && num > 7)) // 即使当num == 8时,如果是负数，虽然没越界，但是假设他越界了，依旧可以返回正确的值
                    return positive ? INT_MAX : INT_MIN;
                ret = ret * 10 + num;
            }
            else
                break; 
        }
        return positive ? ret : -ret;
    }
private:
    bool isValid(char ch)
    {
        return ch >= '0' && ch <= '9';
    }
};
```
