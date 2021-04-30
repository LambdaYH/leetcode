---
title: 105. Construct Binary Tree from Preorder and Inorder Traversal
date: 2021-04-11 21:18:50 +0800
categories: leetcode
tags: 
- Tree
---
#### [105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

太难了

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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int index = 0;
        for(int i = 0; i < inorder.size(); ++i)
        {
            map[inorder[i]] = i;
        }
        return tree(preorder, 0, preorder.size() - 1, index);
    }
private:
    unordered_map<int, int> map;
    TreeNode* tree(vector<int>& preorder, int left, int right, int& index)
    {
        if(left > right)
            return nullptr;
        
        int val = preorder[index++];
        TreeNode* root = new TreeNode(val);
        root->left = tree(preorder, left, map[val] - 1, index);
        root->right = tree(preorder, map[val] + 1, right, index);
        
        return root;
    }
};
```

每个在preorder中的点在inorder中的左边都是左树，右边是右树

The two key observations are:

1. Preorder traversal follows Root -> Left -> Right, therefore, given the preorder array preorder, we have easy access to the root which is preorder[0].

2. Inorder traversal follows Left -> Root -> Right, therefore if we know the position of Root, we can recursively split the entire array into two subtrees.
