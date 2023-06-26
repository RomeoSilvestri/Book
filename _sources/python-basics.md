---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Python - Basics

Python is a verstile high-level programming language known for its simplicity and readability. It's widely used in data science. Its rich ecosystem of libraries, such as NumPy, Pandas, and Matplotlib, provides powerful tools for data manipulation, analysis, and visualization. Python's simplicity and flexibility make it a popular choice for data scientists, enabling them to efficiently tackle complex data-driven problems.

**Input and Output**

In Python, you can use the `input` function to prompt the user for input. It displays a message to the user, waits for them to enter a value, and then returns the input as a string.

```{code-cell}
# name = input('Please enter your name: ')
```

The `print` function is used to display data as output. It takes one or more arguments and prints them to the console or standard output stream, separated by spaces.

```{code-cell}
print('Hello World!')
```

```{code-cell}
one = 1
print("Hello World! This is the number:", one)         # print with space
print("Hello World! This is the number: " + str(one))  # print without space
```

**Assignment**

The `=` operator is used for assignment. It assigns the value on the right side to the variable on the left side.

```{code-cell}
a = 'apple'                             # assignment

a, b, c = 'apple', 'banana', 'cherry'   # multiple assignment
a = b = c = 'apple'

fruits = ['apple', 'banana', 'cherry']  
a, b, c = fruits
```

**Escape Characters**

| Operator | Description   |
| :------: | :---------:   |
| `\'`     | single quote  |
| `\"`     | double quotes |
| `\\`     | backslash     |
| `\n`     | newline       |
| `\t`     | tab           |

## Basic Operations

**Arithmetic**

| Operator | Description                       |
| :------: | :---------:                       |
| `+`      | addition                          |
| `-`      | subtraction                       |
| `*`      | multiplication                    |
| `/`      | division                          |
| `**`     | exponentiation                    |
| `//`     | integer division / floor division |
| `%`      | modulo                            |

**Comparison**

| Operator     | Description                          |
| :------:     | :---------:                          |
| `x == y `    | is `x` equal to `y`?                 |
| `x != y`     | is `x` not equal to `y`?             |
| `x > y`      | is `x` greater than `y`?             |
| `x >= y`     | is `x` greater than or equal to `y`? |
| `x < y`      | is `x` less than `y`?                |
| `x <= y`     | is `x` less than or equal to `y`?    |
| `x is y`     | is `x` the same object as `y`?       |
| `x is not y` | is not `x` the same object as `y`?   |

**Logical**

| Operator | Description                          |
| :------: | :---------:                          |
| `x and y` | are `x` and `y` both True?          |
| `x or y` | is at least one of `x` and `y` True? |
| `not x` | is `x` False?                         |

**Membership**

| Operator | Description            |
| :------: | :---------:            |
| `x in y` | is `x` in `y`?         |
| `x not in y` | is not `x` in `y`? |

**Basic Arithmetic Functions**

| Type                      | Library   | Function                                    |
| :--:                      | :-----:   | :------:                                    |
| Absolute Value            | /         | `abs`                                       |
| Exponential and Logarithm | `math`    | `exp`, `log`                                |
| Factorial                 | `math`    | `factorial`                                 |
| Power and Square Root     | `math`    | `pow`, `sqrt`                               |
| Rounding                  | /, `math` | `round`, `floor`, `ceil`, `trunc`           |
| Trigonometryc             | `math`    | `sin`, `cos`, `tan`, `asin`, `acos`, `atan` |


## Variables

**Data Types**

| Category | Type                      |
| :------: | :--:                      |
| Binary   | `bytes`, `memoryview`     |
| Boolean  | `bool`                    |
| None     | `NoneType`                |
| Numeric  | `int`, `float`, `complex` |
| Sequence | `range`                   |
| String   | `str`                     |

**Data Structures**

| Category | Structure          |
| :------: | :-------:          |
| Binary   | `bytearray`        |
| Mapping  | `dict`             |
| Sequence | `list`, `tuple`    |
| Set      | `set`, `frozenset` |

Data Structures Features:
1) Tuple: ordered, unchangeable and allows duplicates
2) List: ordered, changeable and allows duplicates
3) Set: unordered (and unindexed), unchangeable and without duplicates
4) Dictionary: ordered*, changeable and without duplicate members

Casting: refers to the explicit conversion of an object or value from one data type to another. It is achieved using functions like `int`, `float`, `str`, etc. Casting allows for changing the type of data, facilitating compatibility and desired operations between different data types.

Get Type: `type` function\
Get Length: `len` function


### Strings

Strings are sequences of characters enclosed in single or double quotes. They are immutable, meaning their values cannot be changed after creation. Strings support various operations like slicing, concatenation and formatting, making them suitable for text manipulation and data representation.

**Basic Operations**

```{code-cell}
sentence = 'Hello, World!'

print(type(sentence))
print(len(sentence))
```

```{code-cell}
print(sentence[0])      # slicing
print(sentence[:5])
print(sentence[7:])
print(sentence[-6:-1])  
```

```{code-cell}
print("World" in sentence)
print("World" not in sentence)
```

```{code-cell}
w1 = 'Hello'        # concatenate
w2 = 'World'

w3 = w1 + ' ' + w2  
print(w3)
```

**Methods**

| Method | Paramethers | Description |
| :----: | :---------: | :---------: |
| `capitalize`              | /                         | Converts the first character to upper case |
| `casefold`, `lower`         | /                         | Converts string into lower case            |
| `count`                   | value, start, end         | Returns the number of times a specified value occurs |   
| `find`, `index`             | value, start, end         | Searches the string for a specified value and returns the position of where it was found |
| `format`                  | value1, ..., valueN       | Formats specified values in a string       |
| `join`                    | iterable                  | Joins the elements of an iterable to the end of the string |
| `replace`                 | oldvalue, newvalue, count | Returns a string where a specified value is replaced with a specified value |
| `rfind`, `rindex`          | value, start, end         | Searches the string for a specified value and returns the last position of where it was found |
| `split`                   | separator, maxsplit       | Splits the string at the specified separator, and returns a list |
| `splitlines`              | keeplinebreaks            | Splits the string at line breaks and returns a list |                           
| `strip`, `lstrip`, `rstrip` | characters                | Returns a trimmed version of the string |
| `title`                   | /                         | Converts the first character of each word to upper case |
| `upper`                   | /                         | Converts a string into upper case |


### Tuple

Tuples are ordered collections of elements enclosed in parentheses. They are immutable, meaning their values cannot be modified once defined. Tuples can store different data types and are commonly used to group related data or as return values for functions, providing a convenient way to ensure data integrity and prevent accidental modification.

**Creation**

```{code-cell}
tp = ()                                       # empty
tp = ('apple',)                               # one element
tp = ('apple', 'cherry', 'banana', 'orange')
```

**Access**

```{code-cell}
print(tp[:2])  # slicing

for x in tp:   # loop (all elements)
  print(x)
```

**Check Elements**

```{code-cell}
print('cherry' in tp)
print('cherry' not in tp)
```

**Insertion**

```{code-cell}
# 1) conversion into a list (with list constructor)

# 2) '+' operator (can add any iterable)

tp_1 = ('apple', 'cherry')
tp_2 = ('banana', 'orange')
tp_3 = tp_1 + tp_2 
print(tp_3)
```

**Deletion**

```{code-cell}
# 1) conversion into a list

# 2) delete the entire tuple

# del tp
```

**Update**

```{code-cell}
# conversion into a list
```

**Sort**

```{code-cell}
# 1) conversion into a list

# 2) sorted function

tp_sort = sorted(tp)
print(tp)
print(tp_sort)
```

**Copy**

```{code-cell}
# 1) slicing

tp_copy = tp[:]
print(tp_copy)


# 2) constructor

tp_copy = tuple(tp)
print(tp_copy)
```

**Unpack**

```{code-cell}
apple, cherry, banana, orange = tp
apple, *others = tp
```

**Comprehension**

```{code-cell}
tp_new = tuple(x for x in tp if 'a' in x)
print(tp_new)
```

**Methods**

| Method  | Paramethers | Description |
| :----:  | :---------: | :---------: |
| `count` | element     | Returns the number of times a specified value occurs in a tuple |
| `index` | element     | Searches the tuple for a specified value and returns the position of where it was found |


### List

Lists are ordered and mutable collections of elements enclosed in square brackets. They can hold values of different types and allow for dynamic resizing, appending, and modification of elements. Lists are versatile data structures, supporting operations like indexing, slicing, and list comprehensions, making them useful for storing and manipulating data in a flexible manner.

**Creation**

```{code-cell}
ls = []                                       # empty
ls = ['apple', 'cherry', 'banana', 'orange']
```

**Access**

```{code-cell}
print(ls[:2])  # slicing

for x in ls:   # loop
  print(x)
```

**Check Elements**

```{code-cell}
print('cherry' in ls)
print('cherry' not in ls)
```

**Insertion**

```{code-cell}
# 1) '+' operator

ls_1 = ('apple', 'banana')
ls_2 = ('cherry', 'orange')
ls_3 = ls_1 + ls_2 
print(ls_3)


# 2) append: adds an element at the end of the list

ls.append('strawberry')
print(ls)


# 3) insert: adds an element at the specified position

ls.insert(1, 'peach')
print(ls)


# 4) extend: adds elements of a list (or any iterable), to the end of the current list

ls_ext = ['lemon', 'lime']
ls.extend(ls_ext)
print(ls)
```

**Deletion**

```{code-cell}
# 1) remove: removes the element with the specified value

ls.remove('lime')
print(ls)


# 2) pop: removes the element at the specified position

ls.pop(1)
print(ls)


# 3) del: removes the item at the specified position; if the position of the item is not specified, the iterator is deleted

# del ls
del ls[1]
print(ls)


# 4) clear: removes all the elements from the iterable

# ls.clear()
# print(ls)
```

**Update**

```{code-cell}
ls[1] = 'grapes'  # slicing
print(ls)
```

**Sort**

```{code-cell}
# 1) sort method

ls.sort()
print(ls)


# 2) reverse method

ls.reverse()
print(ls)


# 3) sorted function

ls_sort = sorted(ls)
print(ls_sort)
```

**Copy**

```{code-cell}
# 1) slicing

ls_copy = ls[:]
print(ls_copy)


# 2) constructor

ls_copy = list(ls)
print(ls_copy)

# 3) copy: returns a copy of the list

ls_copy = ls.copy()
print(ls_copy)
```

**Unpack**

```{code-cell}
strawberry, orange, lemon, grapes, apple = ls
strawberry, *others = ls
```

**Comprehension**

```{code-cell}
ls_new = [x for x in ls if 'a' in x]
print(ls_new)
```

**Methods**

| Method    | Paramethers | Description |
| :----:    | :---------: | :---------: |
| `append`  | element                          | Adds an element at the end of the list |
| `clear`   | /                                | Removes all the elements from the list |
| `copy`    | /                                | Returns a copy of the list |
| `count`   | element                          | Returns the number of times a specified value occurs in a list |
| `extend`  | iterable                         | Adds elements of a list (or any iterable), to the end of the current list |
| `index`   | element                          | Searches the list for a specified value and returns the position of where it was found |
| `insert`  | position, element                | Adds an element at the specified position |
| `pop`     | position                         | Removes the element at the specified position |
| `remove`  | element                          | Removes the element with the specified value |
| `reverse` | /                                | Reverses the order of the list |
| `sort`    | reverse=True/False, key=function | Sorts the list |


### Set

Sets are unordered and mutable collections of unique elements. They provide efficient membership testing and operations like union, intersection, and difference. Sets do not allow duplicate values, making them useful for eliminating duplicates or checking for membership in a collection of items.

**Creation**

```{code-cell}
st = set()                                    # empty
st = {'apple', 'cherry', 'banana', 'orange'}
```

**Access**

```{code-cell}
for x in st:  # loop
  print(x)
```

**Check Elements**

```{code-cell}
print('cherry' in tp)
print('cherry' not in tp)
```

**Insertion**

```{code-cell}
# 1) add: adds an element to the set

st.add('strawberry')
print(st)


# 2) '|' operator or union method: return a set containing the union of sets

st_original = {'apple', 'cherry', 'banana', 'orange'}
st_plus = {'lemon', 'lime'}

st_union = st_original | st_plus
st_original.union(st_plus)

print(st_union)
print(st_original)


# 3) update: update the set with the union of this set and others

st.update(st_plus)
print(st)
```

**Deletion**

```{code-cell}
# 1) remove / discard : removes the element with the specified value
# - > discard doesn't give errors

st.remove('lemon')
st.discard('lime')
print(st)


# 2) pop: removes a random element from the set

st.pop()
print(st)


# 3) del - > as the lists (but the index cannot be inserted)

# del st


# 4) clear

# st.clear()
# print(st)
```

**Update:** impossible

**Sort**

```{code-cell}
# 1) conversion into a list

# 2) sorted function

st_sort = sorted(st)
print(st_sort)
```

**Copy**

```{code-cell}
# 1) constructor

st_copy = set(st)
print(st_copy)


# 2) copy: returns a copy of the set

st_copy = st.copy()
print(st_copy)
```

**Unpack:** impossible

**Comprehension**

```{code-cell}
st_new = {x for x in st if 'a' in x}
print(st_new)
```

**Methods**

| Method                        | Paramethers     | Description |
| :----:                        | :---------:     | :---------: |
| `add`                         | element         | Adds an element to the set |
| `clear`                       | /               | Removes all the elements from the set |
| `copy`                        | /               | Returns a copy of the set |
| `difference`                  | set             | Returns a set containing the difference between two sets |
| `difference_update`           | set             | Removes the elements in this set that are also included in another specified set |
| `discard`                     | value           | Removes the specified value |
| `intersection`                | set1, ..., setN | Returns a set, that is the intersection of two other sets |
| `intersection_update`         | set1, ..., setN | Removes the elements in this set that are not present in other specified sets |
| `isdisjoint`                  | set             | Returns whether two sets have a intersection or not |
| `issubset`                    | set             | Returns whether another set contains this set or not |
| `issuperset`                  | set             | Returns whether this set contains another set or not |
| `pop`                         | /               | Removes a random element from the set |
| `remove`                      | element         | Removes the element with the specified value |
| `symmetric_difference`        | set             | Returns a set with the symmetric differences of two sets |
| `symmetric_difference_update` | set             | Inserts the symmetric differences from this set and another |
| `union`                       | /               | Return a set containing the union of sets |
| `update`                      | iterable        | Update the set with the union of this set and other iterables |


### Dictionary

Dictionaries are unordered collections of key-value pairs enclosed. They provide efficient value retrieval based on unique keys. Dictionaries allow for adding, modifying, and deleting key-value pairs, making them useful for organizing and accessing data based on custom identifiers.

**Creation**

```{code-cell}
dc = {
  'brand': 'Ford',
  'model': 'Mustang',
  'year': 1964
}
```

**Access**

```{code-cell}
# 1) all keys

for x in dc:
  print(x)


for x in dc.keys():
  print(x)


dc_key = dc.keys()  # list of keys
```

```{code-cell}
# 2) all values

for x in dc:
  print(dc[x])


for x in dc.values():
  print(x)


dc_val = dc.values()  # list of values
```

```{code-cell}
# 3) specific value

print(dc['model'])      # slicing

print(dc.get('model'))  # get method
```

```{code-cell}
# 4) all items 

for x, y in dc.items():
  print(x, y)


dc_item = dc.items()  # list of items
print(dc_item)
```

**Insertion**

```{code-cell}
# 1) slicing

dc['speed'] = 300
print(dc)


# 2) update method

dc.update({'color': 'red'})
print(dc)
```

**Deletion**

```{code-cell}
# 1) pop / del : removes the item with the specified key
# - > del can delete the whole dictionary

dc.pop('speed')
del dc['color']
print(dc)


# 2) popitem: removes the last inserted key-value pair

dc.popitem()
print(dc)


# 3) clear: removes all the elements from the dictionary

# dc.clear()
# print(dc)
```

**Update**

```{code-cell}
dc['brand'] = 'Ferrari'
dc['model'] = 'California'
print(dc)
```

**Sort**

```{code-cell}
dc_key_sort = sorted(dc.keys())
dc_val_sort = sorted(dc.values())

print(dc_key_sort)
print(dc_val_sort)
```

**Copy**

```{code-cell}
# 1) constructor

dc_copy = dict(dc)
print(dc_copy)


# 2) copy method

dc_copy = dc.copy()
print(dc_copy)
```

**Unpack**

```{code-cell}
brand, model = dc.keys()
Ferrari, California = dc.values()
```

**Comprehension**

```{code-cell}
dc_new = {x: y for x, y in dc.items() if 'a' in y}
print(dc_new)
```

**Methods**

| Method       | Paramethers | Description |
| :----:       | :---------: | :---------: |
| `clear`      | /           | Removes all the elements from the set |
| `copy`       | /           | Returns a copy of the set |
| `fromkeys`   | keys, value | Returns a dictionary with the specified keys and value |
| `get`        | key, value  | Returns the value of the specified key |
| `items`      | /           | Returns a list containing a tuple for each key value pair |
| `keys`       | /           | Returns a list containing the dictionary's keys |
| `pop`        | key, value  | Removes the element with the specified key |
| `popitem`    | /           | Removes the last inserted key-value pair |
| `setdefault` | key, value  | Returns the value of the specified key; if the key does not exist, insert the key, with the specified value |
| `values`     | /           | Returns a list of all the values in the dictionary |
| `update`     | iterable    | Updates the dictionary with the union of this dictionary and other iterables |


## Flow Control

### If-Else

`if`: executes a block of code if a certain condition is true\
`elif`: provides an additional condition to check if the preceding if statement is false\
`else`: specifies a block of code to execute when all preceding conditions in the if and elif statements are false

```{code-cell}
a = 5
b = 10

if a > b:
  print('a is greater than b')
elif a == b:
  print('a and b are equal')
else:
  print('a is smaller than b')
```

```{code-cell}
if a > b:  # if statement cannot be empty, so put the pass statement to avoid 
           # getting an error if there is no content
  pass
```


### Try-Except

`try`: tries to execute a block of code checking for exceptions\
`except`: catches and handles specific exceptions that may occur within the try block\
`else`: specifies a block of code to execute if no exceptions are raised in the try block

```{code-cell}
try:
  print(X)
except:
  print('An exception occurred')
  
try:
  print(X)
except NameError:
  print('Variable X is not defined')
except:
  print('Something else went wrong')
  
try:
  print('Hello')
except:
  print('Something went wrong')
else:
  print('Nothing went wrong')
```


### Loops

`while`: executes a set of statements as long as a condition is true\
`for`: executes a set of statements, once for each item in an object

`break`: stops the loop even if the while condition is true\
`continue`: stops the current iteration, and continue with the next\
`pass`: allows to avoid syntax errors and keep the structure of the code intact, even if there is no specific implementation for a certain part

**While**

```{code-cell}
i = 0       
while i < 6:
  i += 1
  print(i)
```

```{code-cell}
i = 0
while i < 6:
  i += 1
  if i == 3:
    continue
  print(i)
```

```{code-cell}
i = 0
while i < 6:
  i += 1
  if i == 3:
    break
  print(i)
```

**For**

```{code-cell}
for x in range(1, 6):
  print(x)
```

```{code-cell}
for x in 'banana':  # loop through string
  print(x)
```

```{code-cell}
fruits = ['apple', 'banana', 'cherry']  # loop through elements
for x in fruits:
  print(x)
```

```{code-cell}
adj = ['red', 'big', 'tasty']           # nested loops
fruits = ['apple', 'banana', 'cherry']
for x in adj:
  for y in fruits:
    print(x, y)
```


## Function

The `def` statement is used to define functions, allowing the creation of reusable blocks of code. The `return` statement is used within a function to specify the value to be outputted or returned. It provides the result back to the caller and terminates the function.

```{code-cell}
def my_function():                # simple function
  print('Hello from a function')

my_function()  # print a string
```

```{code-cell}
def my_function(x):  # function with a parameter and return
  return 5 * x

print(my_function(3))
```

```{code-cell}
def my_function(country = 'Italy'):  # function with a default parameter
  print('I am from ' + country)

my_function('Germany')
```

If the number of arguments to be passed into a function is unknown, add an `*` before the parameter name in the function definition. This way, the function will receive a tuple of parameters and can access the items accordingly.

```{code-cell}
def my_function(*kids):  # function with an arbitrary number of parameters
  print('The youngest child is ' + kids[2])

my_function('Emil', 'Tobias', 'Linus')
```

If the number of keyword arguments to be passed into the function is unknown, two asterisks `**` should be added before the parameter name in the function definition. This way, the function will receive a dictionary of arguments and can access the items accordingly.

```{code-cell}
def my_function(**kid):
  print('His last name is ' + kid['lname'])

my_function(fname = 'Tobias', lname = 'Rossi')
```


## Class

In Python, classes are blueprints for creating objects that encapsulate data and functionality. They define the structure and behavior of objects through attributes (variables) and methods (functions). Classes provide a way to organize and modularize code, promoting code reusability and maintainability. Objects created from classes have their own unique state and can interact with each other through method calls and attribute access.

`self` parameter: is a reference to the current instance of the class, and is used to access variables that belongs to the class; it can have any name\
`__init__()`: is always executed when the class is being initiated; it's used to assign values to object properties, or other operations that are necessary to do when the object is being created\
`__str__()`: controls what should be returned when the class object is represented as a string; if it's not set, the string representation of the object is returned

```{code-cell}
class Person:

  def __init__(self, name, age):
    self.name = name
    self.age = age

  def __str__(self):
    return f'{self.name}({self.age})'
    
  def my_function(self):
    print('Hello, my name is ' + self.name)

person_1 = Person('John', 36)

print(person_1.name)
print(person_1.age)
print(person_1)
person_1.my_function()
```

The methods we’ve seen so far are sometimes calles "regular" methods, they act on an instance of the class (i.e., take self as an argument). There are also class methods that act on the actual class. Class methods are often used as constructors and they are defined using the `@classmethod` decorator.

```{code-cell}
class Member:

    def __init__(self, first, last):
        self.first = first
        self.last = last
        self.email = first.lower() + '.' + last.lower() + '@gmail.com'
        
    def full_name(self):
        return f'{self.first} {self.last}'
    
    @classmethod                           # decorator
    def from_csv(cls, csv_name):
        first, last = csv_name.split(',')
        return cls(first, last)

member_1 = Member.from_csv('John,Rambo')
member_1.full_name()
```

There is a third kind of method called a static method. Static methods do not operate on either the instance or the class, they are just simple functions. But we might want to include them in the class because they are somehow related to the class. They are defined using the `@staticmethod` decorator.