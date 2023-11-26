https://leetcode.com/problems/binary-tree-maximum-path-sum/
<br>
https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/
<br>
https://leetcode.com/problems/minimum-time-to-collect-all-apples-in-a-tree/


```int solve(TreeNode* root,int &res)
    {
        // Base Case 
        if(root==NULL) return NULL;
        int ls = solve(root->left,res);
        int rs = solve(root->right,res);
        int temp = max(max(ls,rs)+root->val,root->val);
        int ans = max(temp,ls+rs+root->val);
        res = max(res,ans);
        return temp;
    }
    int maxPathSum(TreeNode* root) {
        int res = INT_MIN;
        solve(root,res);
        return res;
    }
```

Vertical Order Traversal of BT
```
    class Solution {
public:
    vector<vector<int>> verticalTraversal(TreeNode* root) {
        map<int, map<int, set<int>>> nodes;
        traverse(root, 0, 0, nodes);
        vector<vector<int>> ans;
        for (auto p : nodes) {
            vector<int> col;
            for (auto q : p.second) {
                col.insert(col.end(), q.second.begin(), q.second.end());
            }
            ans.push_back(col);
        }
        return ans;
    }
private:
    void traverse(TreeNode* root, int x, int y, map<int, map<int, set<int>>>& nodes) {
        if (root) {
            nodes[x][y].insert(root -> val);
            traverse(root -> left, x - 1, y + 1, nodes);
            traverse(root -> right, x + 1, y + 1, nodes);
        }
    }
};
```

stack/queue: push / pop
set: insert/remove/find
