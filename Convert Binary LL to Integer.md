# 🔢 Convert Binary Linked List to Integer (Using Powers of 2)

This project demonstrates how to convert a **binary number stored in a singly linked list** into its **decimal (base-10) equivalent** using the **powers of 2 approach**.

---

## 📌 Problem Statement

Given the `head` of a singly linked list where each node contains either `0` or `1`,
the linked list represents a **binary number**.

👉 Return its **decimal equivalent**.

---

## 🔍 Example

### Input:

```text
1 → 0 → 1
```

### Explanation:

```text
1×2² + 0×2¹ + 1×2⁰ = 4 + 0 + 1 = 5
```

### Output:

```text
5
```

---

## 🧠 Approach (Powers of 2)

We follow two main steps:

### 1️⃣ Find Length of Linked List

* This tells us the highest power of 2
* If length = `n`, then first node uses `2^(n-1)`

---

### 2️⃣ Traverse Again and Compute Value

For each node:

```text
value = node.val × 2^(position)
```

* Start from highest power
* Decrease power as we move forward

---

## ⚙️ Algorithm Steps

1. Traverse the list to calculate length `n`
2. Initialize result = 0
3. Traverse again:

   * Add `node.val × 2^(n-1)` to result
   * Decrement `n`
4. Return result

---

## ✅ Java Implementation

```java
class Solution {
    public int getDecimalValue(ListNode head) {
        ListNode curr = head;
        int length = 0;

        // Step 1: Find length
        while (curr != null) {
            length++;
            curr = curr.next;
        }

        curr = head;
        int num = 0;

        // Step 2: Calculate decimal value
        while (curr != null) {
            num += curr.val * Math.pow(2, length - 1);
            length--;
            curr = curr.next;
        }

        return num;
    }
}
```

---

## 📊 Dry Run

Input:

```text
1 → 0 → 1
```

Length = 3

| Node | Power | Calculation | Result |
| ---- | ----- | ----------- | ------ |
| 1    | 2     | 1×4 = 4     | 4      |
| 0    | 1     | 0×2 = 0     | 4      |
| 1    | 0     | 1×1 = 1     | 5      |

✅ Final Output = **5**

---

## ⏱ Complexity Analysis

| Metric           | Value |
| ---------------- | ----- |
| Time Complexity  | O(n)  |
| Space Complexity | O(1)  |

---

## ⚠️ Important Notes

* `Math.pow()` returns a `double`, but Java handles conversion here
* Works efficiently for typical input sizes
* Requires **two traversals** of the list

---

## ⚡ Alternative (Optimized Approach)

Instead of powers, you can use:

```java
num = num * 2 + current.val;
```

✔️ Single traversal
✔️ No need for length
✔️ More efficient

---

## 🎯 Key Insight

> “Each node contributes its value multiplied by a power of 2 based on its position.”

---

## 🚀 Related Problems

* Binary to Decimal Conversion
* Convert Integer to Binary
* Bit Manipulation Basics
* Linked List Traversal Problems

---

## 👨‍💻 Author

Prepared as part of **DSA practice for coding interviews**.

---

⭐ If this helped you, consider starring your repository!
