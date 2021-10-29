---
title: 199. Binary Tree Right Side View
date: 2021-04-08 11:47:36 +0800
categories: leetcode
tags: 
- Tree
---
#### [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)

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
    vector<int> rightSideView(TreeNode* root) {
        if(!root)
            return {};
        vector<int> ret;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty())
        {
            ret.push_back(q.back()->val);
            for(int i = 0, sz = q.size(); i < sz; ++i)
            {
                auto p = q.front();
                q.pop();
                if(p->left)
                    q.push(p->left);
                if(p->right)
                    q.push(p->right);
            }
        }
        return ret;
    }
};
```

T(n) : O(n)
S(n) : O(k)(k为每层数)

##### discussion的方法
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
    vector<int> rightSideView(TreeNode* root) {
        vector<int> ret;
        rightView(ret, root, 0);
        return ret;
    }
private:
    void rightView(vector<int>& ret, TreeNode* node, int depth)
    {
        if(!node)
            return;
        
        if(depth == ret.size()) // 如果当depth != ret.size()时return，则会导致传递的终止，不行，当不等时候，那就继续遍历下去，说不定下面一层又轮到你了
            ret.push_back(node->val);
        
        rightView(ret, node->right, depth + 1);
        rightView(ret, node->left, depth + 1);
    }
};
```
O(logn)
总体思路是每层只添加一个，然后仅当每层没添加时才会添加进去，而层数通过ret的大小来判定，由于是从右到左遍历，因此每层添加的一定是最右的
