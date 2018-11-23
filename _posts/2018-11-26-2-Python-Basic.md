---
title: "[Python] 2. Basic"
date: '2018-11-26 11:00:00'
layout: post
tag:
- Python
- data type
- variable
- statement
category: blog
author: Anran Zhou
---

## Python Basics
* indenting code(4 blank spaces)
	* using colon (:) to mark code blocks
	* tab != blank space
	
* unchangable objects
	* there are some objects in Python cannot be changed. 


### 1. Data Types and Variables / Const
#### 1.1 Date Types
* special type
	* None
* arithmetic types
	* integral
		* boolean(True / False)
		* integer(0,0x, ...)
	* floating point numbers
		* / vs. //
* Compound types
	* string
		* normal
			* single quote. `'strings'`
			* double quotes. `"strings"`
		* raw string
			* `r'raw strings without translation'`
		* multi-lines strings
			* `""" we can write multiple lines here. """`

#### 1.2 Variables
* Identifiers(letters, numbers and underscore)
* Vairables in Python are references to an object in the memory.
* Dynamic type languages
	* The data type of a variable can be changed during the running.

#### 1.3 Const
* All capital characters to represent a const.
* Python doesn't have the procedure to protect the value of a const not being changed.


### 2. String and char encoding 
#### 2.1 Character Encodings

|Encoding Methods|Bytes|
|:---:|:---:|
|ASCII|1 bytes|
|Unicode|2 bytes|
|UTF-8|1 bytes - 2 bytes|

* Python uses Unicode to encode defaultly.
* ASCII: 	
	* 65 - 90 : 'A' -'Z' 
	* 97 - 122 : 'a' -'z'

#### 2.2 Encoding & Decoding Conversion
* Strings to Bytes and vice-versa

	```Python
		# encode
		"abc".encode('ascii')
		"abc".encode('utf-8')
		
		# decode
		b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
		b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8', errors='ignore')
	```
	
* char to int and vice-versa
	* ord()
	* chr()

#### 2.3 Python Strings
* length of a string
* format output
	* %
	* format function
* upper() and lower()

* Examples
	```Python
		str  = "abc"
		len(str)
		
		print('%2d-%02d' % (3, 1))
		print("Hello {0}: {1:.1f}".format('anran', 17.125))
		
		print(str.upper())
		print(str.lower())
	```

### 3. built-in data structures
#### 3.1 list(Array in Python)
* The elements in the lists can have diff data types.
* list of lists can be used to represent two dimensional array.
* Operations:
	```Python
		list_a = ['first']
		# add
		list_a.append('apppend')
		list_a.insert(0, 'insert')

		# del
		list_a.pop()
		list_a.pop(1)

		# change
		list_a[0] = 'change'

		# retrieve
		# retrieve an element
		list_a[0]
		list_a[-1]

		# retrieve all elements
		list_a[:]
		list_a[:-1]
	```


#### 3.2 tuple
tuple is a const list.
* The elements in a tuple cannot be changed. 
* How to define a tuple with only one element? (1,)

#### 3.3 set(hashset in Python)
* Definition
	* directly
		`s = {1, 2, 3}`
	* Using list
		`s = set([1, 2, 3])`
* No duplicate elements in the set
* Operations:
	```Python
	s = set()

	# basic operations
	s.add("key")
	s.remove("key")
	if key in s:
		print(key, "in the set s")

	# logical operations
	s1 = {1, 2}
	s2 = {2, 3}
	s1 & s2	# {2}
	s1 | s2 # {1, 2, 3}
	s1 ^ s2 # {1, 3}
	```

#### 3.4 dict(hashmap in Python)
key in dict should be the unrevised type(like: string, int).
* Operations
	```Python
		score = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
		# basic operations
		# add
		score['anran'] = 100
		# revise
		score['anran'] = 99
		# delete
		score.pop('anran')
		# search key
		if key in score:
			print("key", key, "in the dict score.")
		# search value
		score.get('anran', -1)
	```

### 4. Flow Control
#### 4.1 conditional statement
```Python
	if <condition1>:
		pass
	elif <condition2>:
		pass
	elif <condition3>:
		pass
	else:
		pass
```
#### 4.2 iterative statement
* `for` loop
Using `range` to generate numbers:
```Python
	sum = 0
	for x in range(101):
		sum = sum + x
	print(sum)
```

* `while` loop
```Python
	sum = 0
	n = 0
	while n < 100:
	    n = n + 1
	    if n % 2 == 0: # 如果n是偶数，执行continue语句
	        continue # continue语句会直接继续下一轮循环，后续的print()语句不会执行
	    sum += n
	print(sum)
```

`break` and `continue` can be used in the iterative statements.
 