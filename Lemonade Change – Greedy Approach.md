#  Lemonade Change – Greedy Approach

This repository contains a solution and explanation for the classic greedy problem:

* Lemonade Change (LeetCode 860)

---

## 📌 Problem Statement

You are selling lemonade at **$5 per cup**.

Customers pay using:

* `$5`
* `$10`
* `$20`

👉 You must provide **correct change** for each transaction.

👉 Return `true` if you can give change to every customer, otherwise `false`.

---

## 💡 Approach (Greedy)

We simulate each transaction while maintaining:

* `d5` → number of $5 bills
* `d10` → number of $10 bills

---

## 🧠 Key Rules

### 1. If customer pays `$5`

* No change needed
* Just increment `$5` count

---

### 2. If customer pays `$10`

* Must give `$5` as change
* If not available → return `false`

---

### 3. If customer pays `$20`

Prefer giving:

1. `$10 + $5` ✅ (best option)
2. Else `3 × $5`

If neither possible → return `false`

---

## ✅ Java Solution

```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int d5 = 0;
        int d10 = 0;

        for (int bill : bills) {
            if (bill == 5) {
                d5++;
            } 
            else if (bill == 10) {
                if (d5 == 0) return false;
                d5--;
                d10++;
            } 
            else { // bill == 20
                if (d10 > 0 && d5 > 0) {
                    d10--;
                    d5--;
                } 
                else if (d5 >= 3) {
                    d5 -= 3;
                } 
                else {
                    return false;
                }
            }
        }

        return true;
    }
}
```

---

## ⏱️ Complexity

* Time: **O(n)**
* Space: **O(1)**

---

## 🔥 Greedy Insight

> Always try to use **larger denominations first** when giving change.

Why?

* Preserves smaller bills for future transactions
* Ensures flexibility

---

## 🚀 Key Takeaways

* Do **not track total money** — track denominations
* Always **fail fast** when change cannot be given
* Greedy decisions must be **locally optimal**

---

## ⚠️ Common Mistakes

| Mistake                     | Why it's wrong           |
| --------------------------- | ------------------------ |
| Using total sum             | Cannot form exact change |
| Not prioritizing `$10 + $5` | Wastes smaller bills     |
| Using a boolean flag        | Misses early failures    |

---

## 🎯 Pattern

```text
Greedy + Simulation
```

---

## ⭐ If this helped you, consider giving a star!
