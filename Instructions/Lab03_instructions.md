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

---

## Complete Solutions

### Task 1: `countdown()` - Complete Implementation

```python
def countdown(i: int) -> None:
    """
    Print countdown from i to 0.
    
    From Chapter 3 (page 45):
    Base case: i <= 0
    Recursive case: print i, then countdown(i-1)
    """
    # Base case: stop when i reaches 0 or below
    if i <= 0:
        print(0)
        return
    
    # Recursive case: print current number, then countdown from i-1
    print(i)
    countdown(i - 1)
```

**How it works:**
1. Base case: When `i <= 0`, print 0 and return (stop recursing)
2. Recursive case: Print the current value of `i`, then call `countdown(i - 1)`
3. Each call reduces `i` by 1 until we hit the base case

---

### Task 2: `fact()` - Complete Implementation

```python
def fact(x: int) -> int:
    """
    Calculate factorial of x recursively.
    
    From Chapter 3 (page 49):
    fact(5) = 5 * 4 * 3 * 2 * 1 = 120
    
    Base case: x == 1, return 1
    Recursive case: x * fact(x-1)
    """
    # Base case: factorial of 1 is 1
    if x == 1:
        return 1
    
    # Recursive case: x * factorial of (x-1)
    return x * fact(x - 1)
```

**How it works:**
1. Base case: `fact(1) = 1`
2. Recursive case: `fact(x) = x * fact(x-1)`
3. Example trace:
   - `fact(5)` = `5 * fact(4)` = `5 * 4 * fact(3)` = `5 * 4 * 3 * fact(2)` = `5 * 4 * 3 * 2 * fact(1)` = `5 * 4 * 3 * 2 * 1` = `120`

---

### Task 3: `recursive_sum()` - Complete Implementation

```python
def recursive_sum(arr: List[int]) -> int:
    """
    Sum all elements in array recursively.
    
    Base case: empty array, return 0
    Recursive case: first element + sum of rest
    """
    # Base case: empty array has sum of 0
    if len(arr) == 0:
        return 0
    
    # Recursive case: first element + sum of the rest
    return arr[0] + recursive_sum(arr[1:])
```

**How it works:**
1. Base case: Empty array `[]` returns `0`
2. Recursive case: Take the first element `arr[0]` and add it to the sum of the rest `arr[1:]`
3. Example trace:
   - `recursive_sum([2, 4, 6])` = `2 + recursive_sum([4, 6])` = `2 + 4 + recursive_sum([6])` = `2 + 4 + 6 + recursive_sum([])` = `2 + 4 + 6 + 0` = `12`

---

### Task 4: `recursive_count()` - Complete Implementation

```python
def recursive_count(arr: List) -> int:
    """
    Count elements in array recursively.
    
    Base case: empty array, return 0
    Recursive case: 1 + count of rest
    """
    # Base case: empty array has 0 elements
    if len(arr) == 0:
        return 0
    
    # Recursive case: 1 (for current element) + count of the rest
    return 1 + recursive_count(arr[1:])
```

**How it works:**
1. Base case: Empty array `[]` returns `0`
2. Recursive case: Count 1 for the first element, plus the count of the rest
3. Example trace:
   - `recursive_count([a, b, c])` = `1 + recursive_count([b, c])` = `1 + 1 + recursive_count([c])` = `1 + 1 + 1 + recursive_count([])` = `1 + 1 + 1 + 0` = `3`

---

### Task 5: `recursive_max()` - Complete Implementation

```python
def recursive_max(arr: List[int]) -> int:
    """
    Find maximum element recursively.
    
    Base case: single element, return it
    Recursive case: max of (first, max of rest)
    """
    # Base case: single element is the max
    if len(arr) == 1:
        return arr[0]
    
    # Base case: two elements, return the larger one
    if len(arr) == 2:
        return arr[0] if arr[0] > arr[1] else arr[1]
    
    # Recursive case: compare first element with max of the rest
    sub_max = recursive_max(arr[1:])
    return arr[0] if arr[0] > sub_max else sub_max
```

**How it works:**
1. Base case 1: Single element array - that element is the max
2. Base case 2: Two elements - return the larger one
3. Recursive case: Find the max of the rest of the array, then compare with the first element
4. Example trace:
   - `recursive_max([3, 7, 2])` → compare `3` with `recursive_max([7, 2])` → compare `3` with `7` → return `7`

---

## Example Usage

```python
# Countdown
>>> countdown(5)
5
4
3
2
1
0

# Factorial
>>> fact(5)
120

>>> fact(3)
6

# Recursive sum
>>> recursive_sum([2, 4, 6])
12

>>> recursive_sum([])
0

# Recursive count
>>> recursive_count([1, 2, 3, 4, 5])
5

# Recursive max
>>> recursive_max([3, 7, 2, 9, 1])
9

>>> recursive_max([42])
42
```

---

## Testing
```bash
python -m pytest tests/ -v
```

## Submission
Commit and push your completed `recursion.py` file.
