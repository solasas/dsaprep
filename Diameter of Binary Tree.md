# Diameter of Binary Tree

## Problem

Given a binary tree, return the **diameter** of the tree.

* The diameter is the length of the longest path between any two nodes.
* The path may or may not pass through the root.
* The length is measured in **number of edges**.

---

## Key Idea

* At every node, the longest path passing through it is:

  **left height + right height**

* We compute height and update diameter at the same time.

---

## Approach

1. Traverse the tree using DFS (recursion)
2. For each node:

   * Compute height of left subtree
   * Compute height of right subtree
   * Update diameter using `left + right`
3. Return height to parent

---

## Code (Java)

```java
class Solution {

    int diameter = 0;

    public int diameterOfBinaryTree(TreeNode root) {
        height(root);
        return diameter;
    }

    public int height(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left = height(root.left);
        int right = height(root.right);

        int dia = left + right;
        diameter = Math.max(diameter, dia);

        return Math.max(left, right) + 1;
    }
}
```

---

## How It Works

* The recursion follows **postorder traversal** (Left → Right → Node)
* First, we go down to leaf nodes
* While coming back up:

  * Each node calculates:

    * height of its left subtree
    * height of its right subtree
  * Using these, it computes possible diameter
* The maximum value across all nodes is stored

### Important Points

* **Height** = longest path from node to leaf (in nodes)
* **Diameter** = left height + right height (in edges)
* We calculate diameter at **every node**, not just root

---

## Example

```
      1
     / \
    2   3
   / \
  4   5
```

* At node 2:

  * left = 1, right = 1 → diameter = 2
* At node 1:

  * left = 2, right = 1 → diameter = 3

Final answer = 3

---

## Complexity

**Time Complexity:** O(N)

* Each node is visited once

**Space Complexity:** O(H)

* Recursive stack (H = height of tree)

---

## Key Insight

* Diameter uses both left and right heights
* Height returns only one path (maximum)
* This avoids recomputation and keeps solution optimal

---

## Summary

* Use DFS to compute height
* At each node, calculate `left + right`
* Track maximum diameter globally
* Return height using `max(left, right) + 1`
