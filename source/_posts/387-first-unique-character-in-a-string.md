---
title: 387. First Unique Character in a String
date: 2021-03-16 13:24:21 +0800
categories: leetcode
---
#### [387. First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)
##### First Time
```c++
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<char, int> map;
        for(int i = 0; i < s.size(); ++i)
        {
            if(!map.emplace(s[i], i).second)
                map[s[i]] = -1; 
        }
        for(auto& ch : s)
        {
            if(map[ch] != -1)
                return map[ch];
        }
        return -1;
    }
};
```
##### Second Time
数组由于直接获取内存地址而不需要散列，是更快的O(N)
```
class Solution {
public:
    int firstUniqChar(string s) {
        int eng[26]{0};
        for(auto& ch : s)
        {
            eng[ch - 'a'] += 1;
        }
        int i = 0;
        for(auto& ch : s)
        {
            if(eng[ch - 'a'] == 1)
                return i;
            ++i;
        }
        return -1;
    }
};
```
##### 尝试只进入一次(还是很慢)
```c++
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<char, int> map;
        unordered_set<char> set;
        for(int i = 0; i < s.size(); ++i)
        {
            if(!set.emplace(s[i]).second)
            {
                map.erase(s[i]);
            }else
            {
                map[s[i]] = i;
            }
        }
        int j = map.size() ? map.begin()->second : -1;
        for (auto i = map.begin(); i != map.end(); ++i)
        {
            j = min(j, i->second);
        }
        return j;
    }
};
```

##### 第二次遍历只遍历哈希
```c++
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<char, int> map;
        for(int i = 0, sz = s.size(); i < sz; ++i)
        {
            if(map.count(s[i]))
                map[s[i]] = -1;
            else
                map[s[i]] = i;
        }
        int first = s.size();
        for(auto& [_, frq] : map)
            if(frq != -1 && frq < first)
                first = frq;
        return first == s.size() ? -1 : first;
    }
};
```

##### 用队列，避免了第二次遍历
> 思路与算法

我们也可以借助队列找到第一个不重复的字符。队列具有「先进先出」的性质，因此很适合用来找出第一个满足某个条件的元素。

具体地，我们使用与方法二相同的哈希映射，并且使用一个额外的队列，按照顺序存储每一个字符以及它们第一次出现的位置。当我们对字符串进行遍历时，设当前遍历到的字符为 cc，如果 cc 不在哈希映射中，我们就将 cc 与它的索引作为一个二元组放入队尾，否则我们就需要检查队列中的元素是否都满足「只出现一次」的要求，即我们不断地根据哈希映射中存储的值（是否为 -1−1）选择弹出队首的元素，直到队首元素「真的」只出现了一次或者队列为空。

在遍历完成后，如果队列为空，说明没有不重复的字符，返回 -1−1，否则队首的元素即为第一个不重复的字符以及其索引的二元组。

小贴士

在维护队列时，我们使用了「延迟删除」这一技巧。也就是说，即使队列中有一些字符出现了超过一次，但它只要不位于队首，那么就不会对答案造成影响，我们也就可以不用去删除它。只有当它前面的所有字符被移出队列，它成为队首时，我们才需要将它移除。

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/first-unique-character-in-a-string/solution/zi-fu-chuan-zhong-de-di-yi-ge-wei-yi-zi-x9rok/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


```c++
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<char, int> map;
        queue<pair<char, int>> q;
        for(int i = 0, sz = s.size(); i < sz; ++i)
        {
            if(!map.count(s[i]))
            {
                map.emplace(s[i], i);
                q.emplace(s[i], i);
            }else
            {
                map[s[i]] = -1;
                while(!q.empty() && map[q.front().first] == -1)
                    q.pop();
            }
        }
        return q.empty() ? -1 : q.front().second;
    }
};
```
