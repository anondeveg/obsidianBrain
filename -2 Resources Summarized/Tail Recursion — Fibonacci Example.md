**Date:** 2026-02-08 12:05  
**Source Material:** Personal Notes / Grokking Algorithms  
**Tags:** [[recursion]], [[tail-recursion]]

---

## Recursive Function Structure

Every recursive function has **two cases**:

1. **Base Case**: The function finally returns the result without calling itself.  
2. **Recursive Case**: The function calls itself.

Example for Fibonacci:

- Base case: `n <= 1`  
- Recursive case: `n > 1`  

---

## Basic Recursive Fibonacci

```cpp
#include <tuple>

int recursive_fibonacci(int n) {
    // Base case
    if (n <= 1)
        return n;

    // Recursive case
    return recursive_fibonacci(n - 1) + recursive_fibonacci(n - 2);
}
```

---

## Tail-Recursive Fibonacci

Differences from basic recursion:

- Base case: same as basic recursion  
- Recursive case: last step is **calling the function itself**, not combining returns  

Behavior:

- `fib(0, (a, b)) -> a`  
- `fib(1, (a, b)) -> b`  
- `fib(n, (a, b)) -> fib(n-1, (b, a+b))`  

Tail recursion **uses less memory** and is **generally more efficient** than normal recursion.

```cpp
int tail_recursive_fibonacci(int n, std::tuple<int, int> prev = {0, 1}) {
    if (n <= 0)
        return std::get<0>(prev);
    else if (n == 1)
        return std::get<1>(prev);

    return tail_recursive_fibonacci(
        n - 1, {std::get<1>(prev), std::get<0>(prev) + std::get<1>(prev)});
}
```

---

## References

- [ Tail Recursion Explained - Computerphile ](https://www.youtube.com/watch?v=_JtPhF8MshA)
- Personal Notes / Grokking Algorithms
