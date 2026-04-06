# Same Tree

## Problem
Given two binary trees `p` and `q`, check if they are the same.

Two trees are considered the same if:
- They have the **same structure**
- They have the **same node values**

---

## Key Idea

- Compare both trees **node by node**
- At each step:
  - Check if both nodes are null  
  - Check if one is null  
  - Check if values are equal  
- Recursively compare left and right subtrees  

---

## Approach (DFS - Recursion)

1. If both nodes are null → return true  
2. If one node is null → return false  
3. If values are different → return false  
4. Recursively check:
   - left subtree  
   - right subtree  

---
## How It Works
Recursion compares nodes simultaneously
If both nodes are null → they match
If values differ → trees are not same
Continue checking left and right subtrees
Final result is true only if all nodes match
---
## Complexity
Time Complexity: O(N)
Space Complexity: O(H) (recursion stack)
---
## Important Points
Both structure and values must match
Cannot just compare traversal values
Use && because both left and right must match
---
## Code (Java)

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;

        if (p == null || q == null) return false;

        if (p.val != q.val) return false;

        return isSameTree(p.left, q.left) &&
               isSameTree(p.right, q.right);
    }
}
