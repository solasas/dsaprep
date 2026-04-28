# Rotate Array by K Places (Left and Right Rotation)

## Problem
Rotate an array by `k` places.

There are two types:

---

# 1) Left Rotation

Move the **first k elements** to the end.

## Example

```text
Input:
[1,2,3,4,5]
k=2

Output:
[3,4,5,1,2]
```

---

## Intuition

Split array into two parts:

```text
[1,2] [3,4,5]
```

After left rotation:

```text
[3,4,5] [1,2]
```

We move the front block to the back.

---

# Approach 1 — Brute Force

Rotate left one place, `k` times.

## Left Rotate by 1

```text
Store first element
Shift everything left
Put first element at end
```

---

## Code

```java
class Solution {

    public void rotateLeft(int[] arr,int k){

        int n=arr.length;

        k%=n;

        for(int r=0;r<k;r++){

            int temp=arr[0];

            for(int i=1;i<n;i++){
                arr[i-1]=arr[i];
            }

            arr[n-1]=temp;
        }
    }
}
```

---

## Complexity

Time:

```text
O(n*k)
```

Space:

```text
O(1)
```

---

# Approach 2 — Better (Extra Array)

## Idea

Store rotated positions directly.

---

## Code

```java
class Solution {

    public void rotateLeft(int[] nums,int k){

        int n=nums.length;
        k%=n;

        int[] temp=new int[n];

        for(int i=0;i<n;i++){
            temp[i]=nums[(i+k)%n];
        }

        for(int i=0;i<n;i++){
            nums[i]=temp[i];
        }
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

# Approach 3 — Optimal (Reversal Algorithm)

## Key Idea

Reverse 3 times.

Example:

```text
1 2 3 4 5
k=2
```

Split:

```text
[1 2] [3 4 5]
```

---

### Step 1

Reverse first k:

```text
2 1 3 4 5
```

---

### Step 2

Reverse remaining:

```text
2 1 5 4 3
```

---

### Step 3

Reverse whole array:

```text
3 4 5 1 2
```

Done.

---

## Code

```java
class Solution {

    public void rotateLeft(int[] nums,int k){

        int n=nums.length;

        k%=n;

        reverse(nums,0,k-1);
        reverse(nums,k,n-1);
        reverse(nums,0,n-1);
    }

    private void reverse(int[] arr,int l,int r){

        while(l<r){

            int temp=arr[l];
            arr[l]=arr[r];
            arr[r]=temp;

            l++;
            r--;
        }
    }
}
```

---

## Complexity

Time

```text
O(n)
```

Space

```text
O(1)
```

Optimal.

---

---
# 2) Right Rotation

Move the **last k elements** to front.

---

## Example

```text
Input:
[1,2,3,4,5]
k=2
```

Output:

```text
[4,5,1,2,3]
```

---

## Intuition

Split:

```text
[1,2,3] [4,5]
```

After right rotation:

```text
[4,5] [1,2,3]
```

Back block comes to front.

---

# Approach 1 — Brute Force

Rotate right by one, k times.

---

## Code

```java
class Solution {

    public void rotateRight(int[] nums,int k){

        int n=nums.length;

        k%=n;

        for(int r=0;r<k;r++){

            int temp=nums[n-1];

            for(int i=n-2;i>=0;i--){
                nums[i+1]=nums[i];
            }

            nums[0]=temp;
        }
    }
}
```

---

## Complexity

```text
O(n*k)
```

---

# Approach 2 — Better (Extra Array)

## Formula

For right rotation:

```text
newIndex=(i+k)%n
```

---

## Code

```java
class Solution {

    public void rotateRight(int[] nums,int k){

        int n=nums.length;
        k%=n;

        int[] temp=new int[n];

        for(int i=0;i<n;i++){
            temp[(i+k)%n]=nums[i];
        }

        for(int i=0;i<n;i++){
            nums[i]=temp[i];
        }
    }
}
```

---

## Complexity

Time

```text
O(n)
```

Space

```text
O(n)
```

---

# Approach 3 — Optimal (Reversal Algorithm)

Example

```text
1 2 3 4 5 6 7
k=3
```

---

### Step 1

Reverse whole array

```text
7 6 5 4 3 2 1
```

---

### Step 2

Reverse first k

```text
5 6 7 4 3 2 1
```

---

### Step 3

Reverse rest

```text
5 6 7 1 2 3 4
```

Done.

---

## Code

```java
class Solution {

    public void rotate(int[] nums,int k){

        int n=nums.length;

        k%=n;

        reverse(nums,0,n-1);

        reverse(nums,0,k-1);

        reverse(nums,k,n-1);
    }

    private void reverse(int[] arr,int l,int r){

        while(l<r){

            int temp=arr[l];
            arr[l]=arr[r];
            arr[r]=temp;

            l++;
            r--;
        }
    }
}
```

---

## Complexity

Time

```text
O(n)
```

Space

```text
O(1)
```

Optimal.

---

# Comparison

| Approach | Time | Space |
|---------|------|-------|
| Brute Force | O(nk) | O(1) |
| Extra Array | O(n) | O(n) |
| Reversal Optimal | O(n) | O(1) |

---

# Key Difference

## Left Rotation

```text
First k go to end
```

---

## Right Rotation

```text
Last k come to front
```

---

# Memory Trick

## Left rotation

```text
Parts first
Whole last
```

```java
reverse(first k)
reverse(rest)
reverse(all)
```

---

## Right rotation

```text
Whole first
Parts later
```

```java
reverse(all)
reverse(first k)
reverse(rest)
```

---

# Important

Always do:

```java
k = k % n;
```

Because:

```text
Rotating n times gives original array
```

---

# Interview Preferred Solution

Use:

```text
Reversal Algorithm
```

It is the standard optimal solution.
