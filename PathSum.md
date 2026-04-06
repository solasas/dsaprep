# Path Sum (Root to Leaf)

## Problem
Given the root of a binary tree and an integer `targetSum`, determine if the tree has a **root-to-leaf path** such that:


---

## Theory

- A **root-to-leaf path** starts at the root and ends at a leaf node  
- A **leaf node** is a node with no children  

We need to check if **any one path** satisfies the given sum.

---

## Key Idea

- Traverse the tree using **DFS (recursion)**  
- At each node:
  - Subtract its value from `targetSum`
  - Pass remaining sum to children  
- If we reach a leaf and remaining sum is 0 → valid path exists  

---

## Approach

1. If node is null → return false  
2. If node is a leaf:
   - Check if `node.val == targetSum`  
3. Otherwise:
   - Recursively check left and right subtrees  
   - Return `true` if **any one path** works  

---

## Complexity
Time Complexity: O(N)
Space Complexity: O(H) (recursion stack)
---
## Important Points
Only check sum at leaf nodes
Subtract values instead of adding → simplifies logic
Use || because we check for existence
Summary
Traverse tree using DFS
Subtract values along the path
Return true if any root-to-leaf path equals target sum
---
## Code (Java)

```java
class Solution {
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) return false;

        if (root.val == targetSum && root.left == null && root.right == null) {
            return true;
        }

        return hasPathSum(root.left, targetSum - root.val) ||
               hasPathSum(root.right, targetSum - root.val);
    }
}
'''

