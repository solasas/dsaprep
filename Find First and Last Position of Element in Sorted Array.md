# 🔍 Find First and Last Position of Element in Sorted Array

## 📌 Problem Summary

Given a **sorted array `nums`** and a `target`,  
find the **starting and ending position** of the target.

If the target is not found, return `[-1, -1]`.

---

## 🔍 Example

```
Input:  nums = [5,7,7,8,8,10], target = 8
Output: [3,4]

Input:  nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

---

## 🧠 Key Idea

We use **binary search twice**:

- First → find **first occurrence**
- Second → find **last occurrence**

👉 Normal binary search is not enough because it stops at any occurrence.

---

# 🚀 Approach

### Step 1: Find First Occurrence
- When `nums[mid] == target`  
  → store index  
  → move left → `right = mid - 1`

---

### Step 2: Find Last Occurrence
- When `nums[mid] == target`  
  → store index  
  → move right → `left = mid + 1`

---

## ✅ Code (Java)

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] ans = {-1, -1};

        ans[0] = search(nums, target, true);

        if (ans[0] != -1) {
            ans[1] = search(nums, target, false);
        }

        return ans;
    }

    private int search(int[] nums, int target, boolean findStartIndex) {
        int ans = -1;
        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (target < nums[mid]) {
                right = mid - 1;
            } 
            else if (target > nums[mid]) {
                left = mid + 1;
            } 
            else {
                ans = mid;

                if (findStartIndex) {
                    right = mid - 1;  // move left
                } else {
                    left = mid + 1;   // move right
                }
            }
        }

        return ans;
    }
}
```

---

## 🔥 Dry Run

```
nums = [5,7,7,8,8,10], target = 8
```

### First Occurrence:
```
mid=2 → 7 < 8 → right
mid=4 → 8 → ans=4 → move left
mid=3 → 8 → ans=3 → move left
→ result = 3
```

### Last Occurrence:
```
mid=2 → 7 < 8 → right
mid=4 → 8 → ans=4 → move right
mid=5 → 10 > 8 → left
→ result = 4
```

---

## ⚡ Complexity

- Time: `O(log n)`
- Space: `O(1)`

---

## 🧩 Alternative Approach (Using Bounds)

```java
int first = lowerBound(nums, target);
int last = upperBound(nums, target) - 1;
```

---

## 💡 Key Takeaways

- Use binary search to find **boundaries**
- Don’t stop when target is found
- Keep searching:
  - Left → for first occurrence
  - Right → for last occurrence

---

## 🚀 Pattern Recognition

This pattern is used in:

- First/Last occurrence
- Count frequency of element
- Lower Bound / Upper Bound problems

---
