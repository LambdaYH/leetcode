---
title: 236. Lowest Common Ancestor of a Binary Tree
date: 2021-04-22 16:56:02 +0800
categories: leetcode
tags: Tree
---
#### [236. Lowest Common Ancestor of a Binary Tree](2021-04-22 16:55:59 +0800)

##### DFS
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
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        TreeNode* ret = nullptr;
        backTrack(root, p, q, ret);
        return ret;
    }
private:
    bool backTrack(TreeNode* node, TreeNode* p, TreeNode* q, TreeNode*& ret)
    {
        if(!node)
            return false;
        // 设置为1的话就可以隐藏细节，仅仅那个最近的具有最丰富的细节，往上就没了，所以上面就不会再覆盖之前的结果
        int mid = (node == p || node == q) ? 1 : 0;
        int left = backTrack(node->left, p, q, ret) ? 1: 0;
        int right = backTrack(node->right, p, q, ret) ? 1 : 0;
        if(mid + left + right >= 2)
        {
            ret = node;   
        }
        return mid + left + right;
    }
};
```

抄的solution
T(n) : O(n) <br>
S(n) : O(n)&nbsp;递归堆栈的大小

判断每个节点，当某一结点左边和右边或左边和中间或右边和中间包含目标时，返回那个节点

##### 记录父亲再去遍历
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
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        unordered_map<TreeNode*, TreeNode*> parent;
        parent[root] = nullptr;
        stack<TreeNode*> s;
        s.push(root);
        while(parent.find(p) == parent.end() || parent.find(q) == parent.end())
        {
            auto tmp = s.top();
            s.pop();
            if(tmp->right)
            {
                parent[tmp->right] = tmp;
                s.push(tmp->right);
            }
            if(tmp->left)
            {
                parent[tmp->left] = tmp;
                s.push(tmp->left);
            }
        }
        
        unordered_set<TreeNode*> ancestor;
        while(parent.find(p) != parent.end())
        {
            ancestor.insert(p);
            p = parent[p];
        }
        
        while(ancestor.find(q) == ancestor.end())
        {
            q = parent[q];
        }
        return q;
    }    
};
```
T(n) : O(n) <br>
S(n) : O(n)
