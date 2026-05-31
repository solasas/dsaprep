# 3Sum Closest

## Problem

Given an integer array `nums` and an integer `target`, find three integers such that:

```text
nums[i] + nums[j] + nums[k]
```

is closest to `target`.

Return the sum of the three integers.

---

## Example

```text
Input:
nums = [-1,2,1,-4]
target = 1

Output:
2
```

Explanation:

```text
(-1 + 2 + 1) = 2
```

Closest to:

```text
1
```

Difference:

```text
|2 - 1| = 1
```

---

# Intuition

This problem is very similar to:

```text
3Sum
```

Difference:

### 3Sum

Need:

```text
sum == target
```

(or 0 in original problem)

---

### 3Sum Closest

Need:

```text
sum closest to target
```

Not necessarily equal.

---

# Brute Force

Try every triplet.

Compute:

```text
abs(sum - target)
```

Keep minimum.

---

## Code

```java
class Solution {

    public int threeSumClosest(int[] nums, int target) {

        int closest = Integer.MAX_VALUE;

        int n = nums.length;

        for(int i=0;i<n;i++){

            for(int j=i+1;j<n;j++){

                for(int k=j+1;k<n;k++){

                    int sum =
                        nums[i]+nums[j]+nums[k];

                    if(Math.abs(sum-target)
                        <
                       Math.abs(closest-target))
                    {
                        closest=sum;
                    }
                }
            }
        }

        return closest;
    }
}
```

---

## Complexity

Time:

```text
O(n³)
```

Space:

```text
O(1)
```

---

# Optimal Approach (Sorting + Two Pointers)

## Key Idea

Sort the array first.

Fix one element.

Use two pointers for the remaining two numbers.

Exactly like 3Sum.

---

## Why Sorting Helps

After sorting:

```text
sum too small ?
move left++

sum too large ?
move right--
```

This allows us to improve the sum efficiently.

---

# Algorithm

1. Sort array.
2. Fix element `i`.
3. Set:

```java
left = i+1;
right = n-1;
```

4. Compute:

```java
sum = nums[i] + nums[left] + nums[right];
```

5. Update closest sum if needed.
6. Move pointers.

---

# Code

```java
import java.util.Arrays;

class Solution {

    public int threeSumClosest(int[] nums,
                               int target) {

        Arrays.sort(nums);

        int closest =
            nums[0] + nums[1] + nums[2];

        int n = nums.length;

        for(int i=0;i<n-2;i++){

            int left = i+1;
            int right = n-1;

            while(left < right){

                int sum =
                    nums[i]
                    + nums[left]
                    + nums[right];

                if(Math.abs(sum-target)
                    <
                   Math.abs(closest-target))
                {
                    closest = sum;
                }

                if(sum < target){
                    left++;
                }
                else if(sum > target){
                    right--;
                }
                else{
                    return sum;
                }
            }
        }

        return closest;
    }
}
```

---

# Dry Run

Input:

```text
nums = [-1,2,1,-4]
target = 1
```

---

## Sort

```text
[-4,-1,1,2]
```

---

## Initialize

```text
closest = -4 + (-1) + 1
        = -4
```

---

## i = 0

```text
left = 1
right = 3
```

Sum:

```text
-4 + (-1) + 2
= -3
```

Closer than:

```text
-4
```

Update:

```text
closest = -3
```

Move:

```text
left++
```

---

Next:

```text
-4 + 1 + 2
= -1
```

Closer.

Update:

```text
closest = -1
```

---

## i = 1

```text
left=2
right=3
```

Sum:

```text
-1 + 1 + 2
= 2
```

Difference:

```text
|2-1|=1
```

Best.

Update:

```text
closest=2
```

Answer:

```text
2
```

---

# Why Initialize Like This?

Instead of:

```java
Integer.MAX_VALUE
```

use:

```java
nums[0]+nums[1]+nums[2]
```

because we need a valid sum to compare against.

---

# Complexity

Sorting:

```text
O(n log n)
```

Two Pointer Scan:

```text
O(n²)
```

Total:

```text
O(n²)
```

Space:

```text
O(1)
```

---

# Comparison

| Approach | Time | Space |
|-----------|--------|--------|
| Brute Force | O(n³) | O(1) |
| Sorting + Two Pointers | O(n²) | O(1) |

---

# Pattern Recognition

If you see:

```text
3 numbers
sum closest to target
```

Think:

```text
Sort
Fix one element
Two pointers
Track closest sum
```

---

# Difference from 3Sum

### 3Sum

```text
Need exact match
Store triplets
```

---

### 3Sum Closest

```text
Need closest match
Store only best sum
```

---

# One-Line Memory Trick

```text
Fix one number,
use two pointers,
keep updating the closest sum.
```
