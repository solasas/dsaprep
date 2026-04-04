# Lowest Common Ancestor (LCA) in Binary Tree

## Problem

Given a binary tree and two nodes `p` and `q`, find their lowest common ancestor (LCA).

The LCA is the lowest node that has both `p` and `q` as descendants.

---

## Key Idea

Search for `p` and `q` in both left and right subtrees.

* If both sides return a non-null value, the current node is the LCA.
* Otherwise, return the non-null value.

---

## Approach

1. If `root` is null, return null
2. If `root` is equal to `p` or `q`, return `root`
3. Recursively search left and right
4. If both results are non-null, return `root`
5. Else return the non-null result

---

## Code (Java)

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) return null;

        if (root == p || root == q) {
            return root;
        }

        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);

        if (left != null && right != null) {
            return root;
        }

        return left == null ? right : left;
    }
}
```

---

## How It Works

* The recursion searches for `p` and `q` in subtrees.
* When both are found in different branches of a node, that node is the LCA.
* The result is passed upward.

---

## Example

```
        3
       / \
      5   1
```

* LCA(5, 1) = 3

---

## Complexity

* Time: O(N)
* Space: O(H)

---

## Summary

If both left and right calls return non-null, the current node is the LCA. Otherwise, return the non-null result.
