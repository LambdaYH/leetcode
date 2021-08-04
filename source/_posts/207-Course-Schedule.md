---
title: 207. Course Schedule
date: 2021-04-21 21:06:25 +0800
categories: leetcode
tags: Graph
---
#### [207. Course Schedule](https://leetcode.com/problems/course-schedule/)

##### DFS
```c++
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> map(numCourses);
        vector<bool> done(numCourses, false); // 记录走过的点，如果走到了这个点并标记为true，表示通过这个点可以走回去
        vector<bool> todo(numCourses, false); // 记录在走路过程中走过的点，如果走路过程中撞到了，表明有环，那么必定返回false
        for(auto& course : prerequisites)
        {
            map[course[1]].push_back(course[0]); // 建立有向图,注意方向  review : 其实主要是判断环路，方向无所谓啦
        }
        for(int i = 0; i < numCourses; ++i)
        {
            if(!helper(map, i, todo, done))
                return false;
        }
        return true;
    }
private:
    bool helper(vector<vector<int>>& map, int index, vector<bool>& todo, vector<bool>& done)
    {
        if(todo[index]) // 撞到了 失败了
            return false;
        if(done[index])
            return true; // 因为如果这条路不能走的话，之前就已经返回false了，所以再次走到肯定是安全的
        
        done[index] = true; // 走了这个点
        todo[index] = true; // 走到了这个点
        for(auto& i : map[index])
        {
            if(!helper(map, i, todo, done))
            {
                return false; 
            }
        }
        todo[index] = false; // 这趟走完了，没有发现环，这条路是安全的
        return true;
    }
};
```

对于每个点都是一条路走到黑，所以是DFS

##### review
```c++
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int> visited(numCourses, 0);
        vector<int> checked(numCourses, 0); // 0 : unknown, 1 : ok
        vector<vector<int>> graph(numCourses);
        for(auto& c : prerequisites)
            graph[c[0]].push_back(c[1]);
        for(int i = 0; i < numCourses; ++i)
            if(!check(graph, visited, checked, i))
                return false;
        return true;
    }
private:
    bool check(vector<vector<int>>& graph, vector<int>& visited, vector<int>& checked, int course)
    {
        if(checked[course] == 1)
            return true;
        if(visited[course])
            return false;
        visited[course] = 1;
        for(auto& c : graph[course])
        {
            if(!check(graph, visited, checked, c))
                return false;
        }
        visited[course] = 0;
        checked[course] = 1;
        return true;
    }
};
```
