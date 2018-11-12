---
title: "[C++] Primitive built-in types"
date: '2018-11-11 19:25:24'
layout: post
tag:
- C++
- data type
category: blog
author: Anran Zhou
---

# C++ Primitive built-in types
## Data Type
data types tell us:
* the meaning of data
* the operations on those data.

### 1. Data Types Introduction
#### 1.1 two major built-in types

* arithemetic types
	* integral types 
		* boolean values(`bool`)
		* characters(`char`, `wchar_t`, `char16_t`, `char32_t`)
		* integers(`short`, `int`, `long`, `long long`)
			
	* floating-point types
		* floating-point numbers(`float`, `double`, `long double`)
		
* a special type -- `void`
	* no associative values
	* the return type for functions that do not return a value.	
		
#### 1.2 the size of different types
the size of data type depends on the machines.

#### 1.3 signed and unsigned
* Except for `bool` and the extended character types, the integral types may be signed or unsigned.
* `char ` is different from `integers`.
	* there are three types of `char`: `char`, `unsigned char` and `signed char`.
	* `char ` may represent `unsigned char` or `signed char`. It depends on machines.

#### 1.4 choice of different types
* first, clarify it's integer or floating-point number.
* if it's integer:
	* tiny -> unsigned char / signed char. (not char)
	* normal -> int
	* large -> long long
* if it's floating-point number:
	* double. (not float, nor long double)

### 2. Type Conversions
convert objects of the given type to other, related types.

---
Some experiences when assigning values:

|Types|Operations|Outcome|
|:---:|:---:|:---:|
|bool|nonbool arithmetic types to a bool object| 0 -> false ; 1 otherwise|
||bool to one of the other arithmetic types|false -> 0; true -> 1|
|float|floating-point value to an object of integral type|truncated|
||an integral value to an object of floating-point type|fractional part is zero; may lose precesion|
|unsigned|out-of-range value to an object of unsigned type|modulo|
|signed|out-of-range value to an object of signed type|undefined|

---

Some experience when doing arithmetic operations:
 * signed values are automatically converted to unsigned.


### 3. Literals
Every literal has a type. The form and value of a literal determine its type.
* Integer Literals
not `short` type.
	* decimal
		* signed by default
		* the value of a decimal literal is never a negative number. 

	* octal(0)
		* either signed or unsigned types.
		
	* hexadecimal(0x/0X)
		* either signed or unsigned types.
		
* Floating-Point literals
	* either a decimal point or an exponent specified using scientific notation
	* `double` by default. Override by using suffix.
	
* Character and Character String Literals
	* string literals == array of char literals + '\0'

* Escape Sequences
	An escape sequence begins with a backslash.

* Boolean and Pointer Literals
 *	True or False 
 *	nullptr

![](https://lh5.googleusercontent.com/f0efvvwuX9X4Xg2HGrDUKLVjqk74yOyXr8wV3_vEI2Y3MJtPBzGMdKul9xjpy2zF4OEwB1HP_t7Axa813PL1QAlVbSqbh6YXg7CN5H8vFTj9WOABdj0XWcnx3ddtg7ksp8IVSAC0)