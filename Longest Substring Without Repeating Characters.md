# Longest Substring Without Repeating Characters

## Problem Statement

Given a string `s`, find the length of the longest substring without repeating characters.

A substring is a contiguous sequence of characters.

Return the length of the longest substring containing only unique characters.

---

## Approach: Sliding Window + HashSet

We use a variable-size sliding window.

Maintain:

- `left` → start of window
- `right` → end of window
- `HashSet<Character>` → stores characters currently in the window
- `maxLength` → stores longest valid substring length

### Steps

1. Expand window by moving `right`
2. If current character already exists:
   - Remove characters from left side
   - Continue until duplicate is removed
3. Add current character into set
4. Update maximum length

---

## Why HashSet works here

Unlike the previous subarray problem, we only need to know:

- whether a character exists
- not how many times it appears

Example:

```text
abcabcbb
```

Window:

```text
abc
```

Set:

```text
[a,b,c]
```

When next `a` comes:

```text
abca
```

Duplicate found.

Remove from left:

Remove 'a'

Window becomes:

```text
bca
```

Add new `a`

Window:

```text
bca
```

Continue.

---

## Java Solution

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {

        HashSet<Character> set = new HashSet<>();

        int left = 0;
        int maxLength = 0;

        for(int right=0; right<s.length(); right++){

            while(set.contains(s.charAt(right))){
                set.remove(s.charAt(left));
                left++;
            }

            set.add(s.charAt(right));

            maxLength = Math.max(
                    maxLength,
                    right-left+1
            );
        }

        return maxLength;
    }
}
```

---

## Dry Run

Input:

```text
s = "abcabcbb"
```

Step-by-step:

Window:

```text
a
```

length:

```text
1
```

Window:

```text
ab
```

length:

```text
2
```

Window:

```text
abc
```

length:

```text
3
```

Next character:

```text
a
```

Duplicate found.

Remove:

```text
a
```

Window becomes:

```text
bc
```

Add new `a`

Window:

```text
bca
```

Length:

```text
3
```

Continue similarly.

Final answer:

```text
3
```

---

## Time Complexity

```text
O(n)
```

Each character enters and leaves the window at most once.

---

## Space Complexity

```text
O(min(n, charset))
```

Set stores unique characters.

---

## Key Learning

- Variable-size Sliding Window
- Use HashSet for uniqueness checking
- Remove duplicates using while loop
- Expand and shrink dynamically
- Track maximum valid window size
