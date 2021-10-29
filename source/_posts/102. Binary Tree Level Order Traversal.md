---
title: 102. Binary Tree Level Order Traversal
date: 2021-04-10 19:09:35 +0800
categories: leetcode
tags: Tree
---
#### [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
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
    vector<vector<int>> levelOrder(TreeNode* root) {
        if(!root) return {};
        vector<vector<int>> ret;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty())
        {
            vector<int> tmp;
            for(int i = 0, n = q.size(); i < n; ++i)
            {
                auto p = q.front();
                q.pop();
                tmp.push_back(p->val);
                if(p->left)
                    q.push(p->left);
                if(p->right)
                    q.push(p->right);
            }
            ret.push_back(tmp);
        }
        return ret;
    }
};
```

![image.png](https://image.cinte.cc/2021/04/10/0dbfdf01ef05f.png)


还有使用递归，传入层数，对每一层的vector容器加入
