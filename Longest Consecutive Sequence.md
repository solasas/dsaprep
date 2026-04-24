# Longest Consecutive Sequence

## Problem
Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

### Example

```text
Input: [100,4,200,1,3,2]

Output: 4

Explanation:
Longest consecutive sequence is:
1,2,3,4
Length = 4
```

---

# Intuition

The word **consecutive** suggests numbers like:

```text
x, x+1, x+2, x+3 ...
```

The challenge is finding the **longest streak**.

There are three ways to solve it:

1. Brute Force → Check every sequence manually
2. Better Approach → Sort first
3. Optimal Approach → HashSet in O(n)

---

# Approach 1: Brute Force (Naive)

## Idea
For every element:

- treat it as a possible start
- keep checking if next consecutive number exists

Example:

```text
1 -> check 2 -> check 3 -> check 4
```

Use linear search every time.

---

## Code

```java
class Solution {

    public int longestConsecutive(int[] nums) {

        int longest = 0;

        for(int i=0;i<nums.length;i++){

            int current = nums[i];
            int count = 1;

            while(contains(nums,current+1)){
                current++;
                count++;
            }

            longest=Math.max(longest,count);
        }

        return longest;
    }

    private boolean contains(int[] nums,int target){
        for(int num:nums){
            if(num==target){
                return true;
            }
        }
        return false;
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

# Approach 2: Better (Sorting)

## Intuition

Sort the array first:

```text
[100,4,200,1,3,2]
```

becomes

```text
[1,2,3,4,100,200]
```

Now just count streaks.

---

## Algorithm

- Sort array
- If current = previous + 1

continue streak

- Otherwise reset streak

---

## Code

```java
import java.util.Arrays;

class Solution {

    public int longestConsecutive(int[] nums) {

        if(nums.length==0) return 0;

        Arrays.sort(nums);

        int longest=1;
        int count=1;

        for(int i=1;i<nums.length;i++){

            if(nums[i]==nums[i-1]){
                continue;
            }

            if(nums[i]==nums[i-1]+1){
                count++;
            }
            else{
                count=1;
            }

            longest=Math.max(longest,count);
        }

        return longest;
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

---

# Approach 3: Optimal (HashSet)

## Key Insight

Do NOT start counting from every number.

Only start from a number if it is the **beginning** of a sequence.

A number is a beginning if:

```java
!set.contains(num-1)
```

Example:

```text
1,2,3,4
```

Start only from `1`

Skip:

```text
2
3
4
```

because they are not beginnings.

---

## Why this matters

Without this:

Repeated work.

With this:

Every sequence counted once.

---

## Algorithm

1. Put all numbers in HashSet

2. For every number:

If no previous number exists

```java
num-1 not in set
```

start expanding:

```java
num+1
num+2
...
```

3. Track maximum streak.

---

## Code

```java
import java.util.HashSet;
import java.util.Set;

class Solution {

    public int longestConsecutive(int[] nums) {

        if(nums.length==0) return 0;

        Set<Integer> set=new HashSet<>();

        for(int num:nums){
            set.add(num);
        }

        int longest=0;

        for(int num:set){

            if(!set.contains(num-1)){

                int current=num;
                int streak=1;

                while(set.contains(current+1)){
                    current++;
                    streak++;
                }

                longest=Math.max(longest,streak);
            }
        }

        return longest;
    }
}
```

---

## Dry Run

Input:

```text
[100,4,200,1,3,2]
```

Set:

```text
{100,4,200,1,3,2}
```

Starts of sequences:

- 100
- 200
- 1

For 1:

```text
1→2→3→4
```

Length = 4

Answer = 4

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

# Why O(n) and not O(n²)?

Although there is a while loop:

```java
while(set.contains(current+1))
```

each element is visited at most once in sequence expansion.

So total work remains linear.

---

# Comparison

| Approach | Time | Space |
|---------|------|-------|
| Brute Force | O(n²) | O(1) |
| Sorting | O(n log n) | O(1) |
| HashSet Optimal | O(n) | O(n) |

---

# Pattern Recognition

If problem mentions:

- consecutive sequence
- unsorted array
- O(n) expected

Think:

```text
HashSet + detect starts of sequence
```

---

# Key Interview Takeaway

The trick is:

```java
if(!set.contains(num-1))
```

That single line makes the solution optimal.
