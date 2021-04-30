---
title: 337. House Robber III
date: 2021-04-24 14:57:38 +0800
categories: leetcode
tags: 
- Tree
- Dynamic Programming
---
#### [337. House Robber III](https://leetcode.com/problems/binary-tree-level-order-traversal/)

对于一个节点来说，如果rob这个点，那么他的child就不能rob, 如果不rob，那么他的child可以rob也可以不rob<br>
对于rob这个节点来说，需要计算他的grandchild rob或者不rob的情况，不rob时也需要计算，如果递归则需要重复计算，因此每次的递归函数都计算这一个rob和不rob的情况<br>
用pair保存起来rob和不rob的记过

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
    int rob(TreeNode* root) {
        auto ret = helper(root);
        return max(ret.first, ret.second);
    }
private:
    pair<int, int> helper(TreeNode* node)
    {
        if(!node)
            return {0, 0};
        
        auto left = helper(node->left);
        auto right = helper(node->right);
        
        // if rob
        int rob = node->val + left.second + right.second;
        int notRob = max(left.first, left.second) + max(right.first, right.second);
        
        return {rob, notRob};
    }
};
```

##### approach 1 未改进前的算法使用memo优化
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
    int rob(TreeNode* root) {
        return max(helper(root, false), helper(root, true));
    }
private:
    unordered_map<TreeNode*, int> robed;
    unordered_map<TreeNode*, int> noRobed;
    int helper(TreeNode* node, bool isRobed)
    {
        if(!node)
            return 0;
        if(isRobed)
        {
            if(robed.find(node) != robed.end())
                return robed[node];
            else
            {
                int left = helper(node->left, false);
                int right = helper(node->right, false);
                int ret = node->val + left + right;
                robed[node] = ret;
                return ret;
            }
        }else
        {
            if(noRobed.find(node) != noRobed.end())
                return noRobed[node];
            else
            {
                int left = max(helper(node->left, false), helper(node->left, true));
                int right = max(helper(node->right, false), helper(node->right, true));
                int ret = left + right;
                noRobed[node] = ret;
                return ret;
            }
        }
    }
};
```

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
    int rob(TreeNode* root) {
        unordered_map<int, vector<int>> pc;
        vector<int> val;
        queue<TreeNode*> qNode;
        queue<int> qIndex;
        int index = -1;
        qNode.push(root);
        qIndex.push(index);
        while(!qNode.empty())
        {
            auto node = qNode.front();
            qNode.pop();
            auto fatherI = qIndex.front();
            qIndex.pop();
            if(node)
            {
                ++index;
                pc[fatherI].push_back(index);
                val.push_back(node->val);
                qNode.push(node->left);
                qNode.push(node->right);
                qIndex.push(index);
                qIndex.push(index);
            }
        }
        vector<int> dpRob(index + 1);
        vector<int> dpNoRob(index + 1);
        
        for(int i = index; i >= 0; --i)
        {
            if(pc[i].empty())
            {
                dpRob[i] = val[i];
                dpNoRob[i] = 0;
            }else
            {
                dpRob[i] = val[i];
                for(auto& j : pc[i])
                {
                    dpRob[i] += dpNoRob[j];
                    dpNoRob[i] += max(dpRob[j], dpNoRob[j]);
                }
            }
        }
        return max(dpRob[0], dpNoRob[0]);
    }
};
```

base : leaf

