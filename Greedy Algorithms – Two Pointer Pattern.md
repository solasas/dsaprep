# 🧠 Greedy Algorithms – Two Pointer Pattern

This repository contains solutions and explanations for classic **Greedy + Two Pointer** problems commonly asked in coding interviews.

---

## 📌 Problems Covered

* 🍪 Assign Cookies (LeetCode 455)
* 🏋️ Match Players and Trainers (LeetCode 2410)

---

# 🍪 1. Assign Cookies

## 📝 Problem Statement

You are given two arrays:

* `g[i]` → greed factor of each child
* `s[j]` → size of each cookie

Each child can receive **at most one cookie**.

👉 A child is satisfied if:

```
s[j] >= g[i]
```

👉 Return the **maximum number of satisfied children**.

---

## 💡 Approach

* Sort both arrays
* Start with the smallest greed and smallest cookie
* If cookie satisfies the child → move both pointers
* Otherwise → try a bigger cookie

---

## ✅ Java Solution

```java
import java.util.Arrays;

class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);

        int child = 0;
        int cookie = 0;

        while (child < g.length && cookie < s.length) {
            if (s[cookie] >= g[child]) {
                child++;
            }
            cookie++;
        }

        return child;
    }
}
```

---

## ⏱️ Complexity

* Time: **O(n log n + m log m)**
* Space: **O(1)**

---

## 🧠 Key Insight

> Always satisfy the **least greedy child first** to maximize total satisfied children.

---

# 🏋️ 2. Match Players and Trainers

## 📝 Problem Statement

You are given:

* `players[i]` → ability of players
* `trainers[j]` → capacity of trainers

👉 A match is possible if:

```
players[i] <= trainers[j]
```

👉 Return the **maximum number of matches**.

---

## 💡 Approach

* Sort both arrays
* Start from the largest values
* Match strongest player with strongest trainer
* If not possible → try a smaller player

---

## ✅ Java Solution

```java
import java.util.Arrays;

class Solution {
    public int matchPlayersAndTrainers(int[] players, int[] trainers) {
        Arrays.sort(players);
        Arrays.sort(trainers);

        int player = players.length - 1;
        int trainer = trainers.length - 1;
        int matches = 0;

        while (player >= 0 && trainer >= 0) {
            if (players[player] <= trainers[trainer]) {
                matches++;
                player--;
                trainer--;
            } else {
                player--;
            }
        }

        return matches;
    }
}
```

---

## ⏱️ Complexity

* Time: **O(n log n + m log m)**
* Space: **O(1)**

---

## 🧠 Key Insight

> Match **strongest players with strongest trainers** to avoid wasting resources.

---

# 🔥 Pattern Summary

These problems follow:

```
Greedy + Sorting + Two Pointers
```

---

## 📊 Comparison

| Feature          | Assign Cookies    | Match Players                 |
| ---------------- | ----------------- | ----------------------------- |
| Strategy         | Small → Small     | Large → Large                 |
| Pointer Movement | Forward           | Backward                      |
| Count Method     | Pointer (`child`) | Separate variable (`matches`) |

---

# 🚀 When to Use This Pattern

Use this approach when:

* You need to **maximize assignments or matches**
* There is a condition like `a[i] <= b[j]`
* Each element can be used **at most once**

---

# 🎯 Final Takeaways

* Sorting helps make optimal greedy decisions
* Two pointers reduce time complexity to **O(n log n)**
* Always think:

  > “Am I using the smallest/largest resource efficiently?”

---

## ⭐ If this helped you, consider giving a star!
