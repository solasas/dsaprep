# Count Substrings Containing All Three Characters (`a`, `b`, `c`)
https://www.geeksforgeeks.org/problems/count-substring/1
## Problem Statement

Given a string `s` consisting only of characters:

```text
a, b, c
```

Return the number of substrings containing **at least one occurrence of all three characters**.

### Example

Input:

```text
s = "abcabc"
```

Output:

```text
10
```

---

# Approach 1: Brute Force

## Idea

Generate all possible substrings and check whether each substring contains:

```text
a
b
c
```

Use a frequency array:

```java
int[] freq = new int[3];
```

where:

```text
freq[0] → count of a
freq[1] → count of b
freq[2] → count of c
```

Instead of recounting from scratch, expand the substring and update frequencies.

---

## Algorithm

1. Fix starting index `i`
2. Expand ending index `j`
3. Add current character frequency
4. Check if:

```java
freq[0] > 0 &&
freq[1] > 0 &&
freq[2] > 0
```

5. If yes:

```java
count++;
```

---

## Code

```java
class Solution {
    public static int countSubstring(String s) {

        int n = s.length();
        int count = 0;

        for(int i=0;i<n;i++){

            int[] freq = new int[3];

            for(int j=i;j<n;j++){

                freq[s.charAt(j)-'a']++;

                if(freq[0] > 0 &&
                   freq[1] > 0 &&
                   freq[2] > 0){

                    count++;
                }
            }
        }

        return count;
    }
}
```

---

## Dry Run

Input:

```text
s = "abc"
```

Substrings:

```text
a      ❌
ab     ❌
abc    ✅
b      ❌
bc     ❌
c      ❌
```

Answer:

```text
1
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

# Approach 2: Optimal Sliding Window

## Observation

Once a window contains:

```text
a,b,c
```

then every larger substring extending to the right is also valid.

Example:

```text
abc
abca
abcab
abcabc
```

Instead of counting individually:

Count all at once.

---

## Formula

When current window becomes valid:

```java
count += s.length()-right;
```

Because every future extension remains valid.

---

## Algorithm

1. Expand `right`
2. Add frequency
3. While window contains all:

```text
a,b,c
```

4. Add:

```java
count += n-right;
```

5. Shrink from left

---

## Code

```java
class Solution {
    public static int countSubstring(String s) {

        int[] freq = new int[3];

        int left = 0;
        int count = 0;

        for(int right=0;right<s.length();right++){

            freq[s.charAt(right)-'a']++;

            while(freq[0] > 0 &&
                  freq[1] > 0 &&
                  freq[2] > 0){

                count += s.length()-right;

                freq[s.charAt(left)-'a']--;

                left++;
            }
        }

        return count;
    }
}
```

---

## Dry Run

Input:

```text
s="abcabc"
```

Window:

```text
abc
```

Valid

Count:

```java
count += 6-2;
```

```text
4
```

Substrings counted:

```text
abc
abca
abcab
abcabc
```

Move left and continue.

---

## Complexity

| Approach | Time | Space |
|-----------|-------|--------|
| Brute Force | O(n²) | O(1) |
| Sliding Window | O(n) | O(1) |

---

# Pattern Learned

Problems involving:

```text
Count substrings
Condition satisfied
All future extensions also valid
```

Usually suggest:

```text
Sliding Window + count += n-right
```

Very important interview pattern.
