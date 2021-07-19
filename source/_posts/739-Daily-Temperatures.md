---
title: 739. Daily Temperatures
date: 2021-04-15 14:39:24 +0800
categories: leetcode
---
#### [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)

#####
```c++
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
        vector<int> next(101, INT_MAX);
        vector<int> ret(T.size(), 0);
        for(int i = T.size() - 1; i >= 0; --i)
        {
            int warmer = INT_MAX;
            for(int j = T[i] + 1; j <= 100; ++j)
            {
                if(next[j] < warmer)
                {
                    warmer = next[j];
                }
            }
            if(warmer < INT_MAX)
                ret[i] = warmer - i;
            next[T[i]] = i;
        }
        return ret;
    }
};
```

从后开始，对于温度为70的，接下来只会出现71~100的温度，只需要记录这些温度出现的天数，然后寻求一个最近的天数即可。由于是从后面开始更新的，所以不用怕前面的天数出来扰乱我

##### 使用堆栈
```c++
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
        stack<int> s;
        vector<int> ret(T.size());
        for(int i = T.size() - 1; i >= 0; --i)
        {
            while(!s.empty() && T[i] >= T[s.top()])
                s.pop();
            ret[i] = s.empty() ? 0 : s.top() - i;
            s.push(i);
        }
        return ret;
    }
};
```

假设，对于位于i = 1处的天气为30度，若i = 2处的天气为50，而i = 4处的天气为30，显然，对于I = 1来说，i = 4是对他没有任何意义的，因此可以舍弃掉i = 4; <br>
反之，若T[1] = 30, T[2] = 50, T[4] = 100, 则无法舍弃T[4] 因为若1和2之间出现一个60，则T[4]必须留着。

对于这种次序，只保留从大到小的序列，前面一个如果比后面大，后面的对于前面一个就无用了，就出栈，然后自己算完自己的后，入栈，一人就可以遮蔽后买你的所有效果

另一种堆栈
```c++
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        vector<int> ret(temperatures.size(), 0);
        stack<int> s;
        for(int i = 0; i < temperatures.size(); ++i)
        {
            while(!s.empty() && temperatures[i] > temperatures[s.top()])
            {
                auto tmp = s.top();
                ret[tmp] = i - tmp;
                s.pop();
            }
            s.push(i);
        }
        return ret;
    }
};
```
