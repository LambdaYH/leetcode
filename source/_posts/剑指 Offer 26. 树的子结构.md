---
title: 剑指 Offer 26. 树的子结构
date: 2021-06-18 21:19:15 +0800
categories: 剑指 Offer
---
#### [剑指 Offer 26. 树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)

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
    bool isSubStructure(TreeNode* A, TreeNode* B) {
        if(!B || !A)
            return false;
        if(A->val == B->val && helper(A->left, B->left) && helper(A->right, B->right))
            return true;
        return isSubStructure(A->left, B) || isSubStructure(A->right, B);
    }
private:
    bool helper(TreeNode* A, TreeNode* B)
    {
        if(!B)
            return true;
        if(!A)
            return false;
        if(A->val != B->val)
            return false;
        return helper(A->left, B->left) && helper(A->right, B->right);
        
    }

};
```

遍历树，碰到A中值和B根相同的点就去递归判断是不是相同子树

情况如下

1. 当A为空B非空，则`false`
2. 当B为空A非空，则便利结束，为`true`
3. 当A值!=B值，则`false`
4. A值==B值，继续判断
