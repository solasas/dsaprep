# 🌳 Zigzag (Spiral) Traversal of Binary Tree

## 📌 Problem

Given the root of a binary tree, return the **zigzag level order traversal** of its nodes’ values.

👉 Zigzag traversal means:

* Level 1 → Left to Right
* Level 2 → Right to Left
* Level 3 → Left to Right
* and so on...

---

## 🧠 Intuition

A normal level order traversal (BFS) processes nodes level by level from left to right.

To achieve zigzag order, we need to:

* **Alternate the direction of traversal at each level**
* Efficiently access elements from both ends

👉 This is where a **Deque (Double Ended Queue)** becomes useful.

---

## ⚙️ Approach (Using Deque)

We use:

* A `Deque<Node>` to allow insertion/removal from both ends
* A boolean flag `reverse` to track direction

---

### 🔄 Traversal Logic

| Direction    | Remove from         | Add children              |
| ------------ | ------------------- | ------------------------- |
| Left → Right | Front (`pollFirst`) | Left → Right (`addLast`)  |
| Right → Left | Back (`pollLast`)   | Right → Left (`addFirst`) |

---

## 🚀 Algorithm Steps

1. Initialize:

   * Deque and add root
   * Result list
   * `reverse = false`

2. While deque is not empty:

   * Get current level size
   * Traverse nodes based on `reverse` flag
   * Add children in correct order
   * Flip `reverse`

3. Return result list

---

## 💻 Code

```java
import java.util.*;

class Solution {
    ArrayList<Integer> zigZagTraversal(Node root) {
        ArrayList<Integer> zigzag = new ArrayList<>();
        if (root == null) return zigzag;

        boolean reverse = false;
        Deque<Node> dq = new LinkedList<>();
        dq.add(root);

        while (!dq.isEmpty()) {
            int size = dq.size();

            if (!reverse) {
                for (int i = 0; i < size; i++) {
                    Node curr = dq.pollFirst();
                    zigzag.add(curr.data);

                    if (curr.left != null) dq.addLast(curr.left);
                    if (curr.right != null) dq.addLast(curr.right);
                }
            } else {
                for (int i = 0; i < size; i++) {
                    Node curr = dq.pollLast();
                    zigzag.add(curr.data);

                    if (curr.right != null) dq.addFirst(curr.right);
                    if (curr.left != null) dq.addFirst(curr.left);
                }
            }

            reverse = !reverse;
        }

        return zigzag;
    }
}
```

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(N)`
  → Each node is visited exactly once

* **Space Complexity:** `O(N)`
  → Due to deque storing nodes level-wise

---

## ⚠️ Common Mistakes

* ❌ Forgetting to add root to deque
* ❌ Wrong child insertion order in reverse case
* ❌ Mixing `pollFirst` / `pollLast` incorrectly
* ❌ Not toggling direction (`reverse`)

---

## 🧠 Key Takeaway

> Use a **Deque** to simulate zigzag traversal by controlling both:
>
> * direction of traversal
> * order of insertion

---

## 🔥 Interview Tip

If stuck, you can also:

* Use normal BFS
* Store each level in a list
* Reverse alternate levels

👉 But deque solution is **more optimal and elegant**

---

## 📚 Related Problems

* Binary Tree Level Order Traversal
* Binary Tree Right View
* Binary Tree Left View
* Vertical Order Traversal

---

## 🧠 One-Line Summary

> Alternate direction at each level using deque to efficiently access both ends.
