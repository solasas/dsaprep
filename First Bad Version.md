# 🔍 First Bad Version / First Occurrence (Binary Search)

## 📌 Problem Summary

Given a monotonic array or condition, find the **first index where the value becomes true**.

Example:
```
[0, 0, 0, 1, 1, 1, 1]
         ↑
   First occurrence of 1
```

- `0` → Good (False)  
- `1` → Bad (True)

---

## 🧠 Intuition

The array follows a monotonic pattern:

```
false false false true true true
```

Once it becomes `true`, it never turns `false` again.

---

## ⚡ Approach (Binary Search)

- If `mid` is `true` → search left → `right = mid`
- If `mid` is `false` → search right → `left = mid + 1`

---

## ✅ Code (Java)

### First Occurrence of 1

```java
class Solution {
    public int firstOne(int[] nums) {
        int left = 0;
        int right = nums.length - 1;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] == 1) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }
}
```

---

### First Bad Version

```java
/* The isBadVersion API is defined in the parent class VersionControl.
   boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 1;
        int right = n;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (isBadVersion(mid)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }
}
```

---

## ⏱️ Complexity

- Time: `O(log n)`
- Space: `O(1)`

---

## 💡 Template

```java
while (left < right) {
    int mid = left + (right - left) / 2;

    if (condition(mid)) {
        right = mid;
    } else {
        left = mid + 1;
    }
}
return left;
```

---

## 🧠 Key Takeaway

This is a **boundary-finding binary search** used to find:
- First true
- First bad version
- Lower bound
- Minimum index satisfying condition
