# Missing Number

## Problem

Given an array containing `n` distinct numbers in the range:

```text
[0, n]
```

Return the only number missing from the array.

---

## Example 1

```text
Input:
nums = [3,0,1]

Output:
2
```

Explanation:

Numbers should be:

```text
0,1,2,3
```

Missing:

```text
2
```

---

## Example 2

```text
Input:
nums = [0,1]

Output:
2
```

---

# Intuition

Array length:

```text
n
```

Numbers should contain:

```text
0 → n
```

Exactly one number is missing.

Idea:

Expected:

```text
0+1+2+...+n
```

Subtract actual sum.

Difference = missing number.

---

# Approach 1 — Brute Force

## Idea

For every number from:

```text
0 → n
```

search whether it exists.

---

## Code

```java
class Solution {

    public int missingNumber(int[] nums) {

        int n = nums.length;

        for(int i=0;i<=n;i++){

            boolean found=false;

            for(int num:nums){

                if(num==i){
                    found=true;
                    break;
                }
            }

            if(!found)
                return i;
        }

        return -1;
    }
}
```

---

## Complexity

Time:

```text
O(n²)
```

Space:

```text
O(1)
```

---

# Approach 2 — Better (HashSet)

## Idea

Store all numbers in a set.

Check:

```text
0 → n
```

Find missing value.

---

## Code

```java
import java.util.*;

class Solution {

    public int missingNumber(int[] nums) {

        Set<Integer> set=new HashSet<>();

        for(int num:nums){
            set.add(num);
        }

        for(int i=0;i<=nums.length;i++){

            if(!set.contains(i))
                return i;
        }

        return -1;
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

# Approach 3 — Better (Sorting)

## Idea

Sort array.

Check whether:

```text
nums[i]==i
```

First mismatch = answer.

---

## Code

```java
import java.util.Arrays;

class Solution {

    public int missingNumber(int[] nums) {

        Arrays.sort(nums);

        for(int i=0;i<nums.length;i++){

            if(nums[i]!=i)
                return i;
        }

        return nums.length;
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
depends on sort
```

---

# Approach 4 — Optimal (Math Formula)

## Key Idea

Expected sum:

```text
n(n+1)/2
```

Actual sum:

```text
sum of array
```

Difference:

```text
expected - actual
```

---

## Code

```java
class Solution {

    public int missingNumber(int[] nums) {

        int n=nums.length;

        int actual=0;

        for(int num:nums){
            actual+=num;
        }

        int expected=n*(n+1)/2;

        return expected-actual;
    }
}
```

---

# Dry Run

Input:

```text
[3,0,1]
```

n:

```text
3
```

Expected:

```text
3*(3+1)/2
=6
```

Actual:

```text
3+0+1
=4
```

Missing:

```text
6-4=2
```

Correct.

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

---

# Approach 5 — Optimal (XOR)

## Key Insight

Properties:

```text
a ^ a = 0
a ^ 0 = a
```

Same values cancel.

Compute:

```text
0^1^2^...^n
```

and XOR with array values.

Remaining value = missing number.

---

## Code

```java
class Solution {

    public int missingNumber(int[] nums) {

        int xor=nums.length;

        for(int i=0;i<nums.length;i++){

            xor ^= i;
            xor ^= nums[i];
        }

        return xor;
    }
}
```

---

# Dry Run

Input:

```text
[3,0,1]
```

Start:

```text
xor=3
```

Process:

```text
xor ^=0 ^=3
xor ^=1 ^=0
xor ^=2 ^=1
```

Everything cancels except:

```text
2
```

Answer:

```text
2
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

---

# Comparison

| Approach | Time | Space |
|----------|------|--------|
| Brute Force | O(n²) | O(1) |
| HashSet | O(n) | O(n) |
| Sorting | O(n log n) | O(1) |
| Math Formula | O(n) | O(1) |
| XOR | O(n) | O(1) |

---

# Which is best?

Math:

- simpler
- easier to explain

XOR:

- interview favorite
- avoids overflow issues

---

# Pattern Recognition

When:

```text
numbers from 0 to n
one missing
```

Think:

```text
Math sum
or
XOR
```

---

# One-line Memory Trick

```text
Expected sum - actual sum = missing number
```

or

```text
same XOR values cancel
```
