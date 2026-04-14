# 🔗 Sort Linked List using Merge Sort (O(n log n))

This project implements sorting of a singly linked list using the **Merge Sort algorithm**, which is optimal for linked lists due to its efficient splitting and merging strategy.

---

## 📌 Problem Statement

Given the `head` of a linked list, return the list after sorting it in **ascending order**.

---

## 🔍 Example

### Input:

```
4 → 2 → 1 → 3
```

### Output:

```
1 → 2 → 3 → 4
```

---

## 🚀 Approach: Merge Sort on Linked List

Merge Sort follows **Divide and Conquer**:

1. **Divide** → Split the list into two halves
2. **Conquer** → Recursively sort both halves
3. **Combine** → Merge the sorted halves

---

## 🧠 Key Concepts

### ✅ 1. Finding the Middle

We use **slow and fast pointers**:

* `slow` moves 1 step
* `fast` moves 2 steps
* `fast = head.next` ensures balanced split

---

### ✅ 2. Splitting the List

```java
ListNode rightHead = mid.next;
mid.next = null;
```

👉 This is the **most important step**
👉 It breaks the list into two independent halves

---

### ✅ 3. Merging Two Sorted Lists

We merge using a **dummy node** to simplify pointer handling.

---

## ⚙️ Algorithm Steps

1. Base case:

   * If list is empty or has one node → already sorted

2. Find middle using slow-fast pointers

3. Split the list:

   * Left half → `head`
   * Right half → `mid.next`

4. Recursively sort both halves

5. Merge sorted halves

---

## ✅ Java Implementation

```java
class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode mid = getMid(head);
        ListNode rightHead = mid.next;
        mid.next = null;

        ListNode left = sortList(head);
        ListNode right = sortList(rightHead);

        return merge(left, right);
    }

    private ListNode getMid(ListNode head) {
        ListNode slow = head;
        ListNode fast = head.next;

        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }

    private ListNode merge(ListNode head1, ListNode head2) {
        ListNode dummy = new ListNode();
        ListNode tail = dummy;

        while (head1 != null && head2 != null) {
            if (head1.val < head2.val) {
                tail.next = head1;
                head1 = head1.next;
            } else {
                tail.next = head2;
                head2 = head2.next;
            }
            tail = tail.next;
        }

        tail.next = (head1 != null) ? head1 : head2;

        return dummy.next;
    }
}
```

---

## 📊 Complexity Analysis

| Metric           | Value                      |
| ---------------- | -------------------------- |
| Time Complexity  | O(n log n)                 |
| Space Complexity | O(log n) (recursion stack) |

---

## 🔥 Why Merge Sort for Linked List?

* No random access needed (unlike arrays)
* Efficient splitting using pointers
* Stable sorting
* Optimal time complexity

---

## ⚠️ Common Mistakes

* ❌ Not breaking the list (`mid.next = null`) → infinite recursion
* ❌ Wrong middle calculation → unbalanced split
* ❌ Forgetting base case

---

## 🎯 Interview Tips

> “Merge Sort is preferred for linked lists because it avoids random access and maintains O(n log n) complexity with minimal extra space.”

---

## 🚀 Related Problems

* Merge Two Sorted Lists
* Sort Array (Merge Sort)
* Merge K Sorted Lists
* Linked List Cycle Detection

---

## 👨‍💻 Author

Prepared as part of **DSA Interview Preparation**.

---

⭐ If this helped you, consider starring your repository!
