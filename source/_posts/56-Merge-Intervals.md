---
title: 56. Merge Intervals
date: 2021-04-06 11:53:30 +0800
categories: leetcode
tags: 
- array
---
#### [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)

```c++
bool mySort(vector<int>& a, vector<int>& b)
{
    return a[0] < b[0];
}
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        vector<int> re;
        sort(intervals.begin(), intervals.end(), mySort);
        re.push_back(intervals[0][0]);
        re.push_back(intervals[0][1]);
        int index = 2;
        for(auto i = intervals.begin() + 1; i != intervals.end(); ++i)
        {
            if((*i)[0] <= re[index - 1])
                re[index - 1] = max(re[index - 1], (*i)[1]);
            else
            {
                re.push_back((*i)[0]);
                re.push_back((*i)[1]);
                index += 2;
            }
        }
        vector<vector<int>> ret;
        for(int i = 0; i < re.size(); i += 2)
        {
            ret.push_back({re[i], re[i + 1]});
        }
        return ret;
    }
};
```
T(n) : O(nlogn) <br>
S(n) : O(n)

##### 同样思路的一个Solution

空间和时间占用更少

```c++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> ret;
        for(auto& interval : intervals)
        {
            if(ret.empty() || interval[0] > ret.back()[1])
                ret.push_back(interval);
            else
                ret.back()[1] = max(interval[1], ret.back()[1]);
        }
        return ret;
    }
};
```
