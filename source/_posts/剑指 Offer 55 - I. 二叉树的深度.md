---
title: 剑指 Offer 55 - I. 二叉树的深度
date: 2021-07-05 11:03:30 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 55 - I. 二叉树的深度](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

参考[104. Maximum Depth of Binary Tree](https://leetcode.cinte.cc/2021/04/09/104-Maximum-Depth-of-Binary-Tree/)

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
    int maxDepth(TreeNode* root) {
        if(!root)
            return 0;
        return max(maxDepth(root->left), maxDepth(root->right)) + 1;
    }
};
```

