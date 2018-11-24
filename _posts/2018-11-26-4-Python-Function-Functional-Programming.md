---
title: "[Python] 4. Function and Functional Programming"
date: '2018-11-26 13:00:00'
layout: post
tag:
- Python
- Functional Programming
category: blog
author: Anran Zhou
---
## Function

### 1. Function Basics
* arguments vs. parameters
* arguments
    * format
        * Required arguments
        * Default arguments
            * default arguments should be the unchangable objects.
                * error avoid
                * don't need read/write locks 
            ```Python
                def add_end(L=None):
                    if L is None:
                        L = []
                    L.append('END')
                    return L
            ```
        * varied-size arguments
            ```Python
                def fun1(*args):
                    pass
                # call
                func1(1,2,3)
                func1(*[1,2,3])
            ```
        * keyword arguments
            ```Python
                def func2(**kw):
                    pass
                # call
                func2(**{'name': 'anran', 'age':18 })
            ```
        * limited keyword arguments
            ```Python
                # method 1
                def func3(name, *, city, job):
                    pass
                # call
                func3('anran', city="Raleigh", job="SDE")

                # method 2
                def func4(name, *args, city, job):
                    pass
            ```

    * arguments should be checked.
        ```Python
            if not isinstance(x, str):
                raise TypeError('bad operand types.')
        ```
    * all function calls can be accepted using: `def func(*args, **kw)`
* `pass` as the occupier
* `return` can be `None`. (no return == return None == return )
* `return` can return multiple values


### 2. Functional Programming
#### 2.1 Higher-order Function 
In higher-order functions, functions can be treated as a parameter.
* map/reduce

    Map and Reduce are built-in functions of Python.
    * Examples:
    ```Python
        # map
        # integer to strings
        L = map(str, [1, 2, 3]) # return a map object, list(L) == ['1', '2', '3']
        L = map(lambda x: x*x, [1, 2, 3]) # return a map object, list(L) == [1, 4, 9]
        

        # reduce
        from functools import reduce
        reduce(lambda x,y: x+y, [1, 2, 3]) # 1 + 2 + 3

        # str to int
        reduce(lambda x,y: x*10+y, map(lambda x: ord(x)-ord('0'), "12345"))
    ```

* filter
    ```Python
        def not_empty(s):
            return s and s.strip()

        list(filter(not_empty, ['A', '', 'B', None, 'C', '  ']))
        # 结果: ['A', 'B', 'C']
    ```

* sorted
    ```Python
    #！ /usr/bin/env python3
    # -*- coding: utf-8 -*-

    L = ['bob', 'about', 'Zoo', 'Credit']
    print(sorted(L))
    # self-defined comparators
    print(sorted(L, key=str.lower))

    from operator import itemgetter
    # sort complex data type
    students = [('Bob', 75), ('Adam', 92), ('Bart', 66), ('Lisa', 88)]
    print(sorted(students, key=itemgetter(0)))
    print(sorted(students, key=lambda t: t[1]))
    print(sorted(students, key=itemgetter(1), reverse=True))
    ```

#### 2.2 closure
* Definition
    * We can define functions inside a function
    * The inner functions can use the variables of the outter function
    * Those variables used by the inner function are keeped. 
    * This is closure.
* closure is like the class
    * Define variables in the outter function and use them in the inner functions.
    * inner functions created by calling outter functions have no relationship.
    * Inner funcitons of the same outter function share the vairables of that outter function.

#### 2.3 lambda function
Anonymous Function.
```Python
    # definition
    lambda x : x * x
```

#### 2.4 decorator
* why do we use decorator?
    
    execute functions before or after a certain function.


#### 2.5 partial function
We can bind some parameters of a function when it has too many parameters.
```Python
    from functools import partial
    int2 = partial(int, base=2)
    int2('1000000') # 64
```
