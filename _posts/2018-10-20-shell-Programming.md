---
title: Shell Programming
layout: post
date: '2018-10-20 18:47:42'
tag:
- shell
category: blog
author: Anran Zhou
---

# Shell Programming
There are some references about shell programming:
* [Shell Scripting Tutorial](https://www.shellscript.sh/)
* [Shell Scripting Tutorial](https://www.tutorialspoint.com/unix/shell_scripting.htm)

## 1.  Variables
### 1.1 Variable Name
1. components: number + char + underscore
2. Unix shell variables will have their names in UPPERCASE

### 1.2 Variable Types

|Types|function|
|:---:|:---:|
|Local variable| only valid at the current shell|
|Environment variable|valid at any shells|
|Shell variable|can be either local or environment|

### 1.3 Variables Definition, Accessing, Deletion

{% highlight shell %}
// define a variable
NAME="Anran Zhou"

// access a variable
echo $NAME

// turn a variable as constant
readonly NAME

// delete a variable. unset can not delete a read only var.
unset NAME

{% endhighlight %}

### 1.4 Special Variables

|Variable Name| Function|
|:---:|:---|
|$0|The filename of the current script.|
|$n|the first argument is $1, the second argument is $2, and so on.|
|$#|The number of arguments supplied to a script.|
|$*|All the arguments are double quoted.|
|$@|All the arguments are individually double quoted.|
|$?|The exit status of the last command executed.|
|$$|The process number of the current shell. For shell scripts, this is the process ID under which they are executing.|
|$!|The process number of the last background command.|

### 1.5 Array Variable

{% highlight shell %}
// define an array
NAME=(value1 ... valuen)

// access an array variable
echo ${NAME[0]}

// access all the items in an array
echo ${NAME[*]}
echo ${NAME[@]}

{% endhighlight %}


## 2. Basic Operators
Bourne shell didn't originally have any mechanism to perform simple arithmetic operations but it uses external programs, either `awk` or `expr`.

Requirements: 
* There must be spaces between operators and expressions. 
* The complete expression should be enclosed between \`\` , called the backtick.

### 2.1 Arithmetic Operators
### 2.2 Relational Operators
### 2.3 Boolean Operators
### 2.4 String Operators
### 2.5 File Test Operators

[Operators](https://www.tutorialspoint.com/unix/unix-basic-operators.htm)


## 3. Conditional Statement
### 3.1 The if...else statements
1. if...fi statement
2. if...else...fi statement
3. if...elif...else...fi statement

{% highlight shell %}
// first
if [ expression ] 
then 
   Statement(s) to be executed if expression is true 
fi

// second
if [ expression ]
then
   Statement(s) to be executed if expression is true
else
   Statement(s) to be executed if expression is not true
fi

// third
if [ expression 1 ]
then
   Statement(s) to be executed if expression 1 is true
elif [ expression 2 ]
then
   Statement(s) to be executed if expression 2 is true
elif [ expression 3 ]
then
   Statement(s) to be executed if expression 3 is true
else
   Statement(s) to be executed if no expression is true
fi

{% endhighlight %}


### 3.2 The case...esac Statement
{% highlight shell %}
case word in
   pattern1)
      Statement(s) to be executed if pattern1 matches
      ;;
   pattern2)
      Statement(s) to be executed if pattern2 matches
      ;;
   pattern3)
      Statement(s) to be executed if pattern3 matches
      ;;
   *)
     Default condition to be executed
     ;;
esac
{% endhighlight %}


## 4. Loop in Shell
### 4.1 Basic loops
1. The `while` loop
2. The `for` loop
3. The `until` loop
4. The `select` loop

{% highlight shell %}
// while loop
while command
do
   Statement(s) to be executed if command is true
done

// for loop
for var in word1 word2 ... wordN
do
   Statement(s) to be executed for every word.
done

// until loop
until command
do
   Statement(s) to be executed until command is true
done

// select loop
select var in word1 word2 ... wordN
do
   Statement(s) to be executed for every word.
done

{% endhighlight %}

### 4.2 loop control
1. The break statement

	break n 
	
2. The continue statement

	continue n
	
## 5. Substitution
### 5.1 Command Substitution
Using the outcome of command to substitute the original command.  The format is: \`command\`.

### 5.2 Variable Substitution
The format is: "${var-name}".

|Form | Description|
|:---|:--|
|${var}|Substitute the value of var.|
|${var:-word}|If var is null or unset, word is substituted for var. The value of var does not change.|
|${var:=word}|If var is null or unset, var is set to the value of word.|
|${var:?message}|If var is null or unset, message is printed to standard error. This checks that variables are set correctly.|
|${var:+word}|If var is set, word is substituted for var. The value of var does not change.|


## 6. Quoting Mechanisms
### 6.1 Metacharacters

```
* ? [ ] ' " \ $ ; & ( ) | ^ < > new-line space tab
```

### 6.2 backslash, single quote, double quote and back quote

|Quoting | Description|
|:---:|:---|
|Single quote|All special characters between these quotes lose their special meaning.|
|Double quote|Most special characters between these quotes lose their special meaning with these exceptions: $ , \` , \$ , \' , \" , \\\\|
|Backslash|Any character immediately following the backslash loses its special meaning.|
|Back quote|Anything in between back quotes would be treated as a command and would be executed.|

## 7. IO Redirection
### 7.1 Output Redirection
### 7.2 Input Redirection
### 7.3 Discard the output
### 7.4 from a process to another

|Command | Descriptions|
|:---:|:---|
|pgm > file|Output of pgm is redirected to file|
|pgm < file|Program pgm reads its input from file|
|pgm >> file|Output of pgm is appended to file|
|n > file|Output from stream with descriptor n redirected to file|
|n >> file|Output from stream with descriptor n appended to file|
|n >& m|Merges output from stream n with stream m|
|n <& m|Merges input from stream n with stream m|
|<< tag|Standard input comes from here through next tag at the start of line|
|bar|Takes output from one program, or process, and sends it to another|

## 8. Function

### 8.1 Definition
```
function_name () { 
   list of commands
}
```

### 8.2 Pass Parameters to a Function

```
#!/bin/sh

# Define your function here
Hello () {
   echo "Hello World $1 $2"
}

# Invoke your function
Hello Zara Ali
```

### 8.3 Returning Values from Functions
```
#!/bin/sh

# Define your function here
Hello () {
   echo "Hello World $1 $2"
   return 10
}

# Invoke your function
Hello Zara Ali

# Capture value returnd by last command
ret=$?

echo "Return value is $ret"
```