---
title: 剑指 Offer 34. 二叉树中和为某一值的路径
date: 2021-07-03 16:28:55 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

##### BackTrack
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
    vector<vector<int>> pathSum(TreeNode* root, int target) {
        vector<int> tmp;
        helper(root, target, 0, tmp);
        return ret;
    }
private:
    vector<vector<int>> ret;
    void helper(TreeNode* root, const int& target, int cur, vector<int>& tmp)
    {
        if(!root)
            return;
        cur += root->val;
        tmp.push_back(root->val);
        if(cur == target && !root->left && !root->right)
        {
            ret.push_back(tmp);
        }
        helper(root->right, target, cur, tmp);
        helper(root->left, target, cur, tmp);
        tmp.pop_back();
    }
};
```

