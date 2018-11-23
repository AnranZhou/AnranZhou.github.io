---
title: "[Python] 5. modules"
date: '2018-11-26 14:30:00'
layout: post
tag:
- Python
category: blog
author: Anran Zhou
---
## Module
* why do we use module?
    * maintance
    * namespace

* Package & Module
    * a normal folder contains the file `__init__.py` is a package.
    * a `.py` file is a module.
    * module with Package can distinguish the modules with the same name.

### 1. Define a module
```python3
    #! /user/bin/env python
    # -*- coding: utf-8 -*-

    ' this is the comments'

    __author__ = 'Anran'

    import sys

    def test():
        args = sys.argv
        if len(args)==1:
            print('Hello, world!')
        elif len(args)==2:
            print('Hello, %s!' % args[1])
        else:
            print('Too many arguments!')

    if __name__=='__main__':
        test()    
```

### 2. Use a module
* import module_name
* import module_name.member_name
* from module_name import *

If the import module is not found, it will raise an `ImportError` error.

### 3. Scope
* Public, Private and Special Use

    |Types|Notation|Examples|
    |:---:|:---:|:---:|
    |Public|normal|name|
    |Private|\_\<name> / _\_\<name>|\_id / \_\_id|
    |Special|\_\_\<name>\_\_|\_\_author\_\_ / \_\_name\_\_ / \_\_doc\_\_|

