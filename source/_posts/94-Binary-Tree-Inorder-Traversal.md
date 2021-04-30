---
title: 94. Binary Tree Inorder Traversal
date: 2021-04-07 20:34:47 +0800
categories: leetcode
tags: 
- Tree
---
#### [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ret;
        traversal(ret, root);
        return ret;
    }
private:
    void traversal(vector<int>& ret, TreeNode* root)
    {
        if(!root) return;
        traversal(ret, root->left);  
        ret.push_back(root->val);        
        traversal(ret, root->right);
    }
};
```
T(n) : O(n)<br>
S(n) : O(n)


##### stack
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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ret;
        stack<TreeNode*> s;
        TreeNode* cur = root;
        while(cur || !s.empty())
        {
            while(cur)
            {
                s.push(cur);
                cur = cur->left;
            }
            cur = s.top();
            s.pop();
            ret.push_back(cur->val);
            cur = cur->right;
        }
        return ret;
    }
};
```
