---
title: 95. Unique Binary Search Trees II
date: 2021-04-04 16:45:13 +0800
categories: leetcode
tags: 
- Dynamic Programming
---
#### [95. Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/)

##### dp
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
    vector<TreeNode*> generateTrees(int n) {
        vector<vector<TreeNode*>> dp(n + 1);
        dp[0] = {nullptr};
        for(size_t i = 1; i <= n; ++i)
        {
            for(size_t j = 1; j <= i; ++j)
            {
                for(auto& nodeLeft : dp[j - 1])
                {
                    for(auto& nodeRight : dp[i - j])
                    {
                        TreeNode* tmp = new TreeNode(j);
                        tmp->left = nodeLeft;
                        tmp->right = clone(nodeRight, j);
                        dp[i].push_back(tmp);
                    }
                }
            }
        }
        return dp.back();
    }
private:
    TreeNode* clone(TreeNode* root, int offset)
    {
        if(!root)
            return nullptr;
        TreeNode* newNode = new TreeNode(root->val + offset);
        newNode->left = clone(root->left, offset);
        newNode->right = clone(root->right, offset);
        return newNode;
    }
};
```

和[Unique Binary Search Trees](https://blog.cinte.cc/2021/03/31/96-Unique-Binary-Search-Trees/)相似，只不过这个要列举出所有节点
