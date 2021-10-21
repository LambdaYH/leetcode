---
title: 3. Longest Substring Without Repeating Characters
date: 2021-02-02 23:11:00 +0800
categories: leetcode
---
#### [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
##### 第一次
```c++
class Solution
{
public:
    int lengthOfLongestSubstring(string s)
    {
        int count = 0;
        int max = 0;
        int index = 0;
        int pre_index = 0;
        unordered_map<char, int> map;
        for (const auto ch : s)
        {
            max = count > max ? count : max;
            if (!map.emplace(ch, index++).second)
            {
                auto t = map[ch];
                map[ch] = index - 1;
                if (t - pre_index < 0)
                {
                    ++count;
                    continue;
                }
                count -= t - pre_index;
                pre_index = t + 1;
            }
            else
            {
                ++count;
            }
        }
        max = count > max ? count : max;
        return max;
    }
};
```
![](https://image.cinte.cc/2021/02/02/b303f008647ee.png)

##### review

sliding window
```c+
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> memo;
        int begin = 0, end = 0, sz = s.size();
        int ret = 0;
        while(end < sz)
        {
            char ch = s[end++];
            ++memo[ch];
            while(memo[ch] > 1)
                --memo[s[begin++]];
            ret = max(ret, end - begin);
        }
        return ret;
    }
};
```

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_set<char> memo;
        int begin = 0, end = 0, sz = s.size();
        int ret = 0;
        while(end < sz)
        {
            char ch = s[end++];
            while(memo.count(ch))
                memo.erase(s[begin++]);
            memo.emplace(ch);
            ret = max(ret, end - begin);
        }
        return ret;
    }
};
```

但是如果出现重复的字符的话，begin不需要一个一个递增然后判断，只需要移到重复字符的前一个位置即可，于是可以进行优化
```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> memo(256, -1);
        int begin = -1, end = 0, ret = 0;
        int sz = s.size();
        for(; end < sz; ++end)
        {
            begin = max(begin, memo[s[end]]); // 如果当前的字符在[begin, end]区域重复了，就把begin移动到前一个s[end]出现的地方，跳跃
            memo[s[end]] = end; // 更新当前字符最后出现的坐标
            ret = max(ret, end - begin);
        }
        return ret;
    }
};
```
使用hash map
```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> memo;
        int begin = 0, end = 0, ret = 0;
        int sz = s.size();
        for(; end < sz; ++end)
        {
            begin = max(begin, memo[s[end]]);
            memo[s[end]] = end + 1; // map中默认初始化为0，所以这里加以改变
            ret = max(ret, end - begin + 1);
        }
        return ret;
    }
};
```
