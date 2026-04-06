# Construct Binary Tree from Preorder and Inorder

## Problem
Given two arrays:
- `preorder` (Root → Left → Right)
- `inorder` (Left → Root → Right)

Construct the binary tree.

---

## Theory

A binary tree can be uniquely constructed using preorder and inorder traversals.

- **Preorder** always gives the root first.
- **Inorder** helps identify the left and right subtrees.

### Key Observations

- First element of preorder = root  
- In inorder:
  - Elements left of root → left subtree  
  - Elements right of root → right subtree  

This allows us to recursively reconstruct the tree.

---

## Approach (Using Array Slicing)

1. If preorder is empty → return null  
2. Take first element of preorder as root  
3. Find root index in inorder  
4. Split arrays:
   - Left subtree:
     - preorder → next `index` elements  
     - inorder → left part  
   - Right subtree:
     - remaining elements  
5. Recursively build left and right subtrees  

---

## Code (Java)

```java
class Solution {

    public TreeNode buildTree(int[] preorder, int[] inorder) {

        if (preorder.length == 0) {
            return null;
        }

        int rootVal = preorder[0];

        int index = 0;
        for (int i = 0; i < inorder.length; i++) {
            if (inorder[i] == rootVal) {
                index = i;
                break;
            }
        }

        TreeNode root = new TreeNode(rootVal);

        root.left = buildTree(
            Arrays.copyOfRange(preorder, 1, index + 1),
            Arrays.copyOfRange(inorder, 0, index)
        );

        root.right = buildTree(
            Arrays.copyOfRange(preorder, index + 1, preorder.length),
            Arrays.copyOfRange(inorder, index + 1, inorder.length)
        );

        return root;
    }
}

## Complexity Analysis
Time Complexity: O(N²)
Finding root in inorder → O(N)
Done for each node → O(N²)
Space Complexity: O(N)
Recursive stack
Additional arrays created using copyOfRange
