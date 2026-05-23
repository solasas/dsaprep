# Decode String

## Problem Statement

Given an encoded string, return its decoded string.

Encoding rule:

```text
k[encoded_string]
```

Where:

- `k` = number of repetitions
- `encoded_string` = string inside brackets
- Nested patterns are allowed

Examples:

```text
Input: "3[a]2[bc]"
Output: "aaabcbc"

Input: "3[a2[c]]"
Output: "accaccacc"

Input: "2[abc]3[cd]ef"
Output: "abcabccdcdcdef"
```

---

# Intuition

Whenever we encounter:

```text
[
```

we are entering a **new nested level**.

Before entering:

- Save the current number
- Save the current string

When we encounter:

```text
]
```

we complete the current nested block.

We:

1. Pop repeat count
2. Pop previous string
3. Repeat current string
4. Append to previous string

---

# Data Structures Used

```java
Stack<Integer> numStack
Stack<String> strStack
```

### numStack

Stores repeat counts.

Example:

```text
3[a2[c]]
```

Stores:

```text
3
2
```

---

### strStack

Stores previously built strings.

Example:

```text
3[ab2[c]]
```

Stores:

```text
""
"ab"
```

---

# Algorithm

1. Traverse string character by character

2. If character is digit:

```java
num = num*10 + (ch-'0')
```

Used for multi-digit numbers:

```text
12[a]
100[bc]
```

---

3. If character is:

```text
[
```

Push current state:

```java
numStack.push(num);
strStack.push(curr);
```

Reset:

```java
num=0;
curr="";
```

---

4. If character is:

```text
]
```

Pop:

```java
repeat = numStack.pop()
prev = strStack.pop()
```

Build:

```java
prev + current repeated repeat times
```

---

5. Else:

Normal character

Add to current string:

```java
curr += ch
```

---

# Code

```java
class Solution {
    public String decodeString(String s) {

        Stack<Integer> numStack = new Stack<>();
        Stack<String> strStack = new Stack<>();

        String curr = "";
        int num = 0;

        for(int i=0;i<s.length();i++){

            char ch = s.charAt(i);

            if(Character.isDigit(ch)){

                num = num*10 + (ch-'0');
            }

            else if(ch=='['){

                numStack.push(num);
                strStack.push(curr);

                num = 0;
                curr = "";
            }

            else if(ch==']'){

                int repeat = numStack.pop();

                String prev = strStack.pop();

                StringBuilder sb = new StringBuilder(prev);

                for(int j=0;j<repeat;j++){
                    sb.append(curr);
                }

                curr = sb.toString();
            }

            else{

                curr += ch;
            }
        }

        return curr;
    }
}
```

---

# Dry Run

Input:

```text
3[ab2[c]]
```

---

Read:

```text
3
```

```text
num=3
```

---

Read:

```text
[
```

Push:

```text
numStack=[3]

strStack=[""]
```

Reset:

```text
curr=""
```

---

Read:

```text
a
b
```

```text
curr="ab"
```

---

Read:

```text
2
```

```text
num=2
```

---

Read:

```text
[
```

Push:

```text
numStack=[3,2]

strStack=["","ab"]
```

Reset:

```text
curr=""
```

---

Read:

```text
c
```

```text
curr="c"
```

---

Read:

```text
]
```

Pop:

```text
repeat=2

prev="ab"
```

Build:

```text
ab + cc
```

```text
curr="abcc"
```

---

Read:

```text
]
```

Pop:

```text
repeat=3

prev=""
```

Build:

```text
abccabccabcc
```

Output:

```text
abccabccabcc
```

---

# Why Previous Characters Are Not Lost

Before entering:

```text
[
```

we save:

```java
strStack.push(curr)
```

This stores all previously built characters.

Later:

```java
String prev = strStack.pop();

sb.append(prev);
sb.append(repeated current string);
```

Thus:

```text
previous text + decoded current text
```

gets merged correctly.

---

# Complexity

Time:

```text
O(n)
```

Space:

```text
O(n)
```

---

# Pattern Learned

Problems involving:

```text
Nested structures
Brackets
Repeat patterns
```

Usually suggest:

```text
Stack
```

Especially:

```text
Save state before entering
Restore state after leaving
```

Very important interview pattern.
