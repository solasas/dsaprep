# 🔍 Lower Bound & Upper Bound (Binary Search)

## 📌 Problem Summary

Given a **sorted array**, find:

- **Lower Bound(x)** → first index where element **≥ x**
- **Upper Bound(x)** → first index where element **> x**

---

## 🔍 Example

```
arr = [2, 4, 4, 4, 6, 8]
target = 4

lower bound index = 1  (value = 4)
upper bound index = 4  (value = 6)
```

---

## 🧠 Key Idea

Both problems are **boundary-finding binary search**:

- Shrink the search space
- Return the **first index where condition becomes true**
- No extra variable (`ans`) needed

---

# 🚀 Lower Bound (First ≥ x)

## 💡 Approach

- If `arr[mid] ≥ x` → move left → `right = mid - 1`
- Else → move right → `left = mid + 1`
- Final answer = `left`

---

## ✅ Code (Java)

```java
class Solution {
    int lowerBound(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (arr[mid] >= target) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }
}
```

---

## 🔥 Dry Run (Lower Bound)

```
arr = [2,4,4,4,6,8], target=4

mid=2 → 4 ≥ 4 → right=1
mid=0 → 2 < 4 → left=1
mid=1 → 4 ≥ 4 → right=0

left=1 → answer
```

---

# 🚀 Upper Bound (First > x)

## 💡 Approach

- If `arr[mid] > x` → move left → `right = mid - 1`
- Else → move right → `left = mid + 1`
- Final answer = `left`

---

## ✅ Code (Java)

```java
class Solution {
    int upperBound(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (arr[mid] > target) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }
}
```

---

## 🔥 Dry Run (Upper Bound)

```
arr = [2,4,4,4,6,8], target=4

mid=2 → 4 ≤ 4 → left=3
mid=4 → 6 > 4 → right=3
mid=3 → 4 ≤ 4 → left=4

left=4 → answer
```

---

# ⚡ Key Differences

| Type        | Condition        | Meaning                  | Return |
|-------------|----------------|--------------------------|--------|
| Lower Bound | `>= target`     | first element ≥ target   | left   |
| Upper Bound | `> target`      | first element > target   | left   |

---

# 🚨 Edge Cases

| Case                        | Result              |
|----------------------------|---------------------|
| All elements < target      | returns `n`         |
| All elements ≥ target      | returns `0`         |

---

# 🧠 Pattern Recognition

Used in:

- First/Last occurrence
- Count frequency
- Ceil / Floor problems
- Binary Search on Answer

---

# 🔥 Bonus: Count Frequency

```java
int count = upperBound(arr, x) - lowerBound(arr, x);
```

---

# 🚀 Takeaway

- Same binary search template
- Only condition changes
- Always return `left`

---
