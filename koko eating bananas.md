# 🍌 Koko Eating Bananas

## 📌 Intuition

We need to find the **minimum eating speed** `k` such that Koko can finish all bananas within `h` hours.

Instead of checking every speed from `1` to `max(piles)`, we use **Binary Search on Answers**.

---

## 🧠 Observation

If Koko can finish all bananas with speed:

```text
k = 8
```

then she can also finish with:

```text
k = 9, 10, 11...
```

This creates a monotonic property:

```text
Speed:
1 2 3 4 5 6 7 8 9 ...

Can Finish:
F F F F F F F T T ...
```

We need the **first valid speed**.

---

## 🚀 Search Space

### Minimum Possible Speed

```text
1
```

### Maximum Possible Speed

```text
max(piles)
```

Example:

```text
piles = [3,6,7,11]

max speed = 11
```

---

## 🧩 Helper Function

For a given speed `k`, calculate the total hours needed.

For each pile:

```text
hours = ceil(pile / k)
```

Total:

```text
totalHours = Σ ceil(pile / k)
```

---

## ⚠️ Important

In Java:

```java
Math.ceil((double)pile / k)
```

must use floating point division.

OR use the optimized formula:

```java
(pile + k - 1) / k
```

which directly computes the ceiling.

---

## 🔍 Binary Search Logic

### If:

```text
totalHours <= h
```

Speed is valid.

Try to find a smaller speed.

```java
high = mid - 1
```

---

### If:

```text
totalHours > h
```

Speed is too slow.

Increase speed.

```java
low = mid + 1
```

---

## ✅ Code (Striver Style)

```java
class Solution {

    public int kokoEat(int[] arr, int k) {

        int left = 1;
        int right = findMax(arr);

        while (left <= right) {

            int mid = left + (right - left) / 2;

            long totalHours = calculateTotalHours(arr, mid);

            if (totalHours <= k) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }

    public int findMax(int[] arr) {
        int max = Integer.MIN_VALUE;

        for (int num : arr) {
            max = Math.max(max, num);
        }

        return max;
    }

    public long calculateTotalHours(int[] arr, int hourly) {

        long totalHours = 0;

        for (int num : arr) {
            totalHours += (long) Math.ceil((double) num / hourly);
        }

        return totalHours;
    }
}
```

---

## 🔥 Dry Run

```text
piles = [3,6,7,11]
h = 8
```

Search Space:

```text
low = 1
high = 11
```

### mid = 6

```text
3  -> 1
6  -> 1
7  -> 2
11 -> 2

Total = 6
```

Valid.

```text
high = 5
```

---

### mid = 3

```text
3  -> 1
6  -> 2
7  -> 3
11 -> 4

Total = 10
```

Too many hours.

```text
low = 4
```

---

### mid = 4

```text
3  -> 1
6  -> 2
7  -> 2
11 -> 3

Total = 8
```

Valid.

```text
high = 3
```

Loop ends.

Answer:

```text
4
```

---

## ⏱️ Complexity

### Binary Search

```text
O(log(maxPile))
```

### Helper Function

```text
O(n)
```

### Total

```text
O(n * log(maxPile))
```

### Space

```text
O(1)
```

---

## 🎯 Pattern Recognition

This problem belongs to:

- Koko Eating Bananas
- Minimum Days to Make M Bouquets
- Capacity to Ship Packages Within D Days
- Split Array Largest Sum
- Allocate Minimum Pages
- Painter's Partition Problem

All are solved using:

```text
Binary Search on Answers
```
