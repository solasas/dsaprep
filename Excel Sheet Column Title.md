# Excel Sheet Column Title (LeetCode 168)

## Problem
Convert a positive integer into its corresponding Excel column title.

Examples:

```text
1  -> A
2  -> B
26 -> Z
27 -> AA
28 -> AB
701 -> ZY
```

---

# Intuition

This looks like base-26 conversion, but there is a twist:

Normal base-26 digits are:

```text
0-25
```

But Excel columns use:

```text
1-26
```

```text
A = 1
B = 2
...
Z = 26
```

There is **no zero digit**, and that creates the main challenge.

---

# Key Trick

Before taking modulo:

```java
columnNumber--;
```

We shift:

```text
1..26  -> 0..25
```

Now modulo works correctly.

---

## Why decrement?

### Example: 26

Expected:

```text
26 -> Z
```

Without decrement:

```text
26 % 26 = 0 -> A (wrong)
```

---

With decrement:

```text
26-1 = 25

25 % 26 = 25 -> Z
```

Correct.

---

## Example: 27

Expected:

```text
27 -> AA
```

Step 1:

```text
27-1 = 26

26 % 26 = 0 -> A
26 / 26 = 1
```

Step 2:

```text
1-1 = 0

0 % 26 = 0 -> A
```

Reverse:

```text
AA
```

Correct.

---

# Algorithm

Repeat while number > 0:

1. Decrement number

```java
columnNumber--;
```

2. Find current letter

```java
remainder = columnNumber % 26
```

3. Convert to character

```java
(char)(remainder + 'A')
```

4. Reduce number

```java
columnNumber /= 26
```

5. Reverse result at end.

---

# Code

```java
class Solution {
    public String convertToTitle(int columnNumber) {

        StringBuilder sb = new StringBuilder();

        while(columnNumber > 0){

            columnNumber--; // shift from 1-26 to 0-25

            int rem = columnNumber % 26;

            sb.append((char)(rem + 'A'));

            columnNumber /= 26;
        }

        return sb.reverse().toString();
    }
}
```

---

# Dry Run

Input:

```text
52
```

Iteration 1:

```text
52-1 = 51
51 % 26 = 25 -> Z
51 / 26 = 1
```

Iteration 2:

```text
1-1 = 0
0 % 26 = 0 -> A
```

Built string:

```text
ZA
```

Reverse:

```text
AZ
```

Answer:

```text
52 -> AZ
```

---

# Time Complexity

```text
O(log26 n)
```

---

# Space Complexity

```text
O(log26 n)
```

---

# Pattern

This follows modified base conversion:

```java
while(n > 0){
    n--;
    digit = n % 26;
    add corresponding letter;
    n /= 26;
}
reverse();
```

---

## Core Insight

The decrement:

```java
columnNumber--;
```

is NOT for ASCII.

It fixes Excel's numbering system:

```text
1..26 -> 0..25
```

Then:

```java
(char)(rem + 'A')
```

uses ASCII to convert number to letter.

Two separate ideas.
