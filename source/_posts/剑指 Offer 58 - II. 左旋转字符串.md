---
title: 剑指 Offer 58 - II. 左旋转字符串
date: 2021-07-07 17:38:25 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 58 - II. 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

和[189. Rotate Array](https://leetcode.cinte.cc/2021/07/01/189.%20Rotate%20Array/)一样

#####  转转转
```c++
class Solution {
public:
    string reverseLeftWords(string s, int n) {
        reverse(s, 0, s.size() - 1);
        reverse(s, 0, s.size() - n - 1);
        reverse(s, s.size() - n, s.size() - 1);
        return s;
    }
private:
    void reverse(string& s, int start, int end)
    {
        while(start < end)
            swap(s[start++], s[end--]);
    }
};
```
