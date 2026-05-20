# Sort Colors

## Problem

Given an array:

```text
nums = [2,0,2,1,1,0]
```

where:

```text
0 = Red
1 = White
2 = Blue
```

Sort the array **in-place** so that:

```text
0s first
1s next
2s last
```

Output:

```text
[0,0,1,1,2,2]
```

---

# Intuition

This is also called the **Dutch National Flag Problem**.

We need to separate:

```text
0s | 1s | 2s
```

Instead of sorting the entire array.

We maintain regions:

```text
[0....low-1]      -> all 0s
[low....mid-1]    -> all 1s
[mid....high]     -> unknown
[high+1....n-1]   -> all 2s
```

Process the unknown region.

---

# Approach 1 — Brute Force

## Idea

Simply sort.

---

## Code

```java
import java.util.Arrays;

class Solution {

    public void sortColors(int[] nums) {
        Arrays.sort(nums);
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
depends on sorting
```

---

# Approach 2 — Better (Counting)

## Intuition

Count:

- number of 0s
- number of 1s
- number of 2s

Then overwrite array.

---

## Code

```java
class Solution {

    public void sortColors(int[] nums) {

        int zero=0;
        int one=0;
        int two=0;

        for(int num:nums){

            if(num==0)
                zero++;

            else if(num==1)
                one++;

            else
                two++;
        }

        int index=0;

        while(zero-- >0)
            nums[index++]=0;

        while(one-- >0)
            nums[index++]=1;

        while(two-- >0)
            nums[index++]=2;
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
O(1)
```

---

# Approach 3 — Optimal (Dutch National Flag)

## Key Idea

Use 3 pointers:

```text
low
mid
high
```

Initial:

```text
low=0
mid=0
high=n-1
```

---

### If nums[mid]==0

Swap:

```text
nums[low]
nums[mid]
```

Move:

```text
low++
mid++
```

---

### If nums[mid]==1

Already in correct region.

Move:

```text
mid++
```

---

### If nums[mid]==2

Swap:

```text
nums[mid]
nums[high]
```

Move:

```text
high--
```

Do NOT move `mid`.

Reason:

New element came from right side and is unprocessed.

---

## Code

```java
class Solution {

    public void sortColors(int[] nums) {

        int low=0;
        int mid=0;
        int high=nums.length-1;

        while(mid<=high){

            if(nums[mid]==0){

                swap(nums,low,mid);

                low++;
                mid++;
            }

            else if(nums[mid]==1){

                mid++;
            }

            else{

                swap(nums,mid,high);

                high--;
            }
        }
    }

    private void swap(int[] arr,int i,int j){

        int temp=arr[i];
        arr[i]=arr[j];
        arr[j]=temp;
    }
}
```

---

# Dry Run

Input:

```text
[2,0,2,1,1,0]
```

Initial:

```text
low=0
mid=0
high=5
```

nums[mid]=2

Swap:

```text
2 ↔ 0
```

Array:

```text
[0,0,2,1,1,2]
```

high--

Continue...

Final:

```text
[0,0,1,1,2,2]
```

---

# Why don't we increment mid after swapping with high?

Suppose:

```text
[2,1,0]
```

Swap:

```text
2 ↔ 0
```

becomes:

```text
[0,1,2]
```

The incoming value from `high` may be:

```text
0
1
or
2
```

Still unprocessed.

Need to examine it.

---

# Complexity

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

# Comparison

| Approach | Time | Space |
|----------|------|--------|
| Sort | O(n log n) | depends |
| Counting | O(n) | O(1) |
| Dutch National Flag | O(n) | O(1) |

---

# Pattern Recognition

If array contains:

```text
only 3 categories
```

Think:

```text
Dutch National Flag
```

---

# Key Interview Takeaway

Maintain:

```text
0-region
1-region
unknown
2-region
```

and process unknown region.

---

# One-line Memory Trick

```text
0 → low++
1 → mid++
2 → high--
```
