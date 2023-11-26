https://leetcode.com/problems/binary-tree-maximum-path-sum/
<br>
https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/
<br>
https://leetcode.com/problems/minimum-time-to-collect-all-apples-in-a-tree/
<br>
reverse nodes in group of k

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
Reverse node ll : O(n) space due to recursion, iterative O(1)
```
 ListNode* reverseKGroup(ListNode* head, int k) {
        dummy -> next = head;
        int len = length(head);
        for (int i = 0; i < len / k; i++) {
            for (int j = 1; j < k; j++) {
                ListNode* temp = pre -> next;
                pre -> next = head -> next;
                head -> next = head -> next -> next;
                pre -> next -> next = temp;
            }
            pre = head;
            head = head -> next;
        }
        return dummy -> next;
    }
private:
    ListNode *dummy = new ListNode(0), *pre = dummy;
    int length(ListNode* head) {
        int len = 0;
        while (head) {
            len++;
            head = head -> next;
        }
        return len;
    }

ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode* cursor = head;
        for(int i = 0; i < k; i++){
            if(cursor == nullptr) return head;
            cursor = cursor->next;
        }
        ListNode* curr = head;
        ListNode* prev = nullptr;
        ListNode* nxt = nullptr;
        for(int i = 0; i < k; i++){
            nxt = curr->next;
            curr->next = prev;
            prev = curr;
            curr = nxt;
        }
        head->next = reverseKGroup(curr, k);
        return prev;
    }
```

stack/queue: push / pop
set: insert/remove/find
