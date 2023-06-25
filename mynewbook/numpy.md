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

```{code-cell}
import numpy as np
```

| Category | Type                      |
| :------: | :--:                      |
| Boolean  | `bool` |
| Complex  | `complex64`, `complex128`, `complex256` |
| Float    | `float16`, `float32`, `float64`, `float128` |
| Integer  | `int8`, `int16`, `int32`, `int64`, `uint8`, `uint16`, `uint32`, `uint64`   |
| Object   | `object` |
| String   | `str`, `unicode` |

**Creation:**
```{code-cell}
my_array = np.array([1, 2, 3, 4, 5])  # simple array creation
print(my_array)
print(type(my_array))                 # type
```

`ndim`: return the number of dimensions of an array\
`shape`: return the number of elements in each dimension (like calling *len()* on each dimension)\
`size`: return the total number of elements in an array (i.e., the product of *shape*)

```{code-cell}
array_0d = np.array(1)                                                
array_1d = np.array([1, 2, 3, 4, 5, 6])
array_2d = np.array([[1, 2, 3], [4, 5, 6]])
array_3d = np.array([[[1, 2, 3], [4, 5, 6]], [[3, 2, 1], [6, 5, 4]]])
```

```{code-cell}
list_2d = [[1, 2], [3, 4], [5, 6]]  # creation from list
array_2d = np.array(list_2d)
array_2d
```

| Method        | Paramethers | Description | 
| :----:        | :---------: | :---------: |
| `arange`      | [`start`, ]`stop`, [`step`, ]`dtype=None` | Returns evenly spaced values within a given interval |
| `diag`        | `array`, `k=0` | Returns a diagonal 2d-array extracting the values in the array |
| `empty`       | `shape`, `dtype=float`, `order='C'` | Returns a new empty array of given shape and type |
| `eye`         | `n`, `M=None`, `k=0`, `dtype=float`, `order='C'` | Returns a new identity 2d-array of given number of row (and columns) and type |
| `full`        | `shape`, `fill_value`, `dtype=None`, `order='C'` | Returns a new array of given shape and type, filled with a specific value |
| `identity`    | `n`, `dtype=None` | Returns a new identity quadratic 2d-array of given number of row and columns *n* type |
| `linspace`    | `start`, `stop`, `num=50`, `endpoint=True`, `retstep=False`, `dtype=None`, `axis=0` | Returns evenly spaced numbers over a specified interval |
| `ones`        | `shape`, `dtype=None`, `order='C'` | Returns a new array of given shape and type, filled with ones |
| `random.choice` | `array`, `size=None`, `replace=True`, `p=None` | Generates random values from an array in a given shape with specific probabilities |
| `random.rand` | `d0`, `d1`, `...`, `dN` | Generates random values between 0 and 1 in a given shape |
| `random.randint` | `start`, `end`, `size=None` | Generates random integer values between *start* and *end* in a given shape |
| `zeros`       | `shape`, `dtype=float`, `order='C'` | Returns a new array of given shape and type, filled with zeros |


```{code-cell}
np.arange(1, 5)
```

```{code-cell}
np.arange(0, 11, 2)
```

```{code-cell}
np.linspace(0, 10, 5)
```

```{code-cell}
np.zeros((2, 3))
```

```{code-cell}
np.ones((2, 3))
```

```{code-cell}
np.full((3, 2), 3.14)
```

```{code-cell}
np.random.rand(5, 2)
```



**Access:**

Array **indexing** is the same as accessing an array element.\
You can access an array element by referring to its index number.\
As usual, the indexes in NumPy arrays start with 0, meaning that the first element has index 0, and the second has index 1 etc.

```{code-cell}
arr = np.array([[1,2,3,4,5,6], [7,8,9,10,11,12]])

print('1st row and 2nd column: ', arr[0, 1])
```

Array **slicing** in python means taking elements from one given index to another given index.\
We pass slice instead of index like this: [start:end].\
We can also define a step, like this: [start:end:step].

If we don't pass start its considered 0.\
If we don't pass end its considered length of array in that dimension.\
If we don't pass step its considered 1.

```{code-cell}
print('From the 2nd row, slice elements from column 1 to 4 (not included): ', arr[1, 1:4])
```

Array **iterating** means going through elements one by one. You can iterate through the elements of an array using the for loop.

```{code-cell}
for x in arr:  # iterate through all the rows
  print(x)
```

```{code-cell}
for x in arr:  # 1) iterate through all the elements
  for y in x:
    print(y)
```

`nditer`(array, flags=None, op_flags=None, op_dtypes=None, order='K', casting='safe', op_axes=None, itershape=None, buffersize=0)[\*](https://numpy.org/doc/stable/reference/generated/numpy.nditer.html)
```{code-cell}
for x in np.nditer(arr):  # 2) iterate through all the elements
  print(x)
```

```{code-cell}
# 3) iterate through all the elements skipping 1 element at a time

for x in np.nditer(arr[:, ::2]):
  print(x)
```

```{code-cell}
# 4) iterate through all the elements changing the data type in-place

for x in np.nditer(arr, flags=['buffered'], op_dtypes=['S']):
  print(x)
```

`ndenumerate`(array)[\*](https://numpy.org/doc/stable/reference/generated/numpy.ndenumerate.html)
```{code-cell}
# 5) iterate through all the elements printing the indexes

for idx, x in np.ndenumerate(arr):
  print(idx, x)
```

**filter** and **search**
```{code-cell}
print(arr % 2 == 0)
print(np.where(arr % 2 == 0))  # search
print(arr[arr % 2 == 0])
```



**Operations:**

**Elementwise:**

```{code-cell}
array_x = np.array([[1,2,3], [4,5,6]])  # 2x3
array_y = np.array([[2,1,3], [6,5,4]])  # 2x3
array_z = np.array([[1], [2], [3]])     # 3x1
array_w = np.array([[1, 2, 3]])         # 1x3
```

```{code-cell}
array_x + 1
```

```{code-cell}
array_x + array_y
```

```{code-cell}
array_x == array_y
```

```{code-cell}
np.array_equal(x, y)
```

```{code-cell}
np.dot(array_x, array_z)  #

# array_x @ array_z  # equivalent
```

```{code-cell}
array_z + array_w  # broadcasting
```

**Reshape:**

```{code-cell}
arr.reshape(6, 2)  # 

arr.reshape(2, -1)  # 
```

```{code-cell}
arr.reshape(2, 3, 2)
```

```{code-cell}
arr.flatten()
```

**Sort:**

```{code-cell}
np.sort(arr)
```

**Join** and **Split**

```{code-cell}
np.concatenate((array_x, array_y))
np.concatenate((array_x, array_y), axis=1)

np.stack((array_x, array_y))
np.stack((array_x, array_y), axis=1)

np.hstack((array_x, array_y))
np.vstack((array_x, array_y))
np.dstack((array_x, array_y))
```

```{code-cell}
np.array_split(array_x, 3)
np.array_split(array_x, 3, axis=1)

np.hsplit(array_x, 3)
np.vsplit(array_x, 3)
np.dsplit(array_x, 3)
```


**Methods:**


| Category   | Function | Description | 
| :------:   | :------: | :---------: |
| Arithmetic  1 array -> 1 array | absolute      | |
|            | exp              | |
|            | log, log2, log10 | |
| Arithmetic  2 array -> 1 array | add           | |
|            | subtract       | |
|            | multiply       | |
|            | divide         | |
|            | divmod         | |
|            | power          | |
|            | mod, remainder | |
| Arithmetic  1+ array -> 1 number | sum | |
|            | prod           | |
|            | cumsum         | |
|            | cumprod        | |
| Linear Algebra  1 array -> 1 array | linealg.det | |
|            | linalg.eig     | |
|            | linalg.inv     | |
|            | linalg.matrix_rank | |
|            | linalg.norm    | |
|            | linalg.trace   | |
|            | linalg.svd, linalg.qr, linalg.lu | |
|            | transpose      | |
| Linear Algebra 2 array -> 1 array | dot, matmul, vdot | |
| Rounding  1 array -> 1 array | fix, trunc | |
|            | around         | |
|            | ceil           | |
|            | floor          | |
| Sets  2 array -> 1 array | unique | |
|            | intersect1d    | |
|            | setdiff1d      | |
|            | union1d        | |
| Statistics 1+ array -> 1 number | min, max    | |
|            | mean           | |
|            | median         | |
|            | quantile       | |
| Trigonometric  1 array -> 1 number | sin, cos, tan | |
