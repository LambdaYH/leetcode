---
title: 剑指 Offer 55 - II. 平衡二叉树
date: 2021-07-12 10:51:00 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 55 - II. 平衡二叉树](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/)

##### dfs
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        if(!root)
            return true;
        auto left = dfs(root->left);
        auto right = dfs(root->right);
        if(abs(left - right) <= 1 && isBalanced(root->left) && isBalanced(root->right))
            return true;
        return false;
    }
private:
    int dfs(TreeNode* root)
    {
        if(!root)
            return 0;
        return max(dfs(root->left), dfs(root->right)) + 1;
    }
};
```

##### 剪枝
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        return dfs(root) != -1;
    }
private:
    int dfs(TreeNode* root)
    {
        if(!root)
            return 0;
        auto left = dfs(root->left);
        if(left == -1)
            return -1;
        auto right = dfs(root->right);
        if(right == -1)
            return -1;
        if(abs(left - right) > 1)
            return - 1;
        return max(left, right) + 1;
    }
};
```
