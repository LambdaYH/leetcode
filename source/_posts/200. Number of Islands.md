---
title: 200. Number of Islands
date: 2021-04-13 14:26:01 +0800
categories: leetcode
tags: 
- DFS
- Union Find
---
#### [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

##### DFS
```c++
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        int count{ 0 };
        for(int i = 0; i < grid.size(); ++i)
        {
            for(int j = 0; j < grid[0].size(); ++j)
            {
                if(grid[i][j] == '1')
                {
                    dfs(grid, i, j);
                    ++count;
                }
            }
        }
        return count;
    }
    void dfs(vector<vector<char>>& grid, int i, int j)
    {
        if(i < 0 || j < 0 || i >= grid.size() || j >= grid[0].size() || grid[i][j] != '1')
            return;
        grid[i][j] = '.';
        dfs(grid, i + 1, j);
        dfs(grid, i, j + 1);
        dfs(grid, i - 1, j);
        dfs(grid, i, j - 1);
    }
};
```

深度优先遍历，当遇到一块陆地后，向周围遍历，遍历过的土地做上标记防止重复遍历，当遍历完一整块岛后，返回，计数加一

##### 使用[并查集](https://zh.wikipedia.org/wiki/%E5%B9%B6%E6%9F%A5%E9%9B%86)

对discuss中的代码加以批注

```java
    int[][] distance = {{1,0},{-1,0},{0,1},{0,-1}}; // 4个方向
    public int numIslands(char[][] grid) {  
        if (grid == null || grid.length == 0 || grid[0].length == 0)  {
            return 0;  
        }
        UnionFind uf = new UnionFind(grid);  
        int rows = grid.length;  
        int cols = grid[0].length;  
        for (int i = 0; i < rows; i++) {  
            for (int j = 0; j < cols; j++) {  
                if (grid[i][j] == '1') {  // 当遇上陆地
                    for (int[] d : distance) { // 陆地的4个方向进行遍历
                        int x = i + d[0]; 
                        int y = j + d[1];
                        if (x >= 0 && x < rows && y >= 0 && y < cols && grid[x][y] == '1') { // 当且仅当是陆地时进入循环
                            int id1 = i*cols+j; // 当前陆地的id ，展开成1维表示
                            int id2 = x*cols+y; // 周围陆地的id，同样是展开成一维
                            uf.union(id1, id2); // 进行并查，具体见UnionFind CLASS
                        }  
                    }  
                }  
            }  
        }  
        return uf.count;  
    }
```

Union Find:

```java
    class UnionFind {
        int[] father;  
        int m, n;
        int count = 0;
        UnionFind(char[][] grid) {  
            m = grid.length;  
            n = grid[0].length;  
            father = new int[m*n];  
            for (int i = 0; i < m; i++) {  
                for (int j = 0; j < n; j++) {  
                    if (grid[i][j] == '1') {
                        int id = i * n + j;
                        father[id] = id; // 对每一个陆地初始化，初始化后，每个陆地都各自分为一类
                        count++; // 在归并之前，总数
                    }
                }  
            }  
        }
        public void union(int node1, int node2) {  
            int find1 = find(node1); // 查找node 1 和 node 2属于哪一类
            int find2 = find(node2);
            if(find1 != find2) {
                father[find1] = find2; // 由于二者是邻接的陆地，因此当二者属于的类不同时，将其合并
                count--; // 2块陆地合并，计数减一
            }
        }
        // 递归查找所属的类，直到查找到其所属的最顶端类
        public int find (int node) {
            if (father[node] == node) {  
                return node;
            }
            father[node] = find(father[node]);  
            return father[node];
        }
    }
```
