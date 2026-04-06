# Sum Root to Leaf Numbers

## Problem
Given the root of a binary tree where each node contains a digit (0–9),  
each root-to-leaf path represents a number.

Return the **total sum of all root-to-leaf numbers**.

---

## Theory

- A **root-to-leaf path** forms a number by concatenating digits  

For example:

```
    1
   / \
  2   3
```

Paths:
- 1 → 2 = 12  
- 1 → 3 = 13  

Total sum = `12 + 13 = 25`

---

## Key Idea

- Use **DFS (recursion)**  
- At each node:
  ```
  current = current * 10 + node.val
  ```
- When a **leaf node** is reached:
  - Add the number to the result  

---

## Approach

1. Start DFS with `current = 0`  
2. At each node:
   - Update current number  
3. If leaf node:
   - Return current number  
4. Otherwise:
   - Return sum of left and right subtree  

---

## Code (Java)

```java
class Solution {
    public int sumNumbers(TreeNode root) {
        return dfs(root, 0);
    }

    public int dfs(TreeNode root, int current) {
        if (root == null) return 0;

        current = current * 10 + root.val;

        // leaf node
        if (root.left == null && root.right == null) {
            return current;
        }

        return dfs(root.left, current) + dfs(root.right, current);
    }
}
```

---

## Example

```
    1
   / \
  2   3
```

Paths:
```
1 → 2 = 12  
1 → 3 = 13  
```

Output:
```
12 + 13 = 25
```

---

## How It Works

### Step-by-step

- Start at root:
  ```
  current = 0 → 1
  ```

- Left path:
  ```
  1 → 2
  current = 1*10 + 2 = 12
  ```
  Leaf → return 12  

- Right path:
  ```
  1 → 3
  current = 1*10 + 3 = 13
  ```
  Leaf → return 13  

- Final sum:
  ```
  12 + 13 = 25
  ```

---

## Complexity

- **Time Complexity:** O(N)  
- **Space Complexity:** O(H) (recursion stack)  

---

## Important Points

- Only consider **root-to-leaf paths**  
- Build numbers using multiplication (`*10`)  
- Use DFS to traverse all paths  

---

## Summary

- Traverse tree using DFS  
- Build numbers along the path  
- Add values when reaching leaf nodes  
- Return total sum of all paths  
