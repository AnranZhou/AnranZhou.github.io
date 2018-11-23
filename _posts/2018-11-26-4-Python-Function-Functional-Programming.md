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

* filter

* sorted

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


#### 2.5 partial function


