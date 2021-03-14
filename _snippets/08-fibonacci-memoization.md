---
title: "Memoization and Recursion in Python"
permalink: /snippets/python-fibonacci-memo/
excerpt: "finding fib series using efficient memoization"
last_modified_at: 2021-02-05
tags:
 - python
 - algo
---

## let's try to program to find the nth fibonanci number

Here is an example to think about recursion and memoization in Python.

```python
def fib(n, memo = {0:0, 1:1}):
    if n in memo:
        return memo[n]
    memo[n] = fib(n - 1, memo) + fib(n - 2, memo)
    return memo[n]
```

When we run this function `fib()` with various values of n:

```python
fib(3), fib(4), fib(6)

>>> (2, 3, 8)
```

Now let's look at how long it takes to run this function for a realtively large value, 100:

```python
%%time 
fib(100)

>>> CPU times: user 0 ns, sys: 0 ns, total: 0 ns
>>> Wall time: 212 µs

>>> 354224848179261915075
```
