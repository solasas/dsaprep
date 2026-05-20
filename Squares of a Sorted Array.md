# Squares of a Sorted Array

## Problem

Given a sorted integer array `nums` (can contain negative values), return an array of the squares of each number sorted in non-decreasing order.

---

## Example 1

```text
Input:
nums = [-4,-1,0,3,10]

Output:
[0,1,9,16,100]
```

Explanation:

```text
Squares:
16,1,0,9,100

Sorted:
0,1,9,16,100
```

---

## Example 2

```text
Input:
nums = [-7,-3,2,3,11]

Output:
[4,9,9,49,121]
```

---

# Intuition

The array is sorted:

```text
[-7,-3,2,3,11]
```

But after squaring:

```text
49,9,4,9,121
```

Not sorted anymore.

Why?

Because:

```text
negative numbers become positive
```

and large negative values can produce large squares.

Observation:

Largest square always comes from either:

```text
left end
or
right end
```

Because:

```text
|-7| > |2|
```

Use two pointers:

- `left` → start
- `right` → end

Compare absolute values and place larger square at the end.

---

# Approach 1 — Brute Force

## Idea

Square every element and sort.

---

## Code

```java
import java.util.Arrays;

class Solution {

    public int[] sortedSquares(int[] nums) {

        for(int i=0;i<nums.length;i++){
            nums[i]=nums[i]*nums[i];
        }

        Arrays.sort(nums);

        return nums;
    }
}
```

---

## Complexity

Time:

```text
O(n log n)
```

Space:

```text
O(1)
```

(ignoring sorting internals)

---

# Approach 2 — Optimal (Two Pointers)

## Key Insight

Largest square lies at either end.

Fill answer array from back.

---

## Algorithm

1. `left = 0`
2. `right = n-1`
3. Compare:

```java
Math.abs(nums[left])
Math.abs(nums[right])
```

4. Put larger square at:

```java
answer[index]
```

5. Move pointer

---

## Code

```java
class Solution {

    public int[] sortedSquares(int[] nums) {

        int n=nums.length;

        int left=0;
        int right=n-1;

        int[] ans=new int[n];

        int index=n-1;

        while(left<=right){

            int leftSquare =
                    nums[left]*nums[left];

            int rightSquare =
                    nums[right]*nums[right];

            if(leftSquare > rightSquare){

                ans[index]=leftSquare;
                left++;
            }
            else{

                ans[index]=rightSquare;
                right--;
            }

            index--;
        }

        return ans;
    }
}
```

---

# Dry Run

Input:

```text
[-4,-1,0,3,10]
```

Initial:

```text
left=0
right=4
index=4
```

Compare:

```text
16 vs 100
```

Put:

```text
100
```

Answer:

```text
[_,_,_,_,100]
```

Move:

```text
right--
```

---

Compare:

```text
16 vs 9
```

Put:

```text
16
```

Answer:

```text
[_,_,_,16,100]
```

Move:

```text
left++
```

Continue...

Final:

```text
[0,1,9,16,100]
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

# Why does this work?

Because:

```text
largest absolute value
=
largest square
```

Largest absolute value always exists at boundaries of a sorted array.

---

# Pattern Recognition

When:

- sorted array
- negatives and positives
- compare extremes

Think:

```text
Two Pointers
```

---

# Comparison

| Approach | Time | Space |
|----------|------|--------|
| Square + Sort | O(n log n) | O(1) |
| Two Pointer | O(n) | O(n) |

---

# Key Interview Takeaway

Instead of sorting after transformation:

```text
Use properties of sorted array
```

---

# One-line Memory Trick

```text
Biggest square comes from biggest absolute value at either end.
```
