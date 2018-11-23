---
title: "[C++] 4. Expressions"
date: '2018-11-21 13:24:00'
layout: post
tag:
- C++
- expression
- operator
category: blog
author: Anran Zhou
---

# Expressions
An expression is composed of one or more `operands` and yields a `result` when it is evaluated.
* Examples
	* simplest
		* expression: literal or variable
		* result: the value of literal and variable
	* more complicated
		* expression: an operator and one or more operands.
		* result: the value of expression
* Evaluation of an expression
	* operators
	* operands
	* the precedence of operators
	
## 1. Fundamentals
### 1.1 Basic Concepts
* Divide operators based on the number of operands
	* unary operators -- one operand
		* address-of (&) 
		* dereference (*)
	* binary operators -- two operands
		* equality (==)  
		* multiplication (*)
	* ternary operators -- three operands
	* unlimited -- unlimited operands

#### 1.1.1 Grouping Operators and Operands
Understanding expressions with multiple operators requires understanding the `precedence` and `associativity` of the operators and may depend on the order of evaluation of the operands.

`5 + 10 * 20/2;`

#### 1.1.2 Operand Conversions
As part of evaluating an expression, operands are often converted from one type to another.

`small int(bool, char, short) -> int`

`int -> float`

#### 1.1.3 Overloaded Operators
We can define what most operators mean when applied to class types.
* we can change the type and result
* we cannot change the number and precedence, associativity.

#### 1.1.4 Lvalues and Rvalues
Every expression in C++ is either an rvalue (pronounced “are-value”) or an lvalue (pronounced “ell-value”).
* Roughly speaking, when we use an object as an rvalue, we use the object’s value (its contents). When we use an object as an lvalue, we use the object’s identity (its location in memory).
* we can use an lvalue when an rvalue is required, but we cannot use an rvalue when an lvalue (i.e., a location) is required.

### 1.2 Precedence and Associativity
#### 1.2.1 Parentheses Override Precedence and Associativity


#### 1.2.2 When Precedence and Associativity Matter


### 1.3 Order of Evaluation
#### 1.3.1 Order of Evaluation, Precedence, and Associativity


#### 1.3.2 Advice: Managing Compound Expressions



## 2. Arithmetic Operators

## 3. Logical and Relational Operators

## 4. Assignment Operators

## 5. Increment and Decrement Operators

## 6. The Member Access Operators

## 7. The Conditional Operators

## 8. The Bitwise Operators

## 9. The sizeof Operators

## 10. Comma Operator

## 11. Type Conversions
### 11.1 Implicit Conversion

### 11.2 Explicit Conversion

## 12. Operator Precedence Table