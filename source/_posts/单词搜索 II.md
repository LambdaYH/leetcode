---
title: 单词搜索 II
date: 2021-10-11 16:35:53 +0800
categories: leetcode
mathjax: false

---

#### [212. 单词搜索 II](https://leetcode-cn.com/problems/word-search-ii/)

##### 前缀树+df

###### 初始版本

```c++
class Solution {
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        auto root = new TireNode();
        for(auto& word : words)
            insert(root, word);
        int nx = board.size(), ny = board[0].size();
        for(int i = 0; i < nx; ++i)
            for(int j = 0; j < ny; ++j)
                dfs(board, i, j, root, nx, ny);
        vector<string> ret(set.begin(), set.end());
        return ret;
    }
private:
    unordered_set<string> set;
    struct TireNode
    {
        string word;
        unordered_map<char, TireNode*> childs;
    };
    void insert(TireNode* root, string& word)
    {
        auto node = root;
        for(auto ch : word)
        {
            if(!node->childs.count(ch))
                node->childs.emplace(ch, new TireNode());
            node = node->childs[ch];
        }
        node->word = word;
    }
    void dfs(vector<vector<char>>& board, int i, int j, TireNode* node, int nx, int ny)
    {
        if(i < 0 || j < 0 || i >= nx || j >= ny || board[i][j] < 'a')
            return;
        if(!node->childs.count(board[i][j]))
            return;
        node = node->childs[board[i][j]];
        if(!node->word.empty())
            set.emplace(node->word);
        board[i][j] -= 'a';
        dfs(board, i + 1, j, node, nx, ny);
        dfs(board, i - 1, j, node, nx, ny);
        dfs(board, i, j + 1, node, nx, ny);
        dfs(board, i, j - 1, node, nx, ny);
        board[i][j] += 'a';
    }
};
```

![1633941766209.png](https://image.cinte.cc/2021/10/11/b8da12b42cf28.png)

###### 优化后的版本

```c++
class Solution {
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        auto root = new TireNode();
        // 用words中的word构建前缀树
        for(auto& word : words)
            insert(root, word);
        int nx = board.size(), ny = board[0].size();
        for(int i = 0; i < nx; ++i)
            for(int j = 0; j < ny; ++j)
                dfs(board, i, j, root, nx, ny);
        return ret;
    }
private:
    vector<string> ret;
    struct TireNode
    {
        string word;
        TireNode* childs[26]{}; // 不使用hash表而使用数组，可以使得搜索速度更快，但反之也会占用更多空间
    };
    void insert(TireNode* root, string& word)
    {
        auto node = root;
        for(auto ch : word)
        {
            if(!node->childs[ch - 'a'])
                node->childs[ch - 'a'] = new TireNode();
            node = node->childs[ch - 'a'];
        }
        node->word = word;
    }
    void dfs(vector<vector<char>>& board, int i, int j, TireNode* node, int nx, int ny)
    {
        if(i < 0 || j < 0 || i >= nx || j >= ny || board[i][j] == '#')
            return;
        char ch = board[i][j];
        if(!node->childs[ch - 'a'])
            return;
        node = node->childs[ch - 'a']; // 要先过去再判断，因为只有这一步走完后的节点才表示当前ch对应的节点
        if(!node->word.empty())
        {
            ret.emplace_back(node->word);
            node->word.clear(); // 相比将结果放入hash中来去重的方法，这种将走到过的记录为空字符串可以更加节省时间。又可以避免重复录入。
        }
        // 标准的回溯+dfs
        board[i][j] = '#';
        dfs(board, i + 1, j, node, nx, ny);
        dfs(board, i - 1, j, node, nx, ny);
        dfs(board, i, j + 1, node, nx, ny);
        dfs(board, i, j - 1, node, nx, ny);
        board[i][j] = ch;
    }
};
```

![1633941806615.png](https://image.cinte.cc/2021/10/11/47568072d1908.png)
