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
