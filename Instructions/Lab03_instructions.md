# Lab 03: Recursion

## Overview
In this lab, you will implement several **recursive functions** from Chapter 3 of "Grokking Algorithms." Recursion is a fundamental concept where a function calls itself.

## Learning Objectives
- Understand the two parts of every recursive function: base case and recursive case
- Implement classic recursive algorithms
- Visualize the call stack
- Convert iterative thinking to recursive thinking

## Background

### The Two Cases
Every recursive function has:
1. **Base case**: When the function stops calling itself (prevents infinite recursion)
2. **Recursive case**: When the function calls itself with a smaller problem

### The Call Stack
Each recursive call adds a frame to the call stack. When the base case is reached, the stack "unwinds" as each call returns its result.

```
fact(3)
  → 3 * fact(2)
       → 2 * fact(1)
            → 1  (base case!)
       ← 2 * 1 = 2
  ← 3 * 2 = 6
```

## Your Tasks

### Task 1: Implement `countdown()`
Print numbers from `i` down to 0:
- Base case: `i <= 0` (stop)
- Recursive case: print `i`, then call `countdown(i-1)`

### Task 2: Implement `fact()`
Calculate factorial (n! = n × (n-1) × ... × 1):
- Base case: `x == 1` returns `1`
- Recursive case: `x * fact(x-1)`

### Task 3: Implement `recursive_sum()`
Sum all elements in an array:
- Base case: empty array returns `0`
- Recursive case: `first element + sum(rest of array)`

### Task 4: Implement `recursive_count()`
Count elements in an array:
- Base case: empty array returns `0`
- Recursive case: `1 + count(rest of array)`

### Task 5: Implement `recursive_max()`
Find the maximum element:
- Base case: single element returns that element
- Recursive case: `max(first, max(rest))`

## Examples

```python
>>> fact(5)
120  # 5 * 4 * 3 * 2 * 1

>>> recursive_sum([2, 4, 6])
12  # 2 + 4 + 6

>>> recursive_max([3, 7, 2, 9, 1])
9
```

## Testing
```bash
python -m pytest tests/ -v
```

## Hints
- Use array slicing: `arr[1:]` gives all elements except the first
- Use `arr[0]` to get the first element
- Always handle the empty array case!
- Python's `max()` function can compare two values: `max(a, b)`

## Submission
Commit and push your completed `recursion.py` file.
