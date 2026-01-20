# Lab 3: Recursion

## 1. Introduction and Objectives

### Overview
Explore recursion through classic examples: factorial, countdown, and sum. Understand the call stack and how to identify base cases vs recursive cases.

### Learning Objectives
- Understand recursion and the call stack
- Identify base case and recursive case
- Implement recursive functions
- Trace recursive calls mentally

### Prerequisites
- Complete Labs 1-2
- Read Chapter 3 in "Grokking Algorithms" (pages 41-54)

---

## 2. Algorithm Background

### Recursion Components
1. **Base Case** - When to stop (prevents infinite recursion)
2. **Recursive Case** - Function calls itself with smaller input

### The Call Stack
Each function call adds a frame to the stack:
```
factorial(3)
  → factorial(2)
      → factorial(1)
          → returns 1
      → returns 2 * 1 = 2
  → returns 3 * 2 = 6
```

---

## 3. Project Structure

```
lab03_recursion/
├── recursion.py   # Recursive function implementations
├── main.py        # Main program with demonstrations
└── README.md      # Your lab report
```

---

## 4. Step-by-Step Implementation

### Step 1: Create `recursion.py`

```python
"""
Lab 3: Recursion Examples
Demonstrates recursive functions and call stack behavior.

From Chapter 3: Every recursive function has two cases:
1. Base case - when the function doesn't call itself again
2. Recursive case - when the function calls itself
"""
from typing import List


# ============================================
# EXAMPLE FROM CHAPTER 3: Countdown
# ============================================
def countdown(i: int) -> None:
    """
    Countdown from i to 0.
    
    From Chapter 3 (page 45):
    def countdown(i):
        print(i)
        if i <= 0:    # Base case
            return
        else:         # Recursive case
            countdown(i-1)
    """
    print(i)
    if i <= 0:      # Base case
        return
    else:           # Recursive case
        countdown(i - 1)


# ============================================
# EXAMPLE FROM CHAPTER 3: Call Stack Demo
# ============================================
def greet(name: str) -> None:
    """
    Demonstrates the call stack.
    
    From Chapter 3 (page 47):
    This function calls greet2 and bye to show
    how the call stack works.
    """
    print(f"hello, {name}!")
    greet2(name)
    print("getting ready to say bye...")
    bye()


def greet2(name: str) -> None:
    """Called by greet()."""
    print(f"how are you, {name}?")


def bye() -> None:
    """Called by greet()."""
    print("ok bye!")


# ============================================
# EXAMPLE FROM CHAPTER 3: Factorial
# ============================================
def fact(x: int) -> int:
    """
    Calculate factorial recursively.
    
    From Chapter 3 (page 49):
    def fact(x):
        if x == 1:
            return 1
        else:
            return x * fact(x-1)
    """
    if x == 1:      # Base case
        return 1
    else:           # Recursive case
        return x * fact(x - 1)


# ============================================
# Verbose version to show call stack
# ============================================
def _indent(depth: int) -> str:
    return "  " * depth


def countdown_verbose(n: int, depth: int = 0) -> None:
    """Countdown with call stack visualization."""
    print(f"{_indent(depth)}countdown({n})")
    
    if n <= 0:
        print(f"{_indent(depth)}Base case reached! Returning...")
        return
    
    print(f"{_indent(depth)}→ {n}")
    countdown_verbose(n - 1, depth + 1)
    print(f"{_indent(depth)}← returning from countdown({n})")


def factorial(n: int, depth: int = 0) -> int:
    """
    Calculate n! recursively.
    
    Base case: n <= 1, return 1
    Recursive case: n * factorial(n-1)
    
    Time Complexity: O(n)
    Space Complexity: O(n) - call stack depth
    """
    print(f"{_indent(depth)}factorial({n})")
    
    # Base case
    if n <= 1:
        print(f"{_indent(depth)}Base case: returning 1")
        return 1
    
    # Recursive case
    result = n * factorial(n - 1, depth + 1)
    print(f"{_indent(depth)}Returning {n} * ... = {result}")
    return result


def recursive_sum(arr: List[int], depth: int = 0) -> int:
    """
    Sum a list recursively.
    
    Base case: empty list, return 0
    Recursive case: first element + sum of rest
    
    This is the "divide and conquer" pattern!
    """
    print(f"{_indent(depth)}sum({arr})")
    
    # Base case
    if len(arr) == 0:
        print(f"{_indent(depth)}Base case (empty): returning 0")
        return 0
    
    # Recursive case: first + sum(rest)
    first = arr[0]
    rest = arr[1:]
    rest_sum = recursive_sum(rest, depth + 1)
    result = first + rest_sum
    print(f"{_indent(depth)}Returning {first} + {rest_sum} = {result}")
    return result


def recursive_count(arr: List, depth: int = 0) -> int:
    """
    Count items in a list recursively.
    
    Base case: empty list, return 0
    Recursive case: 1 + count of rest
    """
    print(f"{_indent(depth)}count({arr})")
    
    if len(arr) == 0:
        print(f"{_indent(depth)}Base case: returning 0")
        return 0
    
    result = 1 + recursive_count(arr[1:], depth + 1)
    print(f"{_indent(depth)}Returning 1 + ... = {result}")
    return result


def recursive_max(arr: List[int], depth: int = 0) -> int:
    """
    Find maximum in a list recursively.
    
    Base case: single element, return it
    Recursive case: max of (first, max of rest)
    """
    print(f"{_indent(depth)}max({arr})")
    
    # Base case: single element
    if len(arr) == 1:
        print(f"{_indent(depth)}Base case: returning {arr[0]}")
        return arr[0]
    
    # Recursive case
    first = arr[0]
    max_of_rest = recursive_max(arr[1:], depth + 1)
    result = first if first > max_of_rest else max_of_rest
    print(f"{_indent(depth)}max({first}, {max_of_rest}) = {result}")
    return result


def fibonacci(n: int, depth: int = 0) -> int:
    """
    Calculate nth Fibonacci number recursively.
    
    WARNING: This is O(2^n) - very inefficient!
    We'll optimize this with dynamic programming in Lab 11.
    
    Base case: n <= 1, return n
    Recursive case: fib(n-1) + fib(n-2)
    """
    print(f"{_indent(depth)}fib({n})")
    
    # Base case
    if n <= 1:
        return n
    
    # Recursive case (inefficient - repeated calculations!)
    return fibonacci(n - 1, depth + 1) + fibonacci(n - 2, depth + 1)
```

### Step 2: Create `main.py`

```python
"""
Lab 3: Main Program
Demonstrates recursion with various examples from Chapter 3.
"""
from recursion import (
    countdown, greet, fact, countdown_verbose,
    factorial, recursive_sum, recursive_count, recursive_max
)


def main():
    # =========================================
    # EXAMPLE 1: Call Stack (from Chapter 3)
    # =========================================
    print("=" * 60)
    print("EXAMPLE 1: THE CALL STACK (Chapter 3, page 47)")
    print("=" * 60)
    print("\nCalling greet('maggie'):")
    print("-" * 40)
    greet("maggie")
    print("""
    Call stack visualization:
    
    1. greet("maggie") is called
       [greet: name="maggie"]
       
    2. greet calls greet2("maggie")
       [greet2: name="maggie"]
       [greet: name="maggie"]
       
    3. greet2 returns, popped off stack
       [greet: name="maggie"]
       
    4. greet calls bye()
       [bye]
       [greet: name="maggie"]
       
    5. bye returns, greet returns
       [empty]
    """)
    
    # =========================================
    # EXAMPLE 2: Countdown
    # =========================================
    print("\n" + "=" * 60)
    print("EXAMPLE 2: COUNTDOWN (Chapter 3, page 45)")
    print("=" * 60)
    print("\nSimple countdown from 3:")
    countdown(3)
    
    # =========================================
    # EXAMPLE 3: Factorial (from Chapter 3)
    # =========================================
    print("\n" + "=" * 60)
    print("EXAMPLE 3: FACTORIAL (Chapter 3, page 49)")
    print("=" * 60)
    print("\nCalculating fact(3):")
    print("-" * 40)
    result = fact(3)
    print(f"\nfact(3) = {result}")
    
    print("""
    Call stack for fact(3):
    
    fact(3): x=3, returns 3 * fact(2)
      fact(2): x=2, returns 2 * fact(1)
        fact(1): x=1, returns 1  ← Base case!
      fact(2): returns 2 * 1 = 2
    fact(3): returns 3 * 2 = 6
    """)
    
    # =========================================
    # EXAMPLE 4: Factorial with visualization
    # =========================================
    print("\n" + "=" * 60)
    print("EXAMPLE 4: FACTORIAL WITH CALL STACK TRACE")
    print("=" * 60)
    print("\nCalculating 5! (5 factorial):")
    result = factorial(5)
    print(f"\n5! = {result}")
    
    # =========================================
    # EXAMPLE 3: Recursive Sum
    # =========================================
    print("\n" + "=" * 60)
    print("EXAMPLE 3: RECURSIVE SUM")
    print("=" * 60)
    numbers = [2, 4, 6]
    print(f"\nSumming {numbers}:")
    result = recursive_sum(numbers)
    print(f"\nSum = {result}")
    
    # =========================================
    # EXAMPLE 4: Recursive Count
    # =========================================
    print("\n" + "=" * 60)
    print("EXAMPLE 4: RECURSIVE COUNT")
    print("=" * 60)
    items = ['a', 'b', 'c', 'd']
    print(f"\nCounting {items}:")
    result = recursive_count(items)
    print(f"\nCount = {result}")
    
    # =========================================
    # EXAMPLE 5: Recursive Max
    # =========================================
    print("\n" + "=" * 60)
    print("EXAMPLE 5: RECURSIVE MAX")
    print("=" * 60)
    numbers = [3, 7, 2, 9, 1]
    print(f"\nFinding max in {numbers}:")
    result = recursive_max(numbers)
    print(f"\nMax = {result}")
    
    # =========================================
    # EXAMPLE 6: Fibonacci (WARNING: Slow!)
    # =========================================
    print("\n" + "=" * 60)
    print("EXAMPLE 6: FIBONACCI")
    print("=" * 60)
    print("\nCalculating fib(6):")
    print("(Notice the repeated calculations!)")
    result = fibonacci(6)
    print(f"\nfib(6) = {result}")
    
    print("\n" + "-" * 40)
    print("Fibonacci sequence: ", end="")
    for i in range(10):
        # Don't print trace for this
        print(fib_simple(i), end=" ")
    print()
    
    # =========================================
    # SUMMARY
    # =========================================
    print("\n" + "=" * 60)
    print("KEY TAKEAWAYS")
    print("=" * 60)
    print("""
    1. Every recursive function needs:
       - Base case (when to stop)
       - Recursive case (call itself with smaller input)
    
    2. The call stack tracks each function call
       - Each call adds a "frame" to the stack
       - Returns pop frames off the stack
    
    3. Recursion can be elegant but watch out for:
       - Stack overflow (too many recursive calls)
       - Repeated calculations (like naive Fibonacci)
    
    4. Tail recursion can be optimized by some languages
       (Python doesn't optimize tail recursion)
    """)


def fib_simple(n: int) -> int:
    """Simple fibonacci without printing."""
    if n <= 1:
        return n
    return fib_simple(n - 1) + fib_simple(n - 2)


if __name__ == "__main__":
    main()
```

---

## 5. Expected Output (partial)

```
============================================================
EXAMPLE 1: COUNTDOWN
============================================================

Countdown from 3:
countdown(3)
→ 3
  countdown(2)
  → 2
    countdown(1)
    → 1
      countdown(0)
      Base case reached! Returning...
    ← returning from countdown(1)
  ← returning from countdown(2)
← returning from countdown(3)

============================================================
EXAMPLE 2: FACTORIAL
============================================================

Calculating 5! (5 factorial):
factorial(5)
  factorial(4)
    factorial(3)
      factorial(2)
        factorial(1)
        Base case: returning 1
      Returning 2 * ... = 2
    Returning 3 * ... = 6
  Returning 4 * ... = 24
Returning 5 * ... = 120

5! = 120
```

---

## 6. Lab Report Template

```markdown
# Lab 3: Recursion

## Student Information
- **Name:** [Your Name]
- **Date:** [Date]

## Recursion Concepts

### Two Parts of Every Recursive Function
1. **Base Case:** [Explain]
2. **Recursive Case:** [Explain]

### The Call Stack
[Explain how the call stack works with an example]

## Function Analysis

| Function | Base Case | Recursive Case | Time Complexity |
|----------|-----------|----------------|-----------------|
| countdown | n <= 0 | countdown(n-1) | O(n) |
| factorial | n <= 1 | n * factorial(n-1) | O(n) |
| sum | empty list | first + sum(rest) | O(n) |
| max | single item | max(first, max(rest)) | O(n) |
| fibonacci | n <= 1 | fib(n-1) + fib(n-2) | O(2^n) |

## Reflection Questions

1. What happens if you forget the base case?

2. Why is the naive Fibonacci implementation inefficient?

3. Draw the call stack for factorial(4).
```

---

## 7. Submission

1. Save all files in `lab03_recursion/`
2. Complete your lab README
3. Commit and push to GitHub
