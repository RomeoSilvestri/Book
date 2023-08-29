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

# Numpy

NumPy is a powerful Python library for numerical computation. It provides efficient multi-dimensional array operations, along with a wide range of mathematical functions. NumPy's compact syntax and high-performance capabilities make it essential for scientific and data-related tasks.

```{code-cell}
import numpy as np
```

**Data Types**

NumPy introduces specialized data types that are more memory-efficient and offer faster computations compared to the built-in Python data types. These NumPy data types are designed to handle large arrays efficiently, enabling vectorized operations and better numerical precision. In contrast, the standard Python data types are more general-purpose but may not perform as efficiently when dealing with large-scale numerical computations.

| Category | Type                      |
| :------: | :--:                      |
| Boolean  | `bool` |
| Complex  | `complex64`, `complex128`, `complex256` |
| Float    | `float16`, `float32`, `float64`, `float128` |
| Integer  | `int8`, `int16`, `int32`, `int64`, `uint8`, `uint16`, `uint32`, `uint64`   |
| Object   | `object` |
| String   | `str`, `unicode` |


## Creation

```{code-cell}
my_array = np.array([1, 2, 3, 4, 5])  # simple array creation
my_array
```

```{code-cell}
print(type(my_array))
```

`ndim`: returns the number of dimensions of an array\
`shape`: returns the number of elements in each dimension (like calling *len* on each dimension)\
`size`: returns the total number of elements in an array (i.e., the product of *shape*)

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

```{code-cell}
print(np.ndim(array_2d))
print(np.shape(array_2d))
print(np.size(array_2d))
```

**Functions**

| Function      | Paramethers | Description | 
| :------:      | :---------: | :---------: |
| `arange`      | start, stop, step*, dtype*=None ... | Returns evenly spaced values within a given interval |
| `diag`        | v, k*=0 | Returns a diagonal 2d-array extracting the values in the array |
| `empty`       | shape, dtype*=float ... | Returns a new empty array of given shape and type |
| `eye`         | N, M*=None, k*=0, dtype*=float ... | Returns a new identity 2d-array of given number of row (and columns) and type |
| `full`        | shape, fill_value, dtype*=None ... | Returns a new array of given shape and type, filled with a specific value |
| `identity`    | n, dtype*=None ... | Returns a new identity quadratic 2d-array of given number of row and columns |
| `linspace`    | start, stop, num*=50, dtype*=None ... | Returns evenly spaced numbers over a specified interval |
| `ones`        | shape, dtype*=None ... | Returns a new array of given shape and type, filled with ones |
| `random.choice` | a, size*=None, replace*=True, p*=None | Generates random values from a given 1d-array in a given shape with specific probabilities |
| `random.rand` | d0, d1, ..., dN | Generates random values between 0 and 1 in a given shape |
| `random.randint` | low, high*=None, size*=None, dtype*=None | Generates random integer values between *start* and *end* in a given shape |
| `zeros`       | shape, dtype*=float ... | Returns a new array of given shape and type, filled with zeros |

**Examples**

```{code-cell}
np.arange(1, 5)
```

```{code-cell}
np.arange(0, 11, 2)
```

```{code-cell}
np.diag([1, 2, 3])
```

```{code-cell}
np.empty((3, 4))
```

```{code-cell}
np.eye(3, 4)
```

```{code-cell}
np.full((3, 4), 3.14)
```

```{code-cell}
np.identity(3)
```

```{code-cell}
np.linspace(0, 10, 5)
```

```{code-cell}
np.ones((3, 4))
```

```{code-cell}
np.random.choice([1, 2, 3, 4, 5], (3, 4))
```

```{code-cell}
np.random.rand(3, 4)
```

```{code-cell}
np.random.randint(-10, 50, (3, 4))
```

```{code-cell}
np.zeros((3, 4))
```


## Access

Array **indexing** is the same as accessing an array element.\
You can access an array element by referring to its index number.\
As usual, the indexes in NumPy arrays start with 0, meaning that the first element has index 0, and the second has index 1 etc.

```{code-cell}
arr = np.array([[1,2,3,4], [5,6,7,8]])

print('1st row and 2nd column: ', arr[0, 1])
```

Array **slicing** in python means taking elements from one given index to another given index.\
We pass slice instead of index like this: *[start:end]*.\
We can also define a step, like this: *[start:end:step]*.

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

To iterate through the elements of an array, the `nditer`(op, flags*=None, op_dtypes*=None ...) function or the `ndenumerate`(arr) function can be used:

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

```{code-cell}
# 5) iterate through all the elements printing the indexes

for idx, x in np.ndenumerate(arr):
  print(idx, x)
```

Array **filtering** refers to the operation of extracting elements from an array that meet a particular condition, creating a new array that contains only those selected elements.

```{code-cell}
print(arr[arr % 2 == 0])
```

Array **searching** refers to the process of finding specific elements or their indices within an array based on a given condition or value. To search for element indexes, the `where`(condition) function can be used:

```{code-cell}
print(arr % 2 == 0)
print(np.where(arr % 2 == 0))
```


## Operations

**Elementwise**

Elementwise operations involve performing mathematical operations independently on each element of a set. They enable efficient processing of large datasets and are commonly used in programming and mathematical computations.

```{code-cell}
array_x = np.array([[1,2,3], [4,5,6]])     # 2x3
array_y = np.array([[12,11,10], [9,8,7]])  # 2x3
array_z = np.array([[1], [2], [3]])        # 3x1
array_w = np.array([[1, 2, 3]])            # 1x3
```

```{code-cell}
array_x + 1  # operation between array and scalar
```

```{code-cell}
array_x + array_y  # operation between two arrays
```

```{code-cell}
array_x == array_y  # compares the elements of two arrays by returning an array                     # of Boolean values indicating which elements are equal
```

```{code-cell}
np.array_equal(x, y)  # checks whether two arrays are identical
```

```{code-cell}
np.dot(array_x, array_z)  # scalar product between arrays

# array_x @ array_z  # equivalent
```

```{code-cell}
array_z + array_w  # broadcasting
```

**Reshape**

The `reshape` function in NumPy allows for changing the shape or dimensions of an array without altering its data. It enables reorganizing the elements of an array into a different shape while ensuring that the total number of elements remains the same. The reshape function does not change the array in place.

```{code-cell}
arr.reshape(4, 2)  # changes the shape

arr.reshape(2, -1)  # changes the shape by recognizing missing dimensions

arr.reshape(2, 2, 2)  # changes shape and dimensions
```

The `resize` function in NumPy allows modifying the shape of an array, either by adding or removing elements, to fit the specified dimensions. It can resize the array inplace, altering its data, and can also introduce or discard elements based on the new shape.

```{code-cell}
arr.resize(4, 2)  # changes the shape in place
```

The `flatten` function in NumPy converts a multi-dimensional array into a 1D array by concatenating all the elements in a row-major order. It creates a flat array, which is useful for simplifying the array structure and iterating over the elements sequentially. The flatten function does not change the array in place.

```{code-cell}
arr.flatten()
```

**Sort**

The `sort` function in NumPy arranges the elements of an array in ascending order by default, or in descending order if specified. This enables efficient data analysis, searching, and retrieval of specific values within the array.

```{code-cell}
np.sort(arr)
```

**Join** and **Split**

Joining in NumPy usually refers to concatenating or combining arrays along a specified axis. Splitting, on the other hand, involves dividing an array into multiple smaller arrays along a specified axis.

To do the join between two arrays there are basically two ways: chaining (`concatenate` function) joins two arrays without adding additional dimensions, while stacking (`stack` function) adds another dimension.

```{code-cell}
print(np.shape(array_x), np.shape(array_y))

array_c1 = np.concatenate((array_x, array_y))           # concatenates along columns
print(array_c1)
print(np.shape(array_c1))

array_c2 = np.concatenate((array_x, array_y), axis=1)   # concatenates along rows
print(array_c2)
print(np.shape(array_c2))
```

```{code-cell}
array_s1 = np.stack((array_x, array_y))           # stacks two arrays along columns
print(array_s1)
print(np.shape(array_s1))

array_s2 = np.stack((array_x, array_y), axis=1)   # stacks two arrays along rows
print(array_s2)
print(np.shape(array_s2))
```

```{code-cell}
array_s3 = np.hstack((array_x, array_y))  # stacks horizontally (along columns)
print(array_s3)
print(np.shape(array_s3))

array_s4 = np.vstack((array_x, array_y))  # stacks vertically (along rows)
print(array_s4)
print(np.shape(array_s4))

array_s5 = np.dstack((array_x, array_y))  # stacks adding a depth dimension
print(array_s5)
print(np.shape(array_s5))
```

To split an array into many subarrays, the `array_split` functions or variants of the `split` function are used in a similar and opposite manner to the join functions.

```{code-cell}
array_split1 = np.array_split(array_x, 2)          # splits an array into n arrays by columns
print(array_split1)

array_split2 = np.array_split(array_x, 2, axis=1)  # splits an array into n arrays by rows
print(array_split2)

# np.hsplit(array_x, 2)
# np.vsplit(array_x, 2)
# np.dsplit(array_x, 2)
```


## Methods

| Category | Transformation | Function | Description | 
| :------: | :------------: | :------: | :---------: |
| Arithmetic | 1 array -> 1 array | `absolute` | Computes the absolute values of the elements in an array |
|            | | `cumsum` | Returns the cumulative sum of elements in an array along a specified axis |
|            | | `cumprod` | Returns the cumulative product of elements in an array along a specified axis |
|            | | `exp` | Computes the exponential values of the elements in an array |
|            | | `log`, `log2`, `log10` | Compute the logarithms of the elements in an array |
|            | 2 array -> 1 array | `add` | Performs element-wise addition between two arrays |
|            | | `subtract` | Performs element-wise subtraction between two arrays |
|            | | `multiply` | Performs element-wise multiplication between two arrays |
|            | | `divide` | Performs element-wise division between two arrays |
|            | | `divmod` | Returns the quotient and the remainder of element-wise division between two arrays |
|            | | `power` | Raises the elements of an array to the power of corresponding elements in another array |
|            | | `mod`, `remainder` | Returns the remainder of element-wise division between two arrays |
|            | 1+ array -> 1 number | `sum` | Returns the sum of elements in an array |
|            | | `prod` | Returns the product of elements in an array |
| Linear Algebra | 1 array -> 1 array | `linealg.det` | Returns the determinant of a square matrix |
|            | | `linalg.eig` | Returns the eigenvalues and eigenvectors of a square matrix |
|            | | `linalg.inv` | Returns the inverse of a square matrix |
|            | | `linalg.matrix_rank` | Returns the rank of a matrix |
|            | | `linalg.norm` | Returns the Euclidean norm of a vector or the matrix norm of an array |
|            | | `linalg.trace` | Returns the trace of a matrix |
|            | | `linalg.svd`, `linalg.qr`, `linalg.lu` | Returns a specific decomposition of a matrix |
|            | | `transpose` | Returns the transposed matrix |
|            | 2 array -> 1 array | `dot`, `matmul`, `vdot` | Performs matrix multiplication between two arrays |
| Rounding | 1 array -> 1 array | `fix`, `trunc` | Rounds the elements of an array towards zero to the nearest integer |
|          | | `around` | Rounds the elements of an array to the specified number of decimals or to the nearest integer if no decimals are provided |
|          | | `ceil` | Rounds the elements of an array up to the nearest integer |
|          | | `floor` | Rounds the elements of an array down to the nearest integer |
| Sets | 2 array -> 1 array | `unique` | Returns the sorted unique values in an array, removing any duplicates |
|      | | `intersect1d` | Returns the sorted, unique values that are common to two input arrays |
|      | | `setdiff1d` | Returns the sorted, unique values that are in one input array but not in the other |
|      | | `union1d` | Returns the sorted, unique values from combining two input arrays, removing any duplicates |
| Statistics | 1+ array -> 1 number | `min`, `max` | Returns the minimum / maximum value along a specified axis or the minimum / maximum element in an array |
|            | | `mean` | Returns the arithmetic mean of elements in an array along a specified axis |
|            | | `median` | Returns the median value of elements in an array along a specified axis |
|            | | `quantile` | Returns the specified quantile(s) of elements in an array along a specified axis |
| Trigonometric | 1 array -> 1 array | `sin`, `cos`, `tan` | Returns the specific trigonometric function of elements in an array |