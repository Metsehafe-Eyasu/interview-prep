---
title: "Design Circular Queue"
company: "Bloomberg"
category: "technical"
role: "internship"
date: "2024-12-02"
---

# Design Circular Queue

> [LeetCode Problem: Design Circular Queue](https://leetcode.com/problems/design-circular-queue/)

## Question
We receive multiple customer requests in a tuple format (with customer info). We need a **fixed-size buffer** to store them and read them when needed. Essentially, implement a **circular queue** data structure.

**Operations**:
- `enQueue(value)`: Insert an element into the circular queue. Return `true` if successful.
- `deQueue()`: Delete an element. Return `true` if successful.
- `Front()`: Get the front item.
- `Rear()`: Get the last item.
- `isEmpty()`: Checks whether the circular queue is empty.
- `isFull()`: Checks whether the circular queue is full.

**Constraints**:
- The queue is of fixed size.
- Must handle wrap-around indexing.

## Key Points
1. **Array Implementation**:
   - Use a size limit, plus two pointers (head, tail).
2. **Enqueue/Dequeue**:
   - If `isFull`, cannot insert.
   - If `isEmpty`, cannot remove.
3. **Time Complexity**:
   - Each operation in O(1).

## Example
- Capacity = 3
- `enQueue(1) -> true`  
- `enQueue(2) -> true`  
- `enQueue(3) -> true`  
- `enQueue(4) -> false` (queue is full)
- `Rear() -> 3`  
- `isFull() -> true`
- `deQueue() -> true`  
- `enQueue(4) -> true`
- `Rear() -> 4`