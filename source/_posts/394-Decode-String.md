---
title: 394. Decode String
date: 2021-04-15 17:50:34 +0800
categories: leetcode
---
#### [394. Decode String](https://leetcode.com/problems/decode-string/)

##### 我越来越菜了
```c++
class Solution {
public:
    string decodeString(string s) {
        int time = 0;
        string now = "";
        stack<string> st;
        stack<int> ist;
        for(auto& ch : s)
        {
            if('0' <= ch && ch <= '9')
                time = time * 10 + ch - '0';
            else if('a' <= ch && ch <= 'z')
                now += ch;
            else if(ch == '[')
            {
                st.push(now);
                ist.push(time);
                now = "";
                time = 0;
            }else if(ch == ']')
            {
                auto timeTmp = ist.top();
                ist.pop();
                auto tmp = st.top();
                st.pop();
                for(int i = 0; i < timeTmp; ++i)
                    tmp += now;
                now = tmp;
            }
        }
        return now;
    }
};
```

##### 递归
```c++
class Solution {
public:
    string decodeString(string s) {
        int i = 0;
        return help(s, i);
    }
private:
    string help(string& s, int& i)
    {
        string ret = "";
        while(i < s.size() && s[i] != ']')
        {
            if(s[i] >= 'a' && s[i] <= 'z')
                ret += s[i++];
            else
            {
                int time = 0;
                while(s[i] >= '0' &&  s[i] <= '9')
                    time = time * 10 + s[i++] - '0';
                
                ++i;
                string t = help(s, i);
                ++i;
                
                while(time-- > 0)
                    ret += t;
            }
        }
        return ret;
    }
};
```
处理一个框框中的数据，框框里遇到框框就再递归
