---
title: 剑指 Offer 32 - III. 从上到下打印二叉树 III
date: 2021-07-02 20:05:50 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 32 - III. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

##### 双向队列
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
    vector<vector<int>> levelOrder(TreeNode* root) {
        if(!root)
            return {};
        vector<vector<int>> ret;
        deque<TreeNode*> dq;
        bool left = false;
        dq.push_front(root);
        while(!dq.empty())
        {
            vector<int> tmp;
            for(int i = 0, j = dq.size(); i < j; ++i)
            {
                if(left)
                {
                    auto p = dq.back();
                    dq.pop_back();
                    tmp.push_back(p->val);
                    if(p->right)
                        dq.push_front(p->right);
                    if(p->left)
                        dq.push_front(p->left);
                }else
                {
                    auto p = dq.front();
                    dq.pop_front();
                    tmp.push_back(p->val);
                    if(p->left)
                        dq.push_back(p->left);
                    if(p->right)
                        dq.push_back(p->right);
                }
            }
            ret.push_back(tmp);
            left = !left;
        }
        return ret;

    }
};
```

##### 省去多余判断
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
    vector<vector<int>> levelOrder(TreeNode* root) {
        if(!root)
            return {};
        vector<vector<int>> ret;
        deque<TreeNode*> dq;
        bool left = false;
        dq.push_front(root);
        while(!dq.empty())
        {
            vector<int> tmp2;
            for(int i = 0, j = dq.size(); i < j; ++i)
            {
                auto p = dq.front();
                dq.pop_front();
                tmp2.push_back(p->val);
                if(p->left)
                    dq.push_back(p->left);
                if(p->right)
                    dq.push_back(p->right);
            }
            ret.push_back(tmp2);
            if(dq.empty())
                break;
            vector<int> tmp;
            for(int i = 0, j = dq.size(); i < j; ++i)
            {
                auto p = dq.back();
                dq.pop_back();
                tmp.push_back(p->val);
                if(p->right)
                    dq.push_front(p->right);
                if(p->left)
                    dq.push_front(p->left);
            }
            ret.push_back(tmp);
        }
        return ret;

    }
};
```
