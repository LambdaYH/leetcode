---
title: 剑指 Offer 68 - I. 二叉搜索树的最近公共祖先
date: 2021-07-12 15:49:54 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 68 - I. 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

参考[236. Lowest Common Ancestor of a Binary Tree](https://leetcode.cinte.cc/2021/04/22/236-Lowest-Common-Ancestor-of-a-Binary-Tree/)

但因为这题是BST，所以有别的方法

以下情况:

1. 当p，q都在root左侧，那么p，q都在root左子树。
2. 当p，q都在root右侧，那么p，q都在root右子树。
3. 当第一次产生没在同一个子树时，这时候的root就是解
   1. p或q为root，剩下的在一边的树
   2. p，q在root两侧

##### 迭代
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
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        while(root)
        {
            if(root->val > p->val && root->val > q->val)
                root = root->left;
            else if(root->val < p->val && root->val < q->val)
                root = root->right;
            else
                return root;
        }
        return nullptr;
    }
};
```

##### 递归
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
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
            if(root->val > p->val && root->val > q->val)
                return lowestCommonAncestor(root->left, p, q);
            else if(root->val < p->val && root->val < q->val)
                return lowestCommonAncestor(root->right, p, q);
            return root;
    }
};
```
