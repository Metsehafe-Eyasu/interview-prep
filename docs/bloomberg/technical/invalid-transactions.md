---
title: "Invalid Transactions (LeetCode)"
company: "Bloomberg"
category: "technical"
role: "internship"
date: "2024-11-27"
---

# Invalid Transactions

> [LeetCode Problem: Invalid Transactions](https://leetcode.com/problems/invalid-transactions/)

## Question

Given a list of transactions (name, time, amount, city), determine which are **invalid**. A transaction is invalid if:

1. The amount exceeds $1000, or
2. If there exists another transaction with the **same name** within 60 minutes (time difference ≤ 60) but in a **different city**.

You must **return** all invalid transactions as an array.

## Key Points

- **Parsing** each transaction string.
- **Comparison** logic for time windows and city differences.
- **Data Structures**: Possibly group by name and then sort by time to quickly compare.

## Additional Thoughts

- Watch for **duplicates**: if multiple transactions share the same criteria, each can be invalid.
- Efficiency considerations:
  - Possibly `O(n^2)` approach is feasible for typical constraints, or optimize with hashing + sorting.
