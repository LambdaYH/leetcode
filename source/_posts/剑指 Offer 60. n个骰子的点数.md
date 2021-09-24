---
title: 剑指 Offer 60. n个骰子的点数
date: 2021-07-11 16:00:33 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 60. n个骰子的点数](https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/)

##### dp(真的妙)

对于n个骰子来说，他们值的和最小值是所有骰子都是1，最大值是所有骰子都是6，所以他们和的范围是`[n, 6n]`，所以总共有`6n - n + ! = 5n + 1`种情况。

对于n个骰子的值x来说，设n-1个骰子值x的概率是`f(n - 1, x)`，则`f(n, x) = f(n - 1, x - 1) * 1 / 6 + f(n - 1, x - 2) * 1 / 6 ... f(n - 1, x - 6) * 1 / 6`，这个式子表示当第n个骰子取值为y时，概率就是前n个骰子取值为`x - y`乘上当前骰子取y的概率，这样子就形成了递推公式。

但是`x - y`会产生越界问题，由此转变思想，当n-1个骰子取值为x时，n个骰子的取值只能是`x+1 ~ x+6`。由此不用考虑越界。

```c++
class Solution {
public:
    vector<double> dicesProbability(int n) {
        vector<double> pre(6, 1 / 6.0); // 初始化一个骰子的情况
        for(int i = 2; i <= n; ++i) // 从第二个骰子开始
        {
            vector<double> tmp(5 * i + 1, 0); // i个骰子可能的情况共有5n+1种
            for(int j = 0; j < pre.size(); ++j) // 对i-1个骰子情况中可能的取值进行遍历，表示递推式中的x
                for(int k = 0; k < 6; ++k) // 对i-1个骰子可能的取值加上1到6，就是i个骰子情况，由于前面取值加上1到6可能会有重复情况，而把这些重复情况概率加起来就是最终概率。
                    tmp[k + j] += pre[j] * 1 / 6.0;
            pre = tmp;
        }
        return pre;
    }
};
```
