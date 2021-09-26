---
title: 剑指 Offer 62. 圆圈中最后剩下的数字
date: 2021-07-12 11:33:18 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 62. 圆圈中最后剩下的数字](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

[约瑟夫环](https://zh.wikipedia.org/wiki/%E7%BA%A6%E7%91%9F%E5%A4%AB%E6%96%AF%E9%97%AE%E9%A2%98)

[题解](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/solution/jian-zhi-offer-62-yuan-quan-zhong-zui-ho-dcow/)

##### dp
```c++
class Solution {
public:
    int lastRemaining(int n, int m) {
        int pre = 0;
        for(int i = 2; i <= n; ++i)
        {
            pre = (pre + m) % i;
        }
        return pre;
    }
};
```
![Screenshot_20210712-115540_Samsung Notes.jpg](https://image.cinte.cc/2021/07/12/dcd4cf4ae07a7.jpg)
