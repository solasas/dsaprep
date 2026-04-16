# 🔗 Intersection of Two Linked Lists

This project explains how to find the **intersection node of two singly linked lists** using:

* ✅ Brute Force (HashMap)
* 🔥 Optimal Approach (Two Pointers)

---

## 📌 Problem Statement

Given the heads of two singly linked lists `headA` and `headB`,
return the node at which the two lists intersect.

👉 If the two linked lists have no intersection, return `null`.

---

## 🔍 Example

```text
A: 1 → 2 → 3 \
               → 7 → 8
B:       4 → 5 /
```

### Output:

```text
7
```

---

## 🧠 Key Concept

* Intersection means **same node reference**, not same value
* After intersection, both lists share the same tail

---

# 🐢 Brute Force Approach (HashMap)

## 💡 Idea

* Store all nodes of list A in a HashMap
* Traverse list B
* If a node exists in map → intersection found

---

## ✅ Code

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {

        Map<ListNode, Integer> map = new HashMap<>();

        ListNode curr = headA;
        while (curr != null) {
            map.put(curr, 1);
            curr = curr.next;
        }

        curr = headB;
        while (curr != null) {
            if (map.containsKey(curr)) {
                return curr;
            }
            curr = curr.next;
        }

        return null;
    }
}
```

---

## ⏱ Complexity

| Metric | Value    |
| ------ | -------- |
| Time   | O(n + m) |
| Space  | O(n) ❌   |

---

## ⚠️ Drawbacks

* Uses extra memory
* Not optimal for large inputs

---

# 🔥 Optimal Approach (Two Pointers)

## 💡 Idea

* Use two pointers `a` and `b`
* Traverse both lists
* When a pointer reaches end → switch to other list
* They will meet at:

  * Intersection node ✅
  * Or `null` (no intersection)

---

## ✅ Code

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {

        ListNode a = headA;
        ListNode b = headB;

        while (a != b) {
            a = (a == null) ? headB : a.next;
            b = (b == null) ? headA : b.next;
        }

        return a;
    }
}
```

---

## 🧠 Why This Works

* Pointer A travels: A → B
* Pointer B travels: B → A

👉 Both travel equal distance → they align

---

## 📊 Visualization

```text
A: a1 → a2 → c1 → c2
B: b1 → b2 → b3 → c1 → c2
```

After switching:

* Both pointers reach `c1` at same time

---

## ⏱ Complexity

| Metric | Value    |
| ------ | -------- |
| Time   | O(n + m) |
| Space  | O(1) ✅   |

---

# ⚖️ Comparison

| Approach    | Time     | Space  | Notes                |
| ----------- | -------- | ------ | -------------------- |
| HashMap     | O(n + m) | O(n) ❌ | Easy but extra space |
| Two Pointer | O(n + m) | O(1) ✅ | Optimal              |

---

# 🎯 Interview Tips

* Start with brute force (easy to explain)
* Then optimize to two-pointer approach
* Emphasize **reference comparison**, not values

---

# 🚀 Key Takeaways

* Linked list intersection is about **node reference**
* Two-pointer approach avoids extra space
* Pointer switching ensures equal traversal length

---

# 👨‍💻 Author

Prepared as part of **DSA practice for coding interviews**

---

⭐ If this helped you, consider starring your repository!
