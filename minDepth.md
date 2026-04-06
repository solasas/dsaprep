# Minimum Depth of Binary Tree (BFS Approach)

## Problem
Given a binary tree, find its **minimum depth**.

- Minimum depth is the number of nodes along the shortest path from the root node to the nearest leaf node.

---

## Key Idea

- Use **Breadth First Search (BFS)** (level order traversal)
- Traverse the tree level by level
- The **first leaf node encountered gives the minimum depth**

---

## Why BFS?

- BFS explores nodes level by level  
- The first time we reach a leaf node, it is guaranteed to be the shortest path  
- No need to explore the entire tree  

---

## Approach

1. If root is null → return 0  
2. Add root to queue  
3. Initialize depth = 1  
4. Traverse level by level:
   - For each node:
     - If it is a leaf → return depth  
     - Otherwise, add its children to queue  
5. Increment depth after each level  

---

## Code (Java)

```java
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) return 0;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        int depth = 1;

        while (!queue.isEmpty()) {
            int size = queue.size();

            for (int i = 0; i < size; i++) {
                TreeNode curr = queue.poll();

                // check if leaf node
                if (curr.left == null && curr.right == null) {
                    return depth;
                }

                if (curr.left != null) queue.offer(curr.left);
                if (curr.right != null) queue.offer(curr.right);
            }

            depth++;
        }

        return depth;
    }
}
