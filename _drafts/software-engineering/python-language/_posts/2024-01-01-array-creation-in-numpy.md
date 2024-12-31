---
layout: post
title: "Array Creation in NumPy"
author: andre
categories: [ software-engineering, python-language ]
tags: [numpy]
image: /assets/images/software-engineering/python-language/array-creation-in-numpy.png
description: "This post provides a comprehensive guide with examples on using NumPy for array creation, showcasing efficient methods to initialize arrays with specific values, shapes, and patterns."
comments: true
---

- Table of Contents
{:toc .large-only}

NumPy offers a versatile set of tools for array creation, enabling users to initialize arrays efficiently with desired shapes, values, and patterns.

These tools support a wide range of initialization methods, from creating arrays filled with zeros or ones to generating evenly spaced sequences, random values, or customized patterns. Functions like `zeros`, `ones`, `arange`, `linspace`, and `random` provide flexibility for diverse use cases, while advanced techniques such as reshaping and broadcasting allow for precise control over array dimensions.

Designed with performance and scalability in mind, NumPy's array creation capabilities form the foundation for numerical computations and data processing tasks.

For more information, see the [NumPy: Array Creation Routines](https://numpy.org/doc/stable/reference/routines.array-creation.html).


## 1. From Shape or Value

Array creation "From Shape or Value" in NumPy focuses on generating arrays with specific shapes, sizes, or fill values. 
These functions allow for efficient initialization of arrays tailored to various computational needs, from uninitialised 
arrays to those filled with ones, zeros, or custom values.

By using these methods, you can quickly create arrays with predefined characteristics or based on the attributes of 
existing arrays, streamlining workflows for numerical computations and data manipulation.

For more details, see the [Array Creation Routines](https://numpy.org/doc/stable/reference/routines.array-creation.html#routines-array-creation).


| Operation             | Function          | Description                                                                 | Documentation                                                                                           |
|-----------------------|-------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| **Uninitialized**     | `np.empty()`      | Creates an uninitialized array of a given shape                             | [Link](https://numpy.org/doc/stable/reference/generated/numpy.empty.html#numpy.empty)                   |
| **Uninitialized**     | `np.empty_like()` | Creates an uninitialized array based on the shape and type of a given array | [Link](https://numpy.org/doc/stable/reference/generated/numpy.empty_like.html#numpy.empty_like)         |
| **Identity Matrix**   | `np.eye()`        | Creates a 2D array with ones on the diagonal and zeros elsewhere            | [Link](https://numpy.org/doc/stable/reference/generated/numpy.eye.html#numpy.eye)                       |
| **Identity Matrix**   | `np.identity()`   | Returns a square identity matrix                                            | [Link](https://numpy.org/doc/stable/reference/generated/numpy.identity.html#numpy.identity)             |
| **Filled with Ones**  | `np.ones()`       | Creates an array filled with ones                                           | [Link](https://numpy.org/doc/stable/reference/generated/numpy.ones.html#numpy.ones)                     |
| **Filled with Ones**  | `np.ones_like()`  | Creates an array of ones based on a reference array                         | [Link](https://numpy.org/doc/stable/reference/generated/numpy.ones_like.html#numpy.ones_like)           |
| **Filled with Zeros** | `np.zeros()`      | Creates an array filled with zeros                                          | [Link](https://numpy.org/doc/stable/reference/generated/numpy.zeros.html#numpy.zeros)                   |
| **Filled with Zeros** | `np.zeros_like()` | Creates an array of zeros based on a reference array                        | [Link](https://numpy.org/doc/stable/reference/generated/numpy.zeros_like.html#numpy.zeros_like)         |
| **Custom Fill Value** | `np.full()`       | Creates an array filled with a specific value                               | [Link](https://numpy.org/doc/stable/reference/generated/numpy.full.html#numpy.full)                     |
| **Custom Fill Value** | `np.full_like()`  | Creates an array filled with a value based on a reference array             | [Link](https://numpy.org/doc/stable/reference/generated/numpy.full_like.html#numpy.full_like)           |


### 1.1 Empty (np.empty)

The `np.empty()` function in NumPy is used to create a new array of a specified shape and type without initializing its entries. This means that the array will contain arbitrary values (garbage values) based on the memory allocation, making it faster than other initialization methods.

This function is particularly useful for scenarios where array values will be explicitly set later, and the initial content is irrelevant.

**Example:**

```python
import numpy as np

# Create an uninitialized array with shape (2, 3)
uninitialized_array = np.empty((2, 3))

# Create an uninitialized array with a specified data type
uninitialized_float_array = np.empty((2, 3), dtype=float)

# Print the arrays
print("Uninitialized array with shape (2, 3):\n", uninitialized_array)
print("\nUninitialized array with float dtype:\n", uninitialized_float_array)
```

### 1.2 Empty Like (np.empty_like)

The `np.empty_like()` function in NumPy creates a new array with the same shape and type as a specified prototype array. Similar to `np.empty()`, the entries of the array are uninitialized, meaning they contain arbitrary values from memory.

This function is useful when you need to create an uninitialized array that matches the structure of an existing one, saving time and ensuring consistency in shape and type.

**Example:**

```python
import numpy as np

# Define a prototype array
prototype_array = np.array([[1, 2, 3], [4, 5, 6]])

# Create an uninitialized array with the same shape and type as the prototype
uninitialized_like_array = np.empty_like(prototype_array)

# Create an uninitialized array with the same shape but a different data type
uninitialized_float_like_array = np.empty_like(prototype_array, dtype=float)

# Print the arrays
print("Prototype array:\n", prototype_array)
print("\nUninitialized array with the same shape and type:\n", uninitialized_like_array)
print("\nUninitialized array with the same shape but float dtype:\n", uninitialized_float_like_array)
```

### 1.3 Eye (np.eye)

The `np.eye()` function in NumPy creates a 2-D array with ones on its main diagonal and zeros elsewhere. It is commonly used to generate identity matrices or diagonal matrices for linear algebra operations.

You can specify additional parameters like the number of rows (`N`), the number of columns (`M`), the diagonal offset (`k`), and the data type (`dtype`) to customize the array.

**Example:**

```python
import numpy as np

# Create a square identity matrix of size 3x3
identity_matrix = np.eye(3)

# Create a rectangular matrix with 3 rows and 5 columns
rectangular_matrix = np.eye(3, 5)

# Create a matrix with the diagonal offset by 1 (above the main diagonal)
offset_diagonal_matrix = np.eye(4, k=1)

# Create a matrix with the diagonal offset by -1 (below the main diagonal)
lower_diagonal_matrix = np.eye(4, k=-1)

# Print the matrices
print("3x3 Identity matrix:\n", identity_matrix)
print("\n3x5 Rectangular matrix:\n", rectangular_matrix)
print("\nMatrix with diagonal offset by 1:\n", offset_diagonal_matrix)
print("\nMatrix with diagonal offset by -1:\n", lower_diagonal_matrix)
```
**Output:**
```text
3x3 Identity matrix:
 [[1. 0. 0.]
 [0. 1. 0.]
 [0. 0. 1.]]

3x5 Rectangular matrix:
 [[1. 0. 0. 0. 0.]
 [0. 1. 0. 0. 0.]
 [0. 0. 1. 0. 0.]]

Matrix with diagonal offset by 1:
 [[0. 1. 0. 0.]
 [0. 0. 1. 0.]
 [0. 0. 0. 1.]
 [0. 0. 0. 0.]]

Matrix with diagonal offset by -1:
 [[0. 0. 0. 0.]
 [1. 0. 0. 0.]
 [0. 1. 0. 0.]
 [0. 0. 1. 0.]]

```


## Summary

NumPy's array creation routines are essential for initializing arrays efficiently, catering to various computational and data manipulation needs. These functions provide a foundation for generating arrays with specific values, shapes, and patterns, making them indispensable in tasks ranging from numerical analysis to scientific computing.

Functions like `zeros`, `ones`, `arange`, and `linspace` enable seamless initialization of arrays, while random number generators and reshaping techniques add versatility to array handling. These tools not only simplify the process of creating arrays but also enhance performance when working with large datasets.

In conclusion, NumPy's array creation capabilities empower users to build arrays with precision and efficiency, forming the backbone of effective numerical computations and data processing workflows.
 