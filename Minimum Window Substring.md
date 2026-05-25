# Minimum Window Substring

## Problem Statement

Given two strings `s` and `t`, return the minimum window substring of `s` such that every character in `t` (including duplicates) is included in the window.

If no such substring exists, return an empty string `""`.

---

## Approach: Sliding Window + Frequency Arrays

We use two frequency arrays:

- `mapS` → stores frequency of characters inside the current window
- `mapT` → stores frequency of required characters from `t`

We maintain a sliding window:

- `i` → left pointer
- `right` → right pointer

Expand `right` until the current window becomes valid.

A window is valid if:

```text
Current window contains all required characters of t
```

Once valid:

- Update answer if current window is smaller
- Shrink from the left

---

## Algorithm

1. Store character frequencies of `t`
2. Start sliding window
3. Expand `right` pointer until all required characters are found
4. Check if current window is valid
5. Update minimum substring
6. Remove left character
7. Continue

---

## Java Solution

```java
class Solution {

    public String minWindow(String s, String t) {

        int[] mapS = new int[256];
        int[] mapT = new int[256];

        // frequency of t
        for(char ch : t.toCharArray()){
            mapT[ch]++;
        }

        String result = "";

        int right = 0;
        int min = Integer.MAX_VALUE;

        for(int i=0;i<s.length();i++){

            // expand window
            while(right<s.length()
                    && !isDesirable(mapS,mapT)){

                mapS[s.charAt(right)]++;

                right++;
            }

            // valid window found
            if(isDesirable(mapS,mapT)
                    && min > right-i){

                result=s.substring(i,right);

                min=right-i;
            }

            // shrink left
            mapS[s.charAt(i)]--;
        }

        return result;
    }

    private boolean isDesirable(
            int[] mapS,
            int[] mapT
    ){

        for(int i=0;i<256;i++){

            if(mapT[i]>mapS[i])
                return false;
        }

        return true;
    }
}
```

---

## Dry Run

Input:

```text
s = "ADOBECODEBANC"
t = "ABC"
```

Frequency of `t`:

```text
A=1
B=1
C=1
```

Window expansion:

```text
A
AD
ADO
ADOB
ADOBE
ADOBEC
```

Current window:

```text
ADOBEC
```

Valid:

```text
A=1
B=1
C=1
```

Length:

```text
6
```

Update:

```text
result="ADOBEC"
```

Shrink:

Remove:

```text
A
```

Window invalid.

Continue expanding:

```text
DOBECODEBA
```

Still valid.

Continue shrinking.

Eventually:

```text
BANC
```

Length:

```text
4
```

Update:

```text
result="BANC"
```

Final answer:

```text
"BANC"
```

---

## Why isDesirable() works

For every character:

```java
if(mapT[i] > mapS[i])
```

If required frequency is greater than current frequency:

```text
Need:
A=1

Current:
A=0
```

Window is invalid.

Otherwise:

```text
Current window covers all required characters
```

---

## Time Complexity

`isDesirable()` scans:

```text
256 characters
```

for every iteration.

Time:

```text
O(256 × n)
```

Approximately:

```text
O(n)
```

---

## Space Complexity

```text
O(256)
```

Two frequency arrays are used.

---

## Key Learning

- Variable-size Sliding Window
- Frequency arrays for character counting
- Expand right pointer
- Shrink left pointer
- Validate window using frequency comparison
- Brute-force style sliding window
