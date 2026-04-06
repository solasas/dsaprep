# Serialize and Deserialize Binary Tree

## Problem
Design an algorithm to serialize and deserialize a binary tree.

- **Serialize**: Convert a binary tree into a string  
- **Deserialize**: Convert the string back into the original binary tree  

---

## Theory

To reconstruct a binary tree uniquely, we must store:
- Node values  
- Tree structure  

If we only store values, we lose structure.  
So we use `"null"` to represent missing nodes.

---

## Key Idea

- Use **preorder traversal (Root → Left → Right)**  
- Store `"null"` for empty nodes  
- Rebuild the tree using the same order  

---

## Approach

### Serialize

1. Traverse tree using preorder  
2. Add:
   - node value if not null  
   - `"null"` if node is null  
3. Store as comma-separated string  

---

### Deserialize

1. Split string into values  
2. Use a queue to process values  
3. For each value:
   - If `"null"` → return null  
   - Else:
     - create node  
     - build left subtree  
     - build right subtree  

---

## Code (Java)

```java
class Codec {

    // Serialize
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        buildString(root, sb);
        return sb.toString();
    }

    private void buildString(TreeNode root, StringBuilder sb) {
        if (root == null) {
            sb.append("null,");
            return;
        }

        sb.append(root.val).append(",");
        buildString(root.left, sb);
        buildString(root.right, sb);
    }

    // Deserialize
    public TreeNode deserialize(String data) {
        String[] arr = data.split(",");
        Queue<String> queue = new LinkedList<>(Arrays.asList(arr));
        return buildTree(queue);
    }

    private TreeNode buildTree(Queue<String> queue) {
        String val = queue.poll();

        if (val.equals("null")) {
            return null;
        }

        TreeNode node = new TreeNode(Integer.parseInt(val));
        node.left = buildTree(queue);
        node.right = buildTree(queue);

        return node;
    }
}
