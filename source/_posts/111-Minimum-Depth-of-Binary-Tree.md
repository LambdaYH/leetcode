---
title: 111. Minimum Depth of Binary Tree
date: 2021-04-10 10:26:06 +0800
categories: leetcode
tags: Tree
---
#### [111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(!root) return 0;
        int depth{ INT_MAX };
        int tmp{ 1 };
        backTrack(root, depth, tmp);
        return depth;
    }
private:
    void backTrack(TreeNode* root, int& depth, int& tmp)
    {
        if(!root) return;
        if(!root->left && !root->right)
        {
            depth = min(depth, tmp);
            return;
        }
        ++tmp;
        backTrack(root->left, depth, tmp);
        backTrack(root->right, depth, tmp);
        --tmp;
    }
};
```

##### BFS
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(!root) return 0;
        queue<TreeNode*> q;
        q.push(root);
        int depth{ 0 };
        while(!q.empty())
        {
            ++depth;
            auto sz = q.size();
            for(size_t i = 0; i < sz; ++i)
            {
                auto p = q.front();
                q.pop();
                if(p->left)
                    q.push(p->left);
                if(p->right)
                    q.push(p->right);
                if(!p->left && !p->right)
                    return depth;
            }
        }
        return depth;
    }
};
```
