---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
    display_name: R
    language: R
    name: ir
---

# R

**Output:**

Print strings: *print*\
Print strings + variables: *paste*, *paste0*

```{code-cell}
print('Hello World!')

one=1
print(paste("Hello World! I'm the number:", one))    # print with space
print(paste0("Hello World! I'm the number: ", one))  # print without space
```

**Basic arithmetic operations:**

\+ addition, - subtraction, * multiplication, / division\
^ power, %% modulus, %/% integer division\

*Comparison*
== equal, != not equal\
< less than, <= less than or equal to, > greater than, >= greater than or equal to\

*Logical*
& and, | or, !() not\
&& , ||  lazy versions (the execution of an operation is aborted as soon as a condition is not met)\
\
*Identity*\
Identity operators are used to compare the objects, not if they are equal,\
but if they are actually the same object, with the same memory location\
is, is not\
\
*Membership*\
Membership operators are used to test if a sequence is presented in an object\
%in%
```{code-cell}
5 + 2    # -> 7
5 - 2    # -> 3
5 * 2    # -> 10
5 / 2    # -> 2.5
5 ^ 2    # -> 25
5 %% 2   # -> 1
5 %/% 2  # -> 2

5 == 2  # -> False  comparison
5 != 2  # -> True

5 > 2 & 5 < 10     # -> True  logical
5 > 10 | 5 < 10    # -> True
!(5 > 2 & 5 < 10)  # -> False
```

**Basic arithmetic functions:**\
Exponential and Logarithm: exp(), log()\
Trigonometric functions: sin(), cos(), tan(), asin(), acos(), atan()\
Other mathematical functions: abs(), sqrt()
```{code-cell}
exp(5)    # -> 148.413
log(5)    # -> 1.609  natural logarithm
log(5,2)  # -> 2.322  logarithm in base 2
sin(0.5)  # -> 0.479
abs(-5)   # -> 5
```
\
**Variables:**\
\
*Data Types*\
Numeric Types: *integer*, *numeric*, *complex*\
Text Type: *character*\
Boolean Type:	*logical*\
Binary Types:	*raw*

```{code-cell}
# Assignment

x = 5
y = 'John'
a = b = c = 'apple'  # multiple assignment


# Casting

d = as.integer(5.8)  # -> 5
d = as.integer('5')  # -> 5
d = as.numeric(5)    # -> 5.0
d = as.character(5)  # -> '5'


# Get Type

typeof(x)  # basic type of the object
class(x)   # class of the object, which may be a base class or a user-defined class
mode(x)    # mode of the object, which indicates how the data is stored in memory
```