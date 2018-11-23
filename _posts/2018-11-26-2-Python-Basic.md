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
#### 3.1 list

#### 3.2 tuple

#### 3.3 dict

#### 3.4 set



### 4. Flow Control
#### 4.1 conditional statement



#### 4.2 iterative statement