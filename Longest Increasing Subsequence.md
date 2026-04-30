# 📈 Longest Increasing Subsequence (LIS)

## 📌 Problem Statement

Given an integer array `nums`, return the **length of the longest strictly increasing subsequence**.

A subsequence is a sequence derived from the array by deleting some or no elements **without changing the order**.

---

## 🧠 Example

```
Input:  [10, 9, 2, 5, 3, 7, 101, 18]
Output: 4

Explanation:
The LIS is [2, 3, 7, 101]
```

---

# 🚀 Approaches

---

## ✅ 1. Dynamic Programming (O(n²))

### 🔑 Idea

For each index `i`, find the longest increasing subsequence **starting from that index**.

### 📌 Definition

```
dp[i] = length of LIS starting at index i
```

---

### 🔁 Transition

```
dp[i] = 1 + max(dp[j]) for all j > i where nums[j] > nums[i]
```

---

### 💻 Code (Right-to-Left DP)

```java
public int lis(int[] arr) {
    int n = arr.length;
    int[] dp = new int[n];

    for (int i = n - 1; i >= 0; i--) {
        dp[i] = 1;

        for (int j = i + 1; j < n; j++) {
            if (arr[j] > arr[i]) {
                dp[i] = Math.max(dp[i], 1 + dp[j]);
            }
        }
    }

    int max = 0;
    for (int val : dp) {
        max = Math.max(max, val);
    }

    return max;
}
```

---

### 🔍 Example

```
arr = [1, 2, 4, 3]

dp = [3, 2, 1, 1]
Answer = 3
```

---

### ⏱ Complexity

| Metric | Value |
| ------ | ----- |
| Time   | O(n²) |
| Space  | O(n)  |

---

## 🚀 2. Binary Search (Optimal O(n log n))

### 🔑 Idea

Maintain a list `tails` where:

```
tails[i] = smallest ending element of an increasing subsequence of length i+1
```

---

### 💻 Code

```java
public int lengthOfLIS(int[] nums) {
    ArrayList<Integer> tails = new ArrayList<>();

    for (int num : nums) {
        int left = 0, right = tails.size();

        while (left < right) {
            int mid = (left + right) / 2;
            if (tails.get(mid) < num) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }

        if (left == tails.size()) {
            tails.add(num);
        } else {
            tails.set(left, num);
        }
    }

    return tails.size();
}
```

---

### 🔍 Example

```
Input: [2, 5, 3, 7]

Steps:
[2]
[2,5]
[2,3]
[2,3,7]
```

---

### ⏱ Complexity

| Metric | Value      |
| ------ | ---------- |
| Time   | O(n log n) |
| Space  | O(n)       |

---

## ⚠️ Important Notes

* LIS is **strictly increasing** (`>` not `>=`)
* Binary search method gives **only length**, not sequence
* DP method is easier to understand and extend

---

## 🧠 Interview Tips

👉 If asked:

**“Explain LIS approach”**

Say:

> For each element, I try to extend all valid increasing subsequences from future elements and take the maximum length. This gives an O(n²) DP solution.

👉 If asked for optimization:

> We can reduce it to O(n log n) using binary search by maintaining optimal subsequence endings.

---

## 🔥 Variations to Practice

* Print actual LIS
* Longest Bitonic Subsequence
* Maximum Sum Increasing Subsequence
* LIS using recursion + memoization

---

## 🚀 Final Takeaway

> LIS is about finding the longest chain where each next element is greater — solved efficiently using DP or binary search.

---
