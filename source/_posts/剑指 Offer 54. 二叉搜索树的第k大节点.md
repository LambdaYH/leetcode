---
title: 剑指 Offer 54. 二叉搜索树的第k大节点
date: 2021-07-08 20:59:27 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 54. 二叉搜索树的第k大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

##### 左右反着来中序
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
    int kthLargest(TreeNode* root, int k) {
        stack<TreeNode*> q;
        while(!q.empty() || root)
        {
            while(root)
            {
                q.push(root);
                root = root->right;
            }
            root = q.top();
            q.pop();
            if(--k == 0)
                return root->val;
            root = root->left;
        }
        return 0;
    }
};
```
