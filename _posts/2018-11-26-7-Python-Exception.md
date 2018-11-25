---
title: "[Python] 7. Exceptions"
date: '2018-11-26 16:30:00'
layout: post
tag:
- Python
category: blog
author: Anran Zhou
---
## Exception and Testing
* Errors in Programming
    * Bugs
    * Invalid User Operations(Invalid input)
    * Unpredictable Errors.(Full disks, Network Disconnection)

* Solutions
    * Debug
    * Exception Handling
    * Software Testing

### 1. Debug
#### 1.1 print
Print variables with problems.

* cons
    * Delete `print` statement after debugging.
    * The outcome of programs contains irrelative infos.

#### 1.2 assert
```Python
    def foo(s):
    n = int(s)
    assert n != 0, 'n is zero!'
    return 10 / n

    def main():
        foo('0')
```

* pros:
    * assert can throw errors.
    * assert can be ignored by using `python -O xxx.py`. Then `assert` statements are treated as `pass`.
* cons:
    * cons as `print`.

#### 1.3 logging
* 4 levels
    * info
    * debug
    * warning
    * error
* set level after import
    ```Python
        import logging
        logging.basicConfig(level=logging.INFO)
        
        ...
        logging.info('n = %d' % n)
        logging.debug('n = %d' % n)
        ...
    ```
* pros:
    * can redirect infos into consoles and files.
    * One revise to change the output. No need to delete codes.

#### 1.4 pdb
* single-step debug
    
    `python -m pdb err.py`

    |command|effect|
    |:---:|:---:|
    |1|show codes|
    |n|next line|
    |c|execute until break|
    |p \<var\>| show var's value|
    |q|exit|

* set trace
    ```Python
        import pdb

        ...
        pdb.set_trace()
        ...
    ```

    The program will execute until the line of pdb.set_trace().

#### 1.5 IDE
Using the tools provided by IDE to debug.


### 2. Error Handling
* Error Code

    If we met an error, return an error code(like -1) to indicate it.
    * cons
        * added many codes
        * pass error codes until the error handling functions

* Built-in Error
    * Python's errors are classes.

* try ... except ... finally
    ```Python
        try:
            print('try...')
            r = 10 / int('2')
            print('result:', r)
        except ValueError as e:
            print('ValueError:', e)
        except ZeroDivisionError as e:
            print('ZeroDivisionError:', e)
        else:
            print('no error!')
        finally:
            print('finally...')
        print('END')
    ```
* Raise Errors
    ```Python

    # raise errors in programs and throw it to the upper functions
    def foo(s):
        n = int(s)
        if n==0:
            raise ValueError('invalid value: %s' % s)
        return 10 / n

    def bar():
        try:
            foo('0')
        except ValueError as e:
            print('ValueError!')
            raise

    bar()


    # we can change the error msg when throw it to upper functions
    try:
        10 / 0
    except ZeroDivisionError:
        raise ValueError('input error!')
    ```

### 3. Testing
#### 3.1 Unit Testing
Suppose we have a python class like below:
```Python
# my_dict.py
class Dict(dict):

    def __init__(self, **kw):
        super().__init__(**kw)

    def __getattr__(self, key):
        try:
            return self[key]
        except KeyError:
            raise AttributeError(r"'Dict' object has no attribute '%s'" % key)

    def __setattr__(self, key, value):
        self[key] = value
```
We can write the unit test like below：
```Python
# mydict_test.py
import unittest
from mydict import Dict

class TestDict(unittest.TestCase):

    def setUp(self):
        print('setUp...')

    def tearDown(self):
        print('tearDown...')

    def test_init(self):
        d = Dict(a=1, b='test')
        self.assertEqual(d.a, 1)
        self.assertEqual(d.b, 'test')
        self.assertTrue(isinstance(d, dict))

    def test_key(self):
        d = Dict()
        d['key'] = 'value'
        self.assertEqual(d.key, 'value')

    def test_attr(self):
        d = Dict()
        d.key = 'value'
        self.assertTrue('key' in d)
        self.assertEqual(d['key'], 'value')

    def test_keyerror(self):
        d = Dict()
        with self.assertRaises(KeyError):
            value = d['empty']

    def test_attrerror(self):
        d = Dict()
        with self.assertRaises(AttributeError):
            value = d.empty
    
    if __name__ == '__main__':
        unittest.main()
```

* Import `unittest` if we want to use unittest. The test class should be inherited from `unittest.TestCase`.
* Test Method should be in the form of `test_xxx()`
* There are two ways to run unittests 
    * `python mydict_test.py`
    * `python -m unittest mydict_test`

#### 3.2 Doc Testing
pros:
* Testing
* Code Samples  

```Python
# mydict2.py
class Dict(dict):
    '''
    Simple dict but also support access as x.y style.

    >>> d1 = Dict()
    >>> d1['x'] = 100
    >>> d1.x
    100
    >>> d1.y = 200
    >>> d1['y']
    200
    >>> d2 = Dict(a=1, b=2, c='3')
    >>> d2.c
    '3'
    >>> d2['empty']
    Traceback (most recent call last):
        ...
    KeyError: 'empty'
    >>> d2.empty
    Traceback (most recent call last):
        ...
    AttributeError: 'Dict' object has no attribute 'empty'
    '''
    def __init__(self, **kw):
        super(Dict, self).__init__(**kw)

    def __getattr__(self, key):
        try:
            return self[key]
        except KeyError:
            raise AttributeError(r"'Dict' object has no attribute '%s'" % key)

    def __setattr__(self, key, value):
        self[key] = value

if __name__=='__main__':
    import doctest
    doctest.testmod()
```
