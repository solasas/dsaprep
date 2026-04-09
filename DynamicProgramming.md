# 🧠 Dynamic Programming (DP) for Beginners

This repository contains beginner-friendly notes and examples to understand **Dynamic Programming (DP)** — one of the most important concepts in Data Structures & Algorithms (DSA) and coding interviews.

---

# 📌 What is Dynamic Programming?

Dynamic Programming is a technique used to:

* Break problems into **smaller overlapping subproblems**
* **Store results** to avoid recomputation
* Build efficient solutions from smaller results

---

# ❗ Why DP is Needed?

### Without DP:

* Repeated calculations
* Exponential time complexity

Example:

```
fib(5) = fib(4) + fib(3)
       = fib(3) + fib(2) + fib(3) + fib(2) ...
```

👉 Same subproblems are solved multiple times.

---

### With DP:

* Store results (memoization/tabulation)
* Avoid recomputation
* Reduce time complexity to **O(n)**

---

# 🧩 Key Properties of DP

## 1. Overlapping Subproblems

* Same problems are solved again and again

## 2. Optimal Substructure

* Optimal solution can be built from smaller optimal solutions

---

# ⚙️ Two Approaches of DP

---

## 🔁 1. Memoization (Top-Down)

### 👉 Concept:

* Use recursion
* Store computed results
* Reuse stored values

### ✅ Example:

```java
int[] dp = new int[n+1];

int fib(int n) {
    if(n <= 1) return n;

    if(dp[n] != 0) return dp[n];

    return dp[n] = fib(n-1) + fib(n-2);
}
```

### ✔ Pros:

* Easy to implement
* Natural recursive thinking

### ❌ Cons:

* Stack overhead
* Slightly slower

---

## 📊 2. Tabulation (Bottom-Up)

### 👉 Concept:

* Start from base cases
* Build solution iteratively

### ✅ Example:

```java
int fib(int n) {
    if(n <= 1) return n;

    int[] dp = new int[n+1];
    dp[0] = 0;
    dp[1] = 1;

    for(int i = 2; i <= n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }

    return dp[n];
}
```

### ✔ Pros:

* Faster (no recursion)
* No stack overflow
* Interview preferred

### ❌ Cons:

* Slightly harder to derive

---

# 🔥 Memoization vs Tabulation

| Feature  | Memoization    | Tabulation |
| -------- | -------------- | ---------- |
| Approach | Recursive      | Iterative  |
| Start    | Top-down       | Bottom-up  |
| Speed    | Slower         | Faster     |
| Stack    | Uses recursion | No stack   |
| Ease     | Easier         | Moderate   |

---

# 🧠 Base Case vs DP Initialization

### Important Concept:

👉 These are NOT the same!

---

## ✅ Base Case (Edge Handling)

```java
if(n <= 1) return n;
```

* Prevents errors (like array out-of-bounds)
* Handles smallest inputs

---

## ✅ DP Initialization

```java
dp[0] = 0;
dp[1] = 1;
```

* Used to build further values

---

### 🚨 Why both are needed?

If you remove base case:

* `n = 0` → `dp[1]` causes crash ❌
* Base case ensures safe execution ✅

---

# 🪜 Steps to Solve DP Problems

1. **Define State**

   * What does `dp[i]` represent?

2. **Find Recurrence Relation**

   ```
   dp[i] = dp[i-1] + dp[i-2]
   ```

3. **Base Cases**

   ```
   dp[0] = 1
   dp[1] = 1
   ```

4. **Compute**

   * Memoization or Tabulation

---

# 🧠 How to Identify DP Problems

Look for keywords:

* “Maximum / Minimum”
* “Number of ways”
* “Optimal solution”
* “Can we reach…?”

👉 Strong hint = DP

---

# 🚀 Example: Climbing Stairs

### Problem:

You can take 1 or 2 steps. Find total ways to reach step `n`.

### Solution:

```java
int climbStairs(int n) {
    int[] dp = new int[n+1];
    dp[0] = 1;
    dp[1] = 1;

    for(int i = 2; i <= n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }

    return dp[n];
}
```

---

# ⚡ Space Optimization

```java
int climbStairs(int n) {
    int prev2 = 1, prev1 = 1;

    for(int i = 2; i <= n; i++) {
        int curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }

    return prev1;
}
```

👉 Space: **O(1)**

---

# 🎯 Interview Strategy

Always follow this order:

1. Recursion (brute force)
2. Memoization
3. Tabulation
4. Space optimization

---

# 📚 Beginner DP Problems

### 🟢 Easy

* Fibonacci
* Climbing Stairs
* House Robber

### 🟡 Medium

* 0/1 Knapsack
* Longest Common Subsequence (LCS)
* Coin Change

### 🔴 Advanced

* DP on Trees
* DP on Graphs
* Bitmask DP

---

# 🧠 Key Takeaway

> Dynamic Programming = **Recursion + Memory**

---

# ⭐ Final Tips

* Always think in terms of **subproblems**
* Practice identifying patterns
* Convert recursive → DP step by step

---

# 🙌 Contribution

Feel free to add:

* More DP problems
* Optimizations
* Pattern-based explanations

---

Happy Coding 🚀
