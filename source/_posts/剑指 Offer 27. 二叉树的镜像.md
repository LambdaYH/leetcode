---
title: 剑指 Offer 27. 二叉树的镜像
date: 2021-06-21 15:16:55 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 27. 二叉树的镜像](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)

##### 递归
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
    TreeNode* mirrorTree(TreeNode* root) {
        if(!root)
            return nullptr;
        swap(root->left, root->right);
        mirrorTree(root->left);
        mirrorTree(root->right);
        return root;
    }
};
```

##### 迭代
```
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
    TreeNode* mirrorTree(TreeNode* root) {
        if(!root)
            return nullptr;
        stack<TreeNode*> s;
        s.push(root);
        while(!s.empty())
        {
            auto p = s.top();
            s.pop();
            if(p->left)
                s.push(p->left);
            if(p->right)
                s.push(p->right);
            swap(p->right, p->left);
        }        
        return root;
    }
};
```
