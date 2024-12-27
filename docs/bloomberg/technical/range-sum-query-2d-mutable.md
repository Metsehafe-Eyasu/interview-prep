---
title: "Range Sum Query 2D: Mutable"
company: "Bloomberg"
category: "technical"
role: "internship" 
date: "2024-12-29"
---

# Range Sum Query 2D (Mutable)

> [LeetCode #308: Range Sum Query 2D - Mutable](https://github.com/doocs/leetcode/blob/main/solution/0300-0399/0308.Range%20Sum%20Query%202D%20-%20Mutable/README_EN.md)

## Question
You have a 2D matrix that supports:
1. **Update**: `update(row, col, val)` - Update an element at `(row, col)` to be `val`.
2. **Sum Region**: `sumRegion(row1, col1, row2, col2)` - Return the sum of the submatrix from `(row1, col1)` to `(row2, col2)` inclusive.

**Key Points**:
- We need efficient updates **and** sum queries.
- A naive approach (recomputing sums each time) would be too slow for large inputs.

## Possible Approaches
- **Fenwick Tree (Binary Indexed Tree)** for 2D
  - Build a 2D Fenwick tree to handle both updates and sum queries in approximately `O(log m * log n)`.
- **Segment Tree** for 2D
  - Similar complexity, but typically more complex to implement.
- **Comparison to Immutable (LeetCode #304)**:
  - #304 only required prefix sums since the matrix was immutable, but #308 needs a data structure that can handle updates.

## Example
```
Given a matrix:
[
  [3, 0, 1, 4],
  [5, 6, 3, 2],
  [1, 2, 0, 1],
  [4, 1, 0, 1]
]

update(2, 2, 2)  # Modify the element at row=2, col=2
sumRegion(2, 1, 4, 3) -> ?

// Use a Fenwick Tree or Segment Tree approach for both update and range-sum queries
```

## Edge Cases
- Updating the same cell multiple times in succession.
- Querying large submatrices repeatedly.
- Handling row/column indices near the boundaries of the matrix.