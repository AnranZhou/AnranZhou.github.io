---
title: "[Python] 3. Advanced Features"
date: '2018-11-26 12:30:00'
layout: post
tag:
- Python
category: blog
author: Anran Zhou
---
## Advanced Features
Why do we need the pythonic features?

In python, the less the better.

### 1. Slice
Obtain elements in the container. Slice is more concise than for-loop.
```Python
    # all elements. L[:]
    # every 2. L[::2]
    L = [1, 2, 3, 4, 5] # [1, 3, 5]
```

### 2. List Comprehensions
* Avoid loop.
* Powerful.
* Waste of Memory(why?).

    ```Python
        # basic. 1 - 10.
        L = list(range(11))
        L = [x for x in range(11)]

        # 1^2, 2^2, 3^2, ...
        L = [ x^2 for x in range(11)]

        # 1^2, 3^2, ...
        L = [ x^2 for x in range(11) if x % 2]

        # permutation
        L = [ m+n for m in "abc" for n in "xyz"]

        # dict
        L = [k for k in d]
        L = [v for v in d.values()]
        L = [ k + '=' + v for k, v in d.items()]

        # all files and folders under current folder
        [d for d in os.listdir('.')]

        # all upper letters into lower letters
        [e.lower() for e in L if isinstance(e, str) ]
    ```

### 3. Iteration
* Iterable?
    ```Pythoon
    from collections import Iterable
    isinstance("abc", Iterable)
    isinstance([1, 2, 3, 4], Iterable)
    isinstance(1234, Iterable)
    ```

* enumerate
    ```Python
        # Zero-based enumerate
        for k, v in enumerate(['a', 'b', 'c', 'd'])
            print(k, v)
    ```

### 4. Generator
* Generator vs. List Comprehension
    * List Comprehensions calculate all elements
    * Generators only store the algorithm

* Define a Generator
```Python
    # Method 1: ()
    g1 = (x for x in range(2))

    # Method 2: yield
    def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'

    # call next() to execute a generator
    next(g1)    # 0
    next(g1)    # 1
    next(g1)    # StopIteration
```
* Generator vs. Function
    * Functions execute in sequence.
    * Generators execute when calling `next()` function and block in the position of yield.

### 5. Iterator
* Iterable vs. Iterator
    * Iterable can be used to do iteration
    * Iterator can not only be used to do iteration, but can call next().
* why are str, list, dict iteratble not iterator?
    * Iterator -> don't know the size at first
* Build a Iterator `iter()`
* Example:
    ```Python
        g = (x for x in range(11))
        while True:
            try:
                x = next(g)
                print(x)
            except StopIteration as e:
                print("error values: ", e.values)
                break
    ```
    