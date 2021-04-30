---
title: 543. Diameter of Binary Tree
date: 2021-04-13 16:39:37 +0800
categories: leetcode
tags: 
- Tree
---
#### [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

##### 遍历
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
    int diameterOfBinaryTree(TreeNode* root) {
        if(!root) return 0;
        queue<TreeNode*> q;
        q.push(root);
        int ret = 0;
        while(!q.empty())
        {
            auto p = q.front();
            q.pop();
            int dL = 0, dR = 0;
            if(p->left)
            {
                q.push(p->left);
                maxDepth(p->left, dL, 0);
            }
            if(p->right)
            {
                q.push(p->right);
                maxDepth(p->right, dR, 0);
            }
            ret = max(ret, dL + dR);
        }
        return ret;
    }
private:
    void maxDepth(TreeNode* root, int& depth, int tmp)
    {
        if(!root)
            return;
        ++tmp;
        depth = max(tmp, depth);
        maxDepth(root->left, depth, tmp);
        maxDepth(root->right, depth, tmp);
        --tmp;
    }
};
```

##### 顺路计算完所有的点
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
    int diameterOfBinaryTree(TreeNode* root) {
        int maxDepth = 0;
        longest(root, maxDepth);
        return maxDepth;
    }
private:
    int longest(TreeNode* root, int &maxDepth)
    {
        if(!root) return 0;
        
        int left = longest(root->left, maxDepth);
        int right = longest(root->right, maxDepth);
        
        maxDepth = max(maxDepth, left + right);
        return max(left, right) + 1;
    }
};
```
