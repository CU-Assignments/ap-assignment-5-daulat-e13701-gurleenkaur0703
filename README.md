[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/0Zzlu9gw)
# AP-ASSIGNMENT-5-DAULAT-E13701
## TREE
### https://leetcode.com/problems/maximum-depth-of-binary-tree/
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 * int val;
 * TreeNode *left;
 * TreeNode *right;
 * TreeNode() : val(0), left(nullptr), right(nullptr) {}
 * TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 * TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) {
            return 0;
        }
        
        int leftDepth = maxDepth(root->left);
        int rightDepth = maxDepth(root->right);
        
        return 1 + std::max(leftDepth, rightDepth);
    }
};
```
![image](https://github.com/user-attachments/assets/0598b6cd-bbd3-4c56-ba9c-698a04b5e818)

### https://leetcode.com/problems/validate-binary-search-tree/
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 * int val;
 * TreeNode *left;
 * TreeNode *right;
 * TreeNode() : val(0), left(nullptr), right(nullptr) {}
 * TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 * TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return isValidBSTHelper(root, nullptr, nullptr);
    }

private:
    bool isValidBSTHelper(TreeNode* root, TreeNode* minNode, TreeNode* maxNode) {
        if (root == nullptr) {
            return true;
        }

        if ((minNode != nullptr && root->val <= minNode->val) ||
            (maxNode != nullptr && root->val >= maxNode->val)) {
            return false;
        }

        return isValidBSTHelper(root->left, minNode, root) &&
               isValidBSTHelper(root->right, root, maxNode);
    }
};
```
![image](https://github.com/user-attachments/assets/c3908c85-3c21-4a31-9205-732150343ca8)

### https://leetcode.com/problems/symmetric-tree/
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 * int val;
 * TreeNode *left;
 * TreeNode *right;
 * TreeNode() : val(0), left(nullptr), right(nullptr) {}
 * TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 * TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if (root == nullptr) {
            return true;
        }
        return isMirror(root->left, root->right);
    }

private:
    bool isMirror(TreeNode* left, TreeNode* right) {
        if (left == nullptr && right == nullptr) {
            return true;
        }
        if (left == nullptr || right == nullptr) {
            return false;
        }
        return (left->val == right->val) && isMirror(left->left, right->right) && isMirror(left->right, right->left);
    }
};
```
![image](https://github.com/user-attachments/assets/c3e62370-6a5b-44b8-9f7f-03a3ce79f428)

### https://leetcode.com/problems/binary-tree-level-order-traversal/
```
#include <iostream>
#include <vector>
#include <queue>

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 * int val;
 * TreeNode *left;
 * TreeNode *right;
 * TreeNode() : val(0), left(nullptr), right(nullptr) {}
 * TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 * TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    std::vector<std::vector<int>> levelOrder(TreeNode* root) {
        std::vector<std::vector<int>> result;
        if (root == nullptr) {
            return result;
        }

        std::queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            int levelSize = q.size();
            std::vector<int> currentLevel;

            for (int i = 0; i < levelSize; ++i) {
                TreeNode* node = q.front();
                q.pop();

                currentLevel.push_back(node->val);

                if (node->left != nullptr) {
                    q.push(node->left);
                }
                if (node->right != nullptr) {
                    q.push(node->right);
                }
            }
            result.push_back(currentLevel);
        }
        return result;
    }
};
```
![image](https://github.com/user-attachments/assets/d7a6b7f7-7cd5-4ccc-a714-fddb1ead2dc4)

### https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 * int val;
 * TreeNode *left;
 * TreeNode *right;
 * TreeNode() : val(0), left(nullptr), right(nullptr) {}
 * TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 * TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* sortedArrayToBST(std::vector<int>& nums) {
        return sortedArrayToBSTHelper(nums, 0, nums.size() - 1);
    }

private:
    TreeNode* sortedArrayToBSTHelper(std::vector<int>& nums, int left, int right) {
        if (left > right) {
            return nullptr;
        }

        int mid = left + (right - left) / 2;
        TreeNode* root = new TreeNode(nums[mid]);

        root->left = sortedArrayToBSTHelper(nums, left, mid - 1);
        root->right = sortedArrayToBSTHelper(nums, mid + 1, right);

        return root;
    }
};
```
![image](https://github.com/user-attachments/assets/0f3795c8-5134-413c-9ad7-7c41789b8609)

### https://leetcode.com/problems/binary-tree-inorder-traversal/
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 * int val;
 * TreeNode *left;
 * TreeNode *right;
 * TreeNode() : val(0), left(nullptr), right(nullptr) {}
 * TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 * TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    std::vector<int> inorderTraversal(TreeNode* root) {
        std::vector<int> result;
        std::stack<TreeNode*> stack;
        TreeNode* current = root;

        while (current != nullptr || !stack.empty()) {
            while (current != nullptr) {
                stack.push(current);
                current = current->left;
            }

            current = stack.top();
            stack.pop();
            result.push_back(current->val);

            current = current->right;
        }

        return result;
    }
};
```
![image](https://github.com/user-attachments/assets/45ae7d10-fde8-40aa-9af8-492c55ed5628)


### https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 * int val;
 * TreeNode *left;
 * TreeNode *right;
 * TreeNode() : val(0), left(nullptr), right(nullptr) {}
 * TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 * TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* buildTree(std::vector<int>& inorder, std::vector<int>& postorder) {
        std::unordered_map<int, int> inorderMap;
        for (int i = 0; i < inorder.size(); ++i) {
            inorderMap[inorder[i]] = i;
        }
        return buildTreeHelper(inorder, 0, inorder.size() - 1, postorder, 0, postorder.size() - 1, inorderMap);
    }

private:
    TreeNode* buildTreeHelper(std::vector<int>& inorder, int inStart, int inEnd,
                                std::vector<int>& postorder, int postStart, int postEnd,
                                std::unordered_map<int, int>& inorderMap) {
        if (postStart > postEnd || inStart > inEnd) {
            return nullptr;
        }

        int rootVal = postorder[postEnd];
        TreeNode* root = new TreeNode(rootVal);

        int rootIndex = inorderMap[rootVal];
        int leftSubtreeSize = rootIndex - inStart;

        root->left = buildTreeHelper(inorder, inStart, rootIndex - 1,
                                     postorder, postStart, postStart + leftSubtreeSize - 1, inorderMap);
        root->right = buildTreeHelper(inorder, rootIndex + 1, inEnd,
                                      postorder, postStart + leftSubtreeSize, postEnd - 1, inorderMap);

        return root;
    }
};
```
![image](https://github.com/user-attachments/assets/3dd7d37d-2eab-4b8e-a500-b950c05dfd0e)

### https://leetcode.com/problems/kth-smallest-element-in-a-bst/
```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 * int val;
 * TreeNode *left;
 * TreeNode *right;
 * TreeNode() : val(0), left(nullptr), right(nullptr) {}
 * TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 * TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        std::stack<TreeNode*> stack;
        TreeNode* current = root;

        while (current != nullptr || !stack.empty()) {
            while (current != nullptr) {
                stack.push(current);
                current = current->left;
            }

            current = stack.top();
            stack.pop();
            k--;

            if (k == 0) {
                return current->val;
            }

            current = current->right;
        }

        return -1; // Should not reach here if k is valid
    }
};
```
![image](https://github.com/user-attachments/assets/7222fb5e-0729-49bc-b047-ac635e10e384)

### https://leetcode.com/problems/populating-next-right-pointers-in-each-node/
```
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        if (root == nullptr) {
            return nullptr;
        }

        std::queue<Node*> q;
        q.push(root);

        while (!q.empty()) {
            int levelSize = q.size();
            Node* prev = nullptr; // Track the previous node in the level

            for (int i = 0; i < levelSize; ++i) {
                Node* current = q.front();
                q.pop();

                if (prev != nullptr) {
                    prev->next = current;
                }

                prev = current;

                if (current->left != nullptr) {
                    q.push(current->left);
                }
                if (current->right != nullptr) {
                    q.push(current->right);
                }
            }
        }
        return root;
    }
};
```
![image](https://github.com/user-attachments/assets/e143bc36-66e7-427f-9317-0d0aecec7e75)
