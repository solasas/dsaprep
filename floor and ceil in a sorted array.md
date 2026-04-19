# 🔍 Ceil and Floor using Binary Search

## 📌 Problem Summary

Given a **sorted array**, find:

- **Ceil(x)** → smallest element **≥ x**
- **Floor(x)** → largest element **≤ x**

---

## 🔍 Example

```
arr = [2, 4, 6, 8], x = 5

ceil  = 6
floor = 4
```

---

## 🧠 Key Idea

We use **binary search without extra variables (`ans`)**.

Instead of storing answers:
- Let the search space shrink
- Use final pointers (`left` / `right`) to get result

---

# 🚀 Ceil (Smallest ≥ x)

## 💡 Approach

- If `arr[mid] ≥ x` → move left → `right = mid - 1`
- Else → move right → `left = mid + 1`
- After loop, `left` will point to the ceil

---

## ✅ Code (Java)

```java
class Solution {
    public int findCeil(int[] arr, int x) {
        int left = 0, right = arr.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (arr[mid] >= x) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        // check if ceil exists
        if (left == arr.length) return -1;
        return arr[left];
    }
}
```

---

## 🔥 Dry Run (Ceil)

```
arr = [2,4,6,8], x=5

mid=1 → 4 < 5 → left=2
mid=2 → 6 ≥ 5 → right=1

loop ends → left=2 → arr[2]=6 ✅
```

---

# 🚀 Floor (Largest ≤ x)

## 💡 Approach

- If `arr[mid] ≤ x` → move right → `left = mid + 1`
- Else → move left → `right = mid - 1`
- After loop, `right` will point to the floor

---

## ✅ Code (Java)

```java
class Solution {
    public int findFloor(int[] arr, int x) {
        int left = 0, right = arr.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (arr[mid] <= x) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        // check if floor exists
        if (right < 0) return -1;
        return arr[right];
    }
}
```

---

## 🔥 Dry Run (Floor)

```
arr = [2,4,6,8], x=5

mid=1 → 4 ≤ 5 → left=2
mid=2 → 6 > 5 → right=1

loop ends → right=1 → arr[1]=4 ✅
```

---

# ⚡ Key Differences

| Operation | Condition        | Move Direction | Final Answer |
|----------|----------------|---------------|--------------|
| Ceil     | `arr[mid] ≥ x` | Left          | `left`       |
| Floor    | `arr[mid] ≤ x` | Right         | `right`      |

---

# 🧠 Memory Trick

- **Ceil → return `left`**
- **Floor → return `right`**

---

# ⏱️ Complexity

- Time: `O(log n)`
- Space: `O(1)`

---

# 🔥 Pattern Recognition

This pattern is used in:

- Lower Bound (Ceil)
- Upper Bound variations
- First occurrence problems
- Binary Search on Answer

---

# 🚀 Takeaway

This is a **boundary-finding binary search**.

👉 No need for extra variables  
👉 Just rely on **final pointer positions**

---
