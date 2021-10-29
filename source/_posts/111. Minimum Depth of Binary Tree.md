---
title: 111. Minimum Depth of Binary Tree
date: 2021-04-10 10:26:06 +0800
categories: leetcode
tags: Tree
---
#### [111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
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
    int minDepth(TreeNode* root) {
        if(!root) return 0;
        int depth{ INT_MAX };
        int tmp{ 1 };
        backTrack(root, depth, tmp);
        return depth;
    }
private:
    void backTrack(TreeNode* root, int& depth, int& tmp)
    {
        if(!root) return;
        if(!root->left && !root->right)
        {
            depth = min(depth, tmp);
            return;
        }
        ++tmp;
        backTrack(root->left, depth, tmp);
        backTrack(root->right, depth, tmp);
        --tmp;
    }
};
```

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
    int minDepth(TreeNode* root) {
        if(!root)
            return 0;
        if(!root->left)
            return minDepth(root->right) + 1; // 针对不是叶子节点的情况，不能因为当前是根而干扰结果
        if(!root->right)
            return minDepth(root->left) + 1; // 针对不是叶子节点的情况，不能因为当前是根而干扰结果
        return min(minDepth(root->left), minDepth(root->right)) + 1; // 如果当前是子树的根节点，那么会导致结果终止于这个根。所以上面2个if是保证在当前节点不是叶子节点情况下继续往下走。
    }
};
```
##### BFS
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
    int minDepth(TreeNode* root) {
        if(!root) return 0;
        queue<TreeNode*> q;
        q.push(root);
        int depth{ 0 };
        while(!q.empty())
        {
            ++depth;
            auto sz = q.size();
            for(size_t i = 0; i < sz; ++i)
            {
                auto p = q.front();
                q.pop();
                if(p->left)
                    q.push(p->left);
                if(p->right)
                    q.push(p->right);
                if(!p->left && !p->right)
                    return depth;
            }
        }
        return depth;
    }
};
```
