# 🧠 Happy Number using Cycle Detection (Floyd’s Algorithm)

This project demonstrates how to solve the **Happy Number problem** using an optimized approach based on **Floyd’s Cycle Detection Algorithm (Tortoise & Hare)**.

---

## 📌 Problem Statement

A number `n` is called a **Happy Number** if:

1. Replace the number with the **sum of the squares of its digits**
2. Repeat the process
3. If it eventually becomes `1` → ✅ Happy Number
4. If it enters a **cycle (loop)** → ❌ Not a Happy Number

---

## 🔍 Example

### Input:

```
n = 19
```

### Process:

```
19 → 82 → 68 → 100 → 1
```

### Output:

```
true (Happy Number)
```

---

## 🚨 Key Observation

* The sequence of numbers will either:

  * Reach `1` → Happy
  * Enter a loop → Not Happy

Example of a cycle:

```
4 → 16 → 37 → 58 → 89 → 145 → 42 → 20 → 4
```

---

## 💡 Approach

We treat the sequence like a **linked list**:

```
n → f(n) → f(f(n)) → ...
```

Then apply **Floyd’s Cycle Detection Algorithm**:

* `slow` moves 1 step
* `fast` moves 2 steps

---

## ⚙️ Algorithm Steps

1. Initialize:

   * `slow = n`
   * `fast = n`

2. Repeat:

   * `slow = findSquare(slow)`
   * `fast = findSquare(findSquare(fast))`

3. Stop when:

   * `slow == fast`

4. If `slow == 1` → Happy Number
   Else → Not Happy

---

## ✅ Java Implementation

```java
class Solution {
    public boolean isHappy(int n) {
        int slow = n;
        int fast = n;

        do {
            slow = findSquare(slow);
            fast = findSquare(findSquare(fast));
        } while (slow != fast);

        return slow == 1;
    }

    private int findSquare(int n) {
        int ans = 0;
        while (n > 0) {
            int rem = n % 10;
            ans += rem * rem;
            n /= 10;
        }
        return ans;
    }
}
```

---

## ⏱ Complexity Analysis

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log n) |
| Space Complexity | O(1) ✅   |

---

## ⚖️ Comparison with Other Approach

### Using HashSet:

* Store visited numbers
* Detect cycle if repeated

❌ Space Complexity: O(n)

### Using Floyd’s Algorithm (this approach):

* No extra space
* Efficient cycle detection

✅ Space Complexity: O(1)

---

## 🎯 Key Insights

* Numbers form a **sequence similar to a linked list**
* If not reaching `1`, the sequence **must form a cycle**
* Cycle detection avoids extra memory usage

---

## 🔥 Interview Tip

> “This problem can be optimized by treating the number transformation as a linked list and applying Floyd’s cycle detection to identify loops.”

---

## 🚀 Related Problems

* Linked List Cycle Detection
* Find Start of Cycle in Linked List
* Detect Loop Length

---

## 👨‍💻 Author

Implemented as part of **DSA practice for coding interviews**.

---

⭐ If you found this helpful, consider starring your repository!
