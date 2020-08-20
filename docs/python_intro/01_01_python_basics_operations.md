---
title: Operations in Python
template: overrides/main.html
---

The following are simple operations you can perform within python. We start with very basic operations and work up to more complex operations such as defining functions and methods

## Operations

The following are simple math expressions that can be done in Python.

### Arithmetic

<center>

| Symbol | Task Performed |
|----|---|
| +  | Addition |
| -  | Subtraction |
| /  | division |
| %  | mod |
| *  | multiplication |
| //  | floor division |
| **  | to the power of |

</center>

Simple arithmetic calculations can be completed within Python:

```python
# Addition
>>> 1 + 1
2

# Multiplication
>>> 1 * 3
3

# Division
>>> 1 / 2
0.5

# Square
>>> 2 ** 4
16

# Find remainder - called modulus
>>> 4 % 2
0

# Find remainder - called modulus
>>> 5 % 2
1

# BEDMAS
>>> (2 + 3) * (5 + 5)
50
```

### Trigonometry

<center>

| Trig Function | Name | Description |
|---------------|------|-------------|
|math.pi | pi | mathematical constant \(\pi\) |
|math.sin() | sine | sine of an angle in radians |
|math.cos() | cosine | cosine of an angle in radians |
|math.tan() | tangent | tangent of an angle in radians |
|math.asin() | arc sine | inverse sine, ouput in radians |
|math.acos() | arc cosine | inverse cosine, ouput in radians |
|math.atan() | arc tangent | inverse tangent, ouput in radians |
|math.radians() | radians conversion | degrees to radians |
|math.degrees() | degree conversion | radians to degrees |

</center>

Trigonometry functions such as sine, cosine, and tangent can also be calculated using Python:

```py
>>> from math import sin

>>> sin(60)
-0.3048106211022167
```

```py
>>> from math import sin, cos, tan, pi

>>> pi
3.141592653589793

>>> sin(pi/6)
0.49999999999999994

>>> cos(pi/6)
0.8660254037844387

>>> tan(pi/6)
0.5773502691896257

```

### Exponents/Logarithms

Calculating exponents and logarithms with Python is easy. Note the exponent and logarithm functions are imported from the math module just like the trig functions were imported from the math module above.

```py
>>> from math import log, log10, exp, e, pow, sqrt
>>> log(3.0*e**3.4)         # note: natural log
4.4986122886681095

>>> sqrt(3**2 + 4**2)
5.0

# The power function pow() works like the ** operator. pow() raises a number to a power
>>> 5**2
25

>>> pow(5,2)
25.0
```

<center>

| Math function | Name | Description |
|---------------|------|-------------|
|math.e  | Euler’s number | mathematical constant \(e\) |
|math.exp() | exponent | \(e\) raised to a power |
|math.log() | natural logarithm | log base e |
|math.log10() | base 10 logarithm | log base 10 |
|math.pow() | power | raises a number to a power |
|math.sqrt() | square root | square root of a number |

</center>

## Variables

A name that is used to denote something or a value is called a variable. When assigning variables, the variable name should be something meaningful. This way you will remeber what it is for. Variables can not start with a number or special character. In python, variables can be declared and values can be assigned to it as follows:


```py
# I prefer sepearting words in a variable with '_'
>>> name_of_var = 2

# you can also use camelCase
>>> nameOfVar = 2

# Assign numbers to variables. These are now objects in Python.
>>> x = 2
>>> y = 3

# Since they are objects you can now use them to perform operations
>>> z = x + y
>>> z
5

# Multiple variables can be assigned with the same value at once
>>> x = y = 1
>>> print (x,y)
1 1
```

Variable names in Python must conform to the following rules:

* variable names must start with a letter
* variable names can only contain letters, numbers, and the underscore character _
* variable names can not contain spaces
* variable names can not include punctuation
* variable names are not enclosed in quotes or brackets



## String Operations

Strings are sequences of letters, numbers, punctuation, and spaces. Strings are defined by enclosing letters, numbers, punctuation, and spaces in single quotes ' ' or double quotes " ".

```py
# When using strings you can use single quotes or double quotes
>>> single = 'single quotes'
>>> double = "double quotes"

# If you want a string to contain an apostrophe then use double quotes around the string...
>>> apostrophe = " wrap lot's of other quotes"
```

### String Concatenation

Strings can be concatenated or combined using the + operator.

```py
>>> word = "Solution"
>>> another_word = "another solution"
>>> third_word = "3rd solution!"
>>> all_words = word+another_word+third_word
>>> all_words
'Solutionanother solution3rd solution!'
```

### String Comparison

Strings can be compared using the comparison operator; the double equals sign ==.

!!! note 
    the comparison operator (double equals ==) is not the same as the assignment operator, a single equals sign =.

```py
>>> name1 = 'Gabby'
>>> name2 = 'Gabby'
>>> name1 == name2
True

>>> name1 = 'Gabby'
>>> name2 = 'Maelle'
>>> name1 == name2
False
```
## Printing variables

One built-in function in Python is print(). The value or expression inside of the parenthesis of a print() function “prints” out to terminal when the print() function is called.

```python
>>> x = 'hello'

# Use the built-in function to print variables/objects out
>>> print(x)
'hello'

# Use the format function to set the values within the string enclosed by curly braces {}
>>> num = 12
>>> name = 'Sam'

# Either of these methods work...
>>> print('My number is: {one}, and my name is: {two}'.format(one=num,two=name))
'My number is: 12, and my name is: Sam'

>>> print('My number is: {}, and my name is: {}'.format(num,name))
'My number is: 12, and my name is: Sam'
```

## Lists

```python
# With only integers
[1,2,3]

# With integers and strings
['hi',1,[1,2]]

# Adding new values to a list
my_list = ['a','b','c']
my_list.append('d')
print(my_list)

# Indexing a list by the items index
my_list[0]

# Indexing using a slice notation :
my_list[1:]

# Replace existing values in list
my_list[0] = 'NEW'
print(my_list)

# You can create nested lists as well
nest = [1,2,3,[4,5,['target']]]
nest[3]
nest[3][2]
nest[3][2][0]

```

## Dictionaries

```python
d = {'key1':'item1','key2':'item2'}
d

d['key1']
```

## Booleans

```python
True
```

```python
False
```

## Tuples 

```python
t = (1,2,3)
t[0]

# You can not assign items to a tuple like you can with a list
t[0] = 'NEW'
```

## Sets

```python
{1,2,3}

{1,2,3,1,2,1,2,3,3,3,3,2,2,2,1,1,2}
```

## Relational Operators

<center>

| Symbol | Task Performed |
|----|---|
| == | True, if it is equal |
| !=  | True, if not equal to |
| < | less than |
| > | greater than |
| <=  | less than or equal to |
| >=  | greater than or equal to |

</center>

```python
# False statements
1 > 2
'hi' == 'bye'

# True statements
1 < 2
1 >= 1
1 <= 4
1 == 1
```

## Logic Operators

```python
# Using 'and' to indicate both conditions need to be True
(1 > 2) and (2 < 3)

# Using 'or' to indicate only one conditions needs to be True
(1 > 2) or (2 < 3)

# You can have as many conditional statements as you want
(1 == 2) or (2 == 3) or (4 == 4)
```

## if,elif, else Statements

```python
# IF statement
if 1 < 2:
    print('Yep!')
    
# IF ELSE statement
if 1 < 2:
    print('first')
else:
    print('last')

if 1 > 2:
    print('first')
else:
    print('last')

# IF, ELIF, ELSE statement
if 1 == 2:
    print('first')
elif 3 == 3:
    print('middle')
else:
    print('Last')
```

## For Loops

```python
seq = [1,2,3,4,5]
for item in seq:
    print(item)
    
for item in seq:
    print('Yep')

# You can name the iterator whatever you like
for jelly in seq:
    print(jelly+jelly)
    
```

## While Loops

```python
i = 1
while i < 5:
    print('i is: {}'.format(i))
    i = i+1
```

## range() function

```python
range(5)

# Great for using in For loops
for i in range(5):
    print(i)

# You can use it to create lists
list(range(5))
```

## List comprehension

```python
x = [1,2,3,4]

# Perform operations within a For loop and append the outputs to a list object
out = []
for item in x:
    out.append(item**2)
print(out)
```

A very useful technique in Python is the one line for loop:

```python
[item**2 for item in x]
```

## Defining functions

```python
def my_func(param1='default'):
    """
    Docstring goes here.
    """
    print(param1)

# To call your function you need to include brackets at the end
my_func

my_func()
```

Now that you have defined your function with an input you can provide new inputs to the function to perform an operation

```python
# You can either call the defined input varible for your function
my_func(param1='new param')

# Or you can just provide the input, remember if you have multiple function inputs the position of these inputs matter!
my_func('new param')
```

```python
# Use the 'Return' function to return a value from within your function and assign it to a variable
def square(x):
    return x**2

out = square(2)
print(out)
```

## Lambda, map and filter

Instead of writing a function you can use the lambda function instead:

```python
def times2(var):
    return var*2

times2(2)

# lambda
lambda var: var*2

# map
seq = [1,2,3,4,5]
map(times2,seq)

# Combining lambda and map together you get
list(map(times2,seq))

# Here is more detail
list(map(lambda var: var*2,seq))

# Using the filter function to return values that meet a condition
filter(lambda item: item%2 == 0,seq)
list(filter(lambda item: item%2 == 0,seq))
```

## Methods

One of the most useful aspects of the Python language is that everything is an object and has inherent methods.

### string methods

```python
# Assign 'st' to be a string
st = 'hello my name is Sam'

# A string type in Python has several methods
# To return all lowercase
st.lower()

# All uppercase
st.upper()

# Split the string at white spaces
st.split()

# You can use the split method to split at a character you want
tweet = 'Go Sports! #Sports'
tweet.split('#')

# You can return only the part of the string you want after the split method
tweet.split('#')[1]
```

### dictionary methods

```python
d = {'key1': 'item1', 'key2': 'item2'}

# Print the keys in a dictionary
d.keys()

# Print the items in a dictionary
d.items()
```

### list methods

```python
lst = [1,2,3]

lst.pop()
lst

# Find a value within a list
'x' in [1,2,3]

'x' in ['x','y','z']
```
