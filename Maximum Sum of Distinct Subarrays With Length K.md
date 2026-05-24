# Maximum Sum of Distinct Subarrays With Length K

## Problem Statement
Given an integer array `nums` and an integer `k`, find the maximum sum among all subarrays of size `k` such that all elements in the subarray are distinct.

Return the maximum sum. If no valid subarray exists, return `0`.

---

## Approach: Sliding Window + HashMap

We use a fixed-size sliding window of length `k`.

Maintain:

- `sum` → current window sum
- `HashMap<Integer,Integer>` → stores frequency of elements inside the current window
- `left` pointer → start of window
- `right` pointer → end of window

### Steps

1. Add current element into window
2. Update frequency in map
3. Add value to current sum
4. If window size exceeds `k`:
   - Remove left element
   - Decrease frequency
   - Remove from map if frequency becomes `0`
   - Move `left`
5. When window size becomes exactly `k`:
   - Check if `map.size()==k`
   - If true, all elements are distinct
   - Update maximum sum

---

## Why `map.size()==k` works

`map.size()` returns the number of unique elements.

Example:

Window:

```text
[2,9,9]
```

Map:

```text
{
2:1,
9:2
}
```

Window size:

```text
3
```

Map size:

```text
2
```

Since:

```text
window size != map size
```

A duplicate exists.

For distinct elements:

```text
[4,2,9]
```

Map:

```text
{
4:1,
2:1,
9:1
}
```

Window size:

```text
3
```

Map size:

```text
3
```

All elements are distinct.

---

## Java Solution

```java
class Solution {
    public long maximumSubarraySum(int[] nums, int k) {

        HashMap<Integer,Integer> map = new HashMap<>();

        long sum = 0;
        long maxSum = 0;

        int left = 0;

        for(int right=0; right<nums.length; right++){

            // Add current element
            sum += nums[right];

            map.put(
                nums[right],
                map.getOrDefault(nums[right],0)+1
            );

            // Shrink window if size exceeds k
            if(right-left+1 > k){

                sum -= nums[left];

                map.put(
                    nums[left],
                    map.get(nums[left])-1
                );

                if(map.get(nums[left])==0){
                    map.remove(nums[left]);
                }

                left++;
            }

            // Check valid window
            if(right-left+1==k && map.size()==k){
                maxSum=Math.max(maxSum,sum);
            }
        }

        return maxSum;
    }
}
```

---

## Dry Run

Input:

```text
nums = [1,5,4,2,9,9,9]
k = 3
```

Window 1:

```text
[1,5,4]

sum=10

map={1:1,5:1,4:1}

Distinct ✓
max=10
```

Window 2:

```text
[5,4,2]

sum=11

map={5:1,4:1,2:1}

Distinct ✓
max=11
```

Window 3:

```text
[4,2,9]

sum=15

map={4:1,2:1,9:1}

Distinct ✓
max=15
```

Window 4:

```text
[2,9,9]

map={2:1,9:2}

Duplicate exists ✗
```

Final Answer:

```text
15
```

---

## Time Complexity

```text
O(n)
```

Each element enters and leaves the window once.

---

## Space Complexity

```text
O(k)
```

HashMap stores at most `k` unique elements.

---

## Key Learning

- Fixed-size Sliding Window
- Frequency HashMap
- Window size maintenance
- Distinct element detection using `map.size()`
- Use `long` for sum to avoid overflow
