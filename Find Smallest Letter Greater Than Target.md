# 🔍 Find Smallest Letter Greater Than Target

## 📌 Problem Summary

Given a **sorted array of characters `letters`** and a target character `target`,  
return the **smallest character that is strictly greater than `target`**.

👉 The array is **circular**, meaning:
- If no character is greater than `target`, return the **first character**

---

## 🔍 Example

```
Input:  letters = ['c','f','j'], target = 'a'
Output: 'c'

Input:  letters = ['c','f','j'], target = 'c'
Output: 'f'

Input:  letters = ['c','f','j'], target = 'j'
Output: 'c'  // wrap around
```

---

## 🧠 Key Idea

This is an **Upper Bound problem**:

👉 Find the **first element > target**

---

## 🚀 Approach (Binary Search)

- If `letters[mid] > target` → move left → `right = mid - 1`
- Else → move right → `left = mid + 1`
- Final answer = `left`

---

## ⚠️ Important: Circular Behavior

If no element is greater than target:
- `left` becomes `n`
- Use `% n` to wrap around

---

## ✅ Code (Java)

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int left = 0;
        int right = letters.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (letters[mid] > target) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        return letters[left % letters.length];
    }
}
```

---

## 🔥 Dry Run

```
letters = ['c','f','j'], target = 'j'

No element > 'j'
left = 3

3 % 3 = 0 → 'c' ✅
```

---

## ⚡ Complexity

- Time: `O(log n)`
- Space: `O(1)`

---

## 🧩 Pattern Mapping

| Concept        | Condition       | Return |
|---------------|----------------|--------|
| Lower Bound   | `>= target`     | left   |
| Upper Bound   | `> target`      | left   |
| This Problem  | `> target` + circular | left % n |

---

## 💡 Key Takeaway

- This is **Upper Bound + Circular Array**
- Use `%` only when **wrap-around is required**

---
