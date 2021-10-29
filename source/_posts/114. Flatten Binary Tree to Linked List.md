---
title: 114. Flatten Binary Tree to Linked List
date: 2021-04-18 17:41:42 +0800
categories: leetcode
tags: Tree
---
#### [114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)

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
 // preorder traversal 是 root -> left -> right
 // 此方法是将左子树插入到root 和 右子树中间。
class Solution {
public:
    void flatten(TreeNode* root) {
        TreeNode* now = root; // 当前节点
        while(now)
        {
            // 如果当前节点存在左子树，则需要优先遍历
            if(now->left) 
            {
                TreeNode* pre = now->left;
                // 将pre指针移到左子树的右子树的最右端
                while(pre->right)
                {
                    pre = pre->right;
                }
                // 使右子树最末端的右边只想原节点的左子树
                pre->right = now->right;
                // 将源节点的右边指向左边
                now->right = now->left;
                // 上述的操作之后，root的右子树是原来的左子树
                now->left = nullptr;
            }
            // 走到下一个节点，顺序始终是先左后右
            now = now->right;
        }
    }
};
```

太强了
