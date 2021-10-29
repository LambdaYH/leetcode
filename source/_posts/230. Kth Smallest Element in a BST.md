---
title: 230. Kth Smallest Element in a BST
date: 2021-04-19 21:20:28 +0800
categories: leetcode
tags: Tree
---
#### [114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

##### 我越来越菜了
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
    int kthSmallest(TreeNode* root, int k) {
        stack<TreeNode*> s;
        s.push(root);
        TreeNode* cur = root;
        int i{ 0 };
        while(cur || !s.empty())
        {
            while(cur)
            {
                s.push(cur);
                cur = cur->left;
            }
            cur = s.top();
            s.pop();
            if(++i == k)
                return cur->val;
            cur = cur->right;
        }
        return 0;
    }
};
```

in-order 遍历就是从小到大的排序，因此只需要进行in-order遍历

中序遍历中先把最左边的加进栈，然后走一个节点的右边。当没有右树的就会进入下一个循环走到上一个树

##### inorder递归
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
    int kthSmallest(TreeNode* root, int k) {
        int ret;
        inorder(root, ret, k);
        return ret;
    }
private:
    void inorder(TreeNode* root, int& ret, int& k)
    {
        if(!root)
            return;
        inorder(root->left, ret, k);
        if(--k == 0)
        {
            ret = root->val;
            return;
        }
        inorder(root->right, ret, k);
    }
};
```
