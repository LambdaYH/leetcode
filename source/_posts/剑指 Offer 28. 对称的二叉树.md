---
title: 剑指 Offer 28. 对称的二叉树
date: 2021-06-21 17:17:05 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 28. 对称的二叉树](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

##### 递归
```C++
//**
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
    bool isSymmetric(TreeNode* root) {
        if(!root)
            return true;
        return helper(root->left, root->right);
    }
private:
    bool helper(TreeNode* node1, TreeNode* node2)
    {
        if(!node1 && !node2)
            return true;
        if(!node1 || !node2 || node1->val != node2->val)
            return false;
        return helper(node1->left, node2->right) && helper(node1->right, node2->left); 
    }
};
```

##### 迭代
```C++
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
    bool isSymmetric(TreeNode* root) {
        if(!root)
            return true;
        queue<TreeNode*> q;
        q.push(root);
        q.push(root);
        while(!q.empty())
        {
            auto p1 = q.front();
            q.pop();
            auto p2 = q.front();
            q.pop();
            if(!p1 && !p2)
                continue;
            if(!p1 || !p2 || p1->val != p2->val)
                return false;
            q.push(p1->left);
            q.push(p2->right);
            q.push(p1->right);
            q.push(p2->left);
        }
        return true;
    }
};
```
