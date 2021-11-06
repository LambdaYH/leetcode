---
title: 剑指 Offer 37. 序列化二叉树
date: 2021-06-30 10:11:35 +0800
categories: 剑指 Offer
mathjax: false
---
#### [剑指 Offer 37. 序列化二叉树](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/)

#####
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
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        if(!root)
            return "";
        queue<TreeNode*> q;
        q.push(root);
        string ret = "";
        while(!q.empty())
        {
            for(int i = 0, j = q.size(); i < j; ++i)
            {
                auto p = q.front();
                q.pop();
                if(p)
                {
                    ret += to_string(p->val);
                    q.push(p->left);
                    q.push(p->right);
                }else
                {
                    ret += "n";
                }
                ret += ",";
            }
        }
        return ret;
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        if(data == "")
            return nullptr;
        TreeNode* ret = nullptr;
        queue<TreeNode*> q;
        queue<char> s;
        int i = 0;
        for(; i < data.size(); ++i)
        {
            if(data[i] == ',')
            {
                int tmp = 0;
                bool pos = true;
                while(!s.empty())
                {
                    if(s.front() == '-')
                        pos = false;
                    else
                        tmp = tmp * 10 + s.front() - '0';
                    s.pop();
                }
                ret = new TreeNode(pos ? tmp : -tmp);
                q.push(ret);
                break;
            }else
                s.push(data[i]);
        }
        ++i;
        int cur = 0;
        for(; i < data.size(); ++i)
        {
            if(data[i] == ',')
            {
                auto p = q.front();              
                TreeNode* node = nullptr;
                if(s.front() == 'n')
                    s.pop();
                else
                {
                    int tmp = 0;
                    bool pos = true;
                    while(!s.empty())
                    {
                        if(s.front() == '-')
                            pos = false;
                        else
                            tmp = tmp * 10 + s.front() - '0';
                        s.pop();
                    }
                    node = new TreeNode(pos ? tmp : -tmp);
                }
                if(cur++ == 0)
                    p->left = node;
                else
                {
                    p->right = node;
                    q.pop();
                    cur = 0;
                }
                if(node)
                    q.push(node);
            }else
                s.push(data[i]);
        }
        return ret;
    }
};

// Your Codec object will be instantiated and called as such:
// Codec codec;
// codec.deserialize(codec.serialize(root));
```

review
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
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        if(!root)
            return "";
        string ret;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty())
        {
            auto p = q.front();
            q.pop();
            if(p)
            {
                q.push(p->left);
                q.push(p->right);
                ret += to_string(p->val);
            }
            else
                ret += "n";
            ret += ",";
        }
        return ret;
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        if(data.empty())
            return nullptr;
        TreeNode* root = nullptr;
        TreeNode* ret;
        int start = 0, end = 0;
        int n = data.size();
        bool left = false;
        queue<TreeNode*> q;
        while(end < n)
        {
            if(data[end] == ',')
            {
                auto str = data.substr(start, end - start);
                TreeNode* node = nullptr;
                if(str != "n")
                {
                    node = new TreeNode(stoi(str));
                    q.push(node);
                }
                if(!root)
                {
                    root = node;
                    ret = root;
                }else
                {
                    if(!left)
                    {
                        root->left = node;
                        left = true;
                    }
                    else
                    {
                        root->right = node;
                        left = false;
                        q.pop();
                        root = q.front();
                    }
                }
                start = end + 1;
            }
            ++end;
        }
        return ret;
    }
};

// Your Codec object will be instantiated and called as such:
// Codec codec;
// codec.deserialize(codec.serialize(root));
```
