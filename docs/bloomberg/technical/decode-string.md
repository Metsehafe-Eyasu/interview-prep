---
title: "Decode String"
company: "Bloomberg"
category: "technical"
role: "new-grad"
date: "2024-11-29"
---

# Decode String

> [LeetCode Problem: Decode String](https://leetcode.com/problems/decode-string)

## Question

Given an encoded string, return its decoded string. The encoding rule is:

```
k[encoded_string]
```

where the `encoded_string` inside the brackets is repeated `k` times.

**Examples**:

- Input: `"3[a]2[bc]"` → Output: `"aaabcbc"`
- Input: `"3[a2[c]]"` → Output: `"accaccacc"`

## Key Points

1. **Stack-based Parsing**:
   - Typically use one or two stacks (one for counts, one for strings).
2. **Nested Encoding**:
   - Must handle multiple levels of brackets.
3. **Edge Cases**:
   - Empty brackets, large repetition counts, or invalid input strings (depending on constraints).

## Approach Outline

- Iterate over the string.
- Push partial strings or numbers onto stacks.
- When encountering a `']'`, pop and build the repeated substring.
