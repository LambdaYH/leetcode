---
title: 剑指 Offer 32 - I. 从上到下打印二叉树
date: 2021-07-01 20:17:45 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 32 - I. 从上到下打印二叉树](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

#####
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
    vector<int> levelOrder(TreeNode* root) {
        if(!root)
            return {};
        queue<TreeNode*> q;
        vector<int> ret;
        q.push(root);
        while(!q.empty())
        {
            auto p = q.front();
            q.pop();
            ret.push_back(p->val);
            if(p->left)
                q.push(p->left);
            if(p->right)
                q.push(p->right);
        }
        return ret;
    }
};
```
