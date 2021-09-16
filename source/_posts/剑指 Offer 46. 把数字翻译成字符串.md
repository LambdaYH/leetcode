---
title: 剑指 Offer 46. 把数字翻译成字符串
date: 2021-07-06 12:03:44 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 46. 把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

##### BackTrack
```c++
class Solution {
public:
    int translateNum(int num) {
        string strs = to_string(num);
        backTrack(strs, 0);
        return ret;
    }
private:
    int ret = 0;
    void backTrack(string& nums, int cur)
    {
        if(cur >= nums.size() - 1)
        {
            ++ret;
            return;
        }
        backTrack(nums, cur + 1);
        auto sum = (nums[cur] - '0') * 10 + nums[cur + 1] - '0';
        if(nums[cur] != '0' && sum < 26 && sum > 0)
            backTrack(nums, cur + 2);
    }
};
```

##### dp
version.1
```c++
class Solution {
public:
    int translateNum(int num) {
        string str = to_string(num);
        vector<int> dp(str.size());
        dp[0] = 1;
        for(int i = 1; i < str.size(); ++i)
        {
            dp[i] += dp[i - 1];
            auto num = (str[i - 1] - '0') * 10 + str[i] - '0';
            if(num >= 10 && num < 26)
                dp[i] += (i >= 2 ? dp[i - 2] : 1);
        }
        return dp.back();
    }
};
```

version.2

优化dp的空间，但字符串还是占O(n)
```c++
class Solution {
public:
    int translateNum(int num) {
        string str = to_string(num);
        int a = 1, b = 1;
        for(int i = 1; i < str.size(); ++i)
        {
            auto num = (str[i - 1] - '0') * 10 + str[i] - '0';
            a = (num >= 10 && num < 26) ? a + b : b;
            swap(a, b);
        }
        return b;
    }
};
```

version.3

直接使用取余计算数位
```c++
class Solution {
public:
    int translateNum(int num) {
        int a = 1, b = 1;
        int lastNum = num % 10;
        num /= 10;
        while(num)
        {
            auto curNum = num % 10;
            auto sum = curNum * 10 + lastNum;
            a = (sum >= 10 && sum < 26) ? a + b : b;
            num /= 10;
            lastNum = curNum;
            swap(a, b);
        }
        return b;
    }
};
```

递归
```c++
class Solution {
public:
    int translateNum(int num) {
        if(num < 10)
            return 1;
        int ret = 0;
        int a = num % 10;
        num /= 10;
        int b = num % 10;
        if(b != 0 && b * 10 + a < 26)
            ret += translateNum(num / 10);
        ret += translateNum(num);
        return ret;
    }
};
```
