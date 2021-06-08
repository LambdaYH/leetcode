---
title: 10
date: 2021-06-09 01:44:16 +0800
categories: leetcode
tags: 
- Tree
---
#### [101. Syttps://leetcode.com/problems/symmetric-tree/)

##### recursively
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
    bool isSymmetric(TreeNode* root) {
        return isTwoTreesSymmetric(root->left, root->right);
    }
private:
    bool isTwoTreesSymmetric(TreeNode* lTree, TreeNode* rTree)
    {
        if((!lTree && rTree) || (!rTree && lTree))
            return false;
        if(!lTree && !rTree)
            return true;
        if(lTree->val == rTree->val)
            return isTwoTreesSymmetric(lTree->left, rTree->right) && isTwoTreesSymmetric(lTree->right, rTree->left);
        return false;
    }
};
```

##### iteratively queue
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
    bool isSymmetric(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root);
        q.push(root);
        while(!q.empty())
        {
            auto t1 = q.front();
            q.pop();
            auto t2 = q.front();
            q.pop();
            if(!t1 && !t2) continue;
            if(!t1 || !t2) return false;
            if(t1->val != t2->val) return false;
            q.push(t1->left);
            q.push(t2->right);
            q.push(t1->right);
            q.push(t2->left);
        }
        return true;
    }
};
```

##### iteratively stack
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
    bool isSymmetric(TreeNode* root) {
        stack<TreeNode*> s;
        s.push(root);
        s.push(root);
        while(!s.empty())
        {
            auto t1 = s.top();
            s.pop();
            auto t2 = s.top();
            s.pop();
            if(!t1 && !t2) continue;
            if(!t1 || !t2) return false;
            if(t1->val != t2->val) return false;
            s.push(t1->left);
            s.push(t2->right);
            s.push(t1->right);
            s.push(t2->left);
        }
        return true;
    }
};
```
