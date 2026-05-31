# 3Sum

## Problem

Given an integer array `nums`, return all unique triplets:

```text
[a, b, c]
```

such that:

```text
a + b + c = 0
```

No duplicate triplets should be returned.

---

## Example

```text
Input:
[-1,0,1,2,-1,-4]

Output:
[[-1,-1,2],[-1,0,1]]
```

---

# Intuition

Brute force is easy:

Pick every possible triplet and check if sum is 0.

But:

```text
O(n³)
```

Too slow.

---

# Approach 1 — Brute Force

## Idea

Try every triplet.

---

## Code

```java
class Solution {

    public List<List<Integer>> threeSum(int[] nums) {

        Set<List<Integer>> set = new HashSet<>();

        int n = nums.length;

        for(int i=0;i<n;i++){

            for(int j=i+1;j<n;j++){

                for(int k=j+1;k<n;k++){

                    if(nums[i]+nums[j]+nums[k]==0){

                        List<Integer> temp =
                            Arrays.asList(nums[i],nums[j],nums[k]);

                        Collections.sort(temp);

                        set.add(temp);
                    }
                }
            }
        }

        return new ArrayList<>(set);
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
O(number of triplets)
```

---

# Approach 2 — Better (HashSet)

## Idea

Fix first element.

Convert remaining problem into:

```text
Two Sum
```

For each `i`:

Find:

```text
nums[j] + nums[k] = -nums[i]
```

using HashSet.

---

## Code

```java
class Solution {

    public List<List<Integer>> threeSum(int[] nums) {

        Set<List<Integer>> result = new HashSet<>();

        int n = nums.length;

        for(int i=0;i<n;i++){

            Set<Integer> seen = new HashSet<>();

            for(int j=i+1;j<n;j++){

                int third = -(nums[i] + nums[j]);

                if(seen.contains(third)){

                    List<Integer> triplet =
                        Arrays.asList(nums[i], nums[j], third);

                    Collections.sort(triplet);

                    result.add(triplet);
                }

                seen.add(nums[j]);
            }
        }

        return new ArrayList<>(result);
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
O(n)
```

---

# Approach 3 — Optimal (Sorting + Two Pointers)

## Key Insight

Sort first.

Then:

- Fix one element.
- Solve remaining part using two pointers.

---

## Example

```text
[-1,0,1,2,-1,-4]
```

Sort:

```text
[-4,-1,-1,0,1,2]
```

---

## Fix First Element

Suppose:

```text
i = -1
```

Need:

```text
two numbers whose sum = 1
```

Use:

```text
left
right
```

just like Two Sum.

---

# Algorithm

1. Sort array.
2. Fix `i`.
3. Use:

```java
left = i+1
right = n-1
```

4. Calculate:

```java
sum = nums[i] + nums[left] + nums[right]
```

---

### If sum < 0

Need bigger value.

```java
left++
```

---

### If sum > 0

Need smaller value.

```java
right--
```

---

### If sum == 0

Triplet found.

Store it.

Move both pointers.

Skip duplicates.

---

## Code

```java
class Solution {

    public List<List<Integer>> threeSum(int[] nums) {

        List<List<Integer>> ans = new ArrayList<>();

        Arrays.sort(nums);

        int n = nums.length;

        for(int i=0;i<n-2;i++){

            if(i>0 && nums[i]==nums[i-1]){
                continue;
            }

            int left = i+1;
            int right = n-1;

            while(left < right){

                int sum =
                    nums[i] + nums[left] + nums[right];

                if(sum == 0){

                    ans.add(
                        Arrays.asList(
                            nums[i],
                            nums[left],
                            nums[right]
                        )
                    );

                    left++;
                    right--;

                    while(left < right &&
                          nums[left] == nums[left-1]){
                        left++;
                    }

                    while(left < right &&
                          nums[right] == nums[right+1]){
                        right--;
                    }
                }

                else if(sum < 0){
                    left++;
                }

                else{
                    right--;
                }
            }
        }

        return ans;
    }
}
```

---

# Dry Run

Input:

```text
[-1,0,1,2,-1,-4]
```

Sorted:

```text
[-4,-1,-1,0,1,2]
```

---

Fix:

```text
i = -1
```

Pointers:

```text
left = -1
right = 2
```

Sum:

```text
-1 + (-1) + 2 = 0
```

Triplet:

```text
[-1,-1,2]
```

---

Next:

```text
-1 + 0 + 1 = 0
```

Triplet:

```text
[-1,0,1]
```

Done.

---

# Why Sorting Helps

After sorting:

```text
small values → left
large values → right
```

So we can decide:

```text
sum too small?
move left

sum too large?
move right
```

without checking every pair.

---

# Complexity

Sorting:

```text
O(n log n)
```

Two pointer scan:

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

(ignoring output list)

---

# Comparison

| Approach | Time | Space |
|-----------|--------|--------|
| Brute Force | O(n³) | O(1) |
| HashSet | O(n²) | O(n) |
| Sorting + Two Pointers | O(n²) | O(1) |

---

# Pattern Recognition

When you see:

```text
3 numbers
sum = target
```

Think:

```text
Fix one element
Convert remaining problem to Two Sum
```

---

# Key Interview Takeaway

3Sum is simply:

```text
Two Sum + Sorting + Two Pointers
```

---

# One-Line Memory Trick

```text
Fix one number,
find remaining two using left and right pointers.
```
