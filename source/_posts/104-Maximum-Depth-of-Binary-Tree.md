---
title: 104. Maximum Depth of Binary Tree
date: 2021-04-10 10:14:56 +0800
categories: leetcode
tags: Tree
---
#### [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
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
    int maxDepth(TreeNode* root) {
        int depth{ 0 };
        int tmp{ 0 };
        backTrack(root, depth, tmp);
        return depth;
    }
private:
    void backTrack(TreeNode* root, int& depth, int& tmp)
    {
        if(!root) return;
        ++tmp;
        depth = max(depth, tmp);
        backTrack(root->left, depth, tmp);
        backTrack(root->right, depth, tmp);
        --tmp;
    }
};
```

待优化空间占用
