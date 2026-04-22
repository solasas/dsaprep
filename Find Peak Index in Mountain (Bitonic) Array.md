# 🔍 Find Peak Index in Mountain (Bitonic) Array

## 📌 Problem Summary

A **mountain (bitonic) array** is an array where:
- Elements first **strictly increase**
- Then **strictly decrease**

👉 Goal: Find the **peak element (maximum value)**

---

## 🔍 Example

```
Input:  arr = [1, 3, 5, 7, 6, 4, 2]
Output: 3   // index of peak (value = 7)
```

---

## 🧠 Key Idea

Instead of checking all elements (O(n)),  
we use **Binary Search (O(log n))**.

👉 We don’t search for a value  
👉 We search for the **change in slope (↑ → ↓)**

---

## 🚀 Approach (Binary Search on Slope)

At any index `mid`, compare:

```
arr[mid] vs arr[mid + 1]
```

---

### 🔹 Case 1: Ascending Part

```
arr[mid] < arr[mid + 1]
```

👉 You are in the **increasing region**  
👉 Peak lies on the **right side**

```
left = mid + 1
```

---

### 🔹 Case 2: Descending Part

```
arr[mid] > arr[mid + 1]
```

👉 You are in the **decreasing region OR at peak**  
👉 Peak lies on the **left side (including mid)**

```
right = mid
```

---

## ⚡ Convergence

We continue until:

```
left == right
```

👉 This index is the **peak element**

---

## ✅ Code (Java)

```java
class Solution {
    public int peakIndexInMountainArray(int[] arr) {
        int left = 0;
        int right = arr.length - 1;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (arr[mid] < arr[mid + 1]) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }

        return left; // peak index
    }
}
```

---

## 🔥 Dry Run

```
arr = [1,3,5,7,6,4,2]

left=0, right=6
mid=3 → arr[3]=7 > arr[4]=6 → right=3

left=0, right=3
mid=1 → 3 < 5 → left=2

left=2, right=3
mid=2 → 5 < 7 → left=3

left=3, right=3 → peak found
```

---

## ⏱️ Complexity

- Time: `O(log n)`
- Space: `O(1)`

---

## 🧩 Pattern Recognition

This is **Binary Search on Direction / Slope**

Used in:
- Peak Element
- Mountain Array
- Bitonic Search
- Maximum in unimodal arrays

---

## 💡 Key Takeaways

- Compare `arr[mid]` with `arr[mid + 1]`
- Move based on slope direction
- Use `while (left < right)` (not `<=`)
- Final answer is `left` (or `right`)

---

## 🧠 Mental Model

```
If going UP  → move right
If going DOWN → move left
```

---

## 🚀 Takeaway

This is not standard binary search —  
it’s **finding a turning point (maximum)** in a structured array.

---
