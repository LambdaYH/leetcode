---
title: 剑指 Offer 38. 字符串的排列
date: 2021-06-30 15:31:14 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

本题的难点是处理中间的重复字符部分。

##### 使用set来记录最终结果，粗暴的处理
```c++
class Solution {
public:
    vector<string> permutation(string s) {
        vector<string> ret;
        vector<bool> path(s.size());
        backTrack(s, "", ret, path);
        return ret;
    }
private:
    unordered_set<string> set;
    void backTrack(string& s, string tmp, vector<string>& ret, vector<bool>& path)
    {
        if(s.size() == tmp.size())
        {
            if(set.find(tmp) == set.end())
            {
                set.insert(tmp);
                ret.push_back(tmp);
            }
            return;
        }
        for(int i = 0; i < s.size(); ++i)
        {
            if(path[i])
                continue;
            path[i] = true;
            backTrack(s, tmp + s[i], ret, path);
            path[i] = false;
        }
    }
};
```

##### 中心思想是，对于每一位，保证当前位置出现字符串中的每一种字符并且重复的字符只出现一次

抄的大佬

```c++
class Solution {
public:
    vector<string> permutation(string s) {
        backTrack(s, 0);
        return ret;
    }
private:
    vector<string> ret;
    void backTrack(string& s, int index)
    {
        if(index == s.size() - 1) // 这里之所以用s.size() - 1而不是s.size()是因为当前面所有位置都固定完了后，最后一位已经板上钉钉了，所以可以直接结束。
        {
            ret.push_back(s);
            return;
        }
        unordered_set<char> set;
        // 这里i如果从0开始的话，就会导致之前的固定结果被改变
        for(int i = index; i < s.size(); ++i)
        {
            if(set.find(s[i]) != set.end())
                continue;
            set.insert(s[i]); // 防止当前位置上固定重复的字符
            swap(s[i], s[index]); // swap很巧妙，对于第一位来说，意味着后面所有位可以跑到第一位，而同时也意味着第一位可以跑到后面所有位，当index=后面任意一位时，不用担心这一位用不到index之前的，因为前面的已经有机会交换过来了
            backTrack(s, index + 1);
            swap(s[i], s[index]); // 恢复回溯操作
        }
    }
};
```
