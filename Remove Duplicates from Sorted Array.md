# Remove Duplicates from Sorted Array

## Problem

Given a **sorted array** `nums`, remove duplicates **in-place** such that each unique element appears only once.

Return the number of unique elements `k`.

The first `k` positions of the array should contain the unique elements.

---

## Example 1

```text
Input:
nums = [1,1,2]

Output:
2

Modified array:
[1,2,_]
```

---

## Example 2

```text
Input:
nums = [0,0,1,1,1,2,2,3,3,4]

Output:
5

Modified array:
[0,1,2,3,4,_,_,_,_,_]
```

---

# Intuition

Since the array is **sorted**, all duplicates appear **next to each other**.

Example:

```text
[1,1,1,2,2,3,3,4]
```

Duplicates are adjacent.

We don't need extra memory.

We can overwrite duplicates while keeping unique values at the front.

This is a classic **Two Pointer** problem.

---

# Approach 1 — Brute Force (Using Extra Data Structure)

## Idea

Use a Set to keep unique elements.

Then copy them back.

---

## Code

```java
import java.util.*;

class Solution {
    public int removeDuplicates(int[] nums) {

        Set<Integer> set = new LinkedHashSet<>();

        for(int num : nums){
            set.add(num);
        }

        int index = 0;

        for(int val : set){
            nums[index++] = val;
        }

        return set.size();
    }
}
```

---

## Complexity

Time:

```text
O(n)
```

Space:

```text
O(n)
```

---

# Approach 2 — Optimal (Two Pointers)

## Key Idea

Use:

- `i` → last unique element index
- `j` → scan through array

Whenever we find a new value:

Move `i` ahead and place it there.

---

## Algorithm

1. Start:

```java
i=0
```

2. Traverse:

```java
j=1 → n-1
```

3. If:

```java
nums[i]!=nums[j]
```

new element found.

Move:

```java
i++
nums[i]=nums[j]
```

---

## Code

```java
class Solution {

    public int removeDuplicates(int[] nums) {

        int n = nums.length;

        int i = 0;

        for(int j=1;j<n;j++){

            if(nums[i] != nums[j]){

                i++;

                nums[i]=nums[j];
            }
        }

        return i+1;
    }
}
```

---

# Dry Run

Input:

```text
[1,1,2,2,3]
```

Initial:

```text
i=0
j=1
```

---

j=1

```text
1 ==1
skip
```

---

j=2

```text
1 !=2
```

Move:

```text
i=1
nums[1]=2
```

Array:

```text
[1,2,2,2,3]
```

---

j=3

```text
2==2
skip
```

---

j=4

```text
2!=3
```

Move:

```text
i=2
nums[2]=3
```

Array:

```text
[1,2,3,2,3]
```

Only first:

```text
i+1=3
```

elements matter.

---

Final:

```text
[1,2,3,_,_]
```

Answer:

```text
3
```

---

## Complexity

Time:

```text
O(n)
```

Space:

```text
O(1)
```

Optimal.

---

# Why does this work?

Because array is sorted:

```text
duplicates stay together
```

So comparing:

```java
nums[i]
```

with

```java
nums[j]
```

is enough.

---

# Pattern Recognition

When:

- array is sorted
- remove duplicates
- modify in-place

Think:

```text
Two Pointers
```

---

# Key Interview Takeaway

```java
if(nums[i]!=nums[j]){
    i++;
    nums[i]=nums[j];
}
```

This single block performs:

- detection
- shifting
- insertion

---

# Comparison

| Approach | Time | Space |
|----------|------|--------|
| Set | O(n) | O(n) |
| Two Pointer | O(n) | O(1) |

---

# One-line Memory Trick

```text
Keep unique values at front while scanning forward.
```
