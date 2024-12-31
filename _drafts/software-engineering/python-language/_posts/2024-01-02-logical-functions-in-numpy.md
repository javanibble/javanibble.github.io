---
layout: post
title: "Logical Functions in NumPy"
author: andre
categories: [ software-engineering, python-language ]
tags: [numpy]
image: /assets/images/software-engineering/python-language/logical-functions-in-numpy.png
description: "This post provides a comprehensive guide with examples on using logical functions in NumPy for efficient conditional evaluations and data manipulation."
comments: true
---

- Table of Contents
{:toc .large-only}

NumPy provides a comprehensive suite of logical functions that enable element-wise operations on arrays to evaluate conditions, perform logical comparisons, and combine Boolean results.

These functions operate on arrays of any shape and return Boolean arrays (`True` or `False`) as output, making them essential for filtering, masking, and conditional processing. Common operations include logical conjunction (`logical_and`), disjunction (`logical_or`), negation (`logical_not`), and exclusive disjunction (`logical_xor`).

Additionally, functions like `all` and `any` allow for array-wide aggregation of Boolean results. Designed for efficiency and flexibility, NumPy's logical functions are indispensable for array-based computation and data manipulation.

For more information, see the [NumPy: Logical Functions](https://numpy.org/doc/stable/reference/routines.logic.html).

## 1. Truth Value Testing
Truth value testing in NumPy determines whether an array as a whole is considered `True` or `False` based on its elements.

Arrays raise an error when evaluated directly in a Boolean context because their truth value is ambiguous; instead, use methods like `numpy.any()` (to check if any element is `True`) or `numpy.all()` (to check if all elements are `True`) for explicit evaluation.

For more details, see the [Truth Value Testing](https://numpy.org/doc/stable/reference/routines.logic.html#truth-value-testing).



| Operation          | Function            | Description                                                     | Documentation |
|--------------------|---------------------|-----------------------------------------------------------------|---------------|
| **All**            | `np.all()`          | Tests if all array elements along a given axis evaluate to True | [Link](https://numpy.org/doc/stable/reference/generated/numpy.all.html#numpy.all) |
| **Any**            | `np.any()`          | Tests if any array element along a given axis evaluates to True | [Link](https://numpy.org/doc/stable/reference/generated/numpy.any.html#numpy.any) |


### 1.1 All (np.all)
The `np.all()` function in NumPy is used to check if all elements of an array evaluate to True, either across the entire
array or along a specific axis. This function is useful for validating conditions across large datasets, such as 
checking if all values meet a certain criteria, and can be applied to multi-dimensional arrays as well.

**Example:**
```python
import numpy as np

# Define a 2D array (matrix)
a = np.array([[True, False, True], [True, True, False]])

# Perform check if all elements are True using the np.all() function
result_function = np.all(a)

# Perform check if all elements are True along axis 0
result_axis0 = np.all(a, axis=0)

# Perform check if all elements are True along axis 1
result_axis1 = np.all(a, axis=1)

# Print Output
print("\n Check if all elements are True:\n", result_function)
print("\n Check if all elements are True along axis 0:\n", result_axis0)
print("\n Check if all elements are True along axis 1:\n", result_axis1)
```

### 1.2 Any (np.any)
The `np.any()` function in NumPy is used to check if any element in an array evaluates to `True`, either across the entire array or along a specific axis. This function is helpful for identifying if any condition is met within a dataset, such as checking for the presence of specific values or conditions.

**Example:**
```python
import numpy as np

# Define a 2D array (matrix)
a = np.array([[False, False, True], [False, True, False]])

# Perform check if any element is True using the np.any() function
result_function = np.any(a)

# Perform check if any element is True along axis 0
result_axis0 = np.any(a, axis=0)

# Perform check if any element is True along axis 1
result_axis1 = np.any(a, axis=1)

# Print Output
print("\n Check if any element is True:\n", result_function)
print("\n Check if any element is True along axis 0:\n", result_axis0)
print("\n Check if any element is True along axis 1:\n", result_axis1)
```


## 2. Array Contents
NumPy provides functions to evaluate the contents of an array, allowing checks for conditions such as whether elements are finite, infinite, NaN, or non-NaN.

Functions like `numpy.isfinite()`, `numpy.isinf()`, `numpy.isnan()`, and `numpy.isnat()` enable efficient and element-wise checks, making them useful for data validation and preprocessing.

For more details, see the [Array Contents](https://numpy.org/doc/stable/reference/routines.logic.html#array-contents).

| Operation               | Function                | Description                                                               | Documentation                                                                 |
|-------------------------|-------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **Is Finite**           | `np.isfinite()`         | Tests element-wise if numbers are finite (not infinite or NaN).           | [Link](https://numpy.org/doc/stable/reference/generated/numpy.isfinite.html)  |
| **Is Infinite**         | `np.isinf()`            | Tests element-wise if numbers are infinite.                               | [Link](https://numpy.org/doc/stable/reference/generated/numpy.isinf.html)     |
| **Is NaN**              | `np.isnan()`            | Tests element-wise if numbers are NaN (Not a Number).                     | [Link](https://numpy.org/doc/stable/reference/generated/numpy.isnan.html)     |
| **Is NAT (Not a Time)** | `np.isnat()`            | Tests element-wise if datetime elements are NaT (Not a Time).             | [Link](https://numpy.org/doc/stable/reference/generated/numpy.isnat.html)     |
| **Is Complex**          | `np.iscomplex()`        | Tests element-wise if numbers have an imaginary part.                     | [Link](https://numpy.org/doc/stable/reference/generated/numpy.iscomplex.html) |
| **Is Real**             | `np.isreal()`           | Tests element-wise if numbers are real (imaginary part is zero).          | [Link](https://numpy.org/doc/stable/reference/generated/numpy.isreal.html)    |
| **Is Complex Obj**      | `np.iscomplexobj()`     | Tests if the input is a complex object (e.g., complex dtype).             | [Link](https://numpy.org/doc/stable/reference/generated/numpy.iscomplexobj.html) |
| **Is Real Obj**         | `np.isrealobj()`        | Tests if the input is a real object (e.g., real dtype).                   | [Link](https://numpy.org/doc/stable/reference/generated/numpy.isrealobj.html) |

### 2.1 Is Finitie (np.isfinite)
The `np.isfinite()` function in NumPy checks whether each element of an array is finite, meaning it is neither `NaN` (Not a Number) nor `inf` (infinity). This function is useful for filtering or handling invalid data, ensuring that only valid numeric values are processed in calculations or analyses.

**Example:**
```python
import numpy as np

# Define a 2D array (matrix) with some NaN and infinite values
a = np.array([[1, 2, np.nan], [4, np.inf, 6]])

# Perform check for finite values using np.isfinite() function
result_function = np.isfinite(a)

# Print Output
print("\n Check if elements are finite using np.isfinite():\n", result_function)
```

### 2.2 Is Infinite (np.isinf)
The `np.isinf()` function in NumPy checks whether each element of an array is infinite, either positive or negative (`inf` or `-inf`). This function is useful for detecting and handling infinite values in datasets, especially when performing mathematical operations or data validation.

**Example:**
```python
import numpy as np

# Define a 2D array (matrix) with some infinite values
a = np.array([[1, 2, np.inf], [4, -np.inf, 6]])

# Perform check for infinite values using np.isinf() function
result_function = np.isinf(a)

# Print Output
print("\n Check if elements are infinite using np.isinf():\n", result_function)
```

### 2.3 Is NaN (np.isnan)
The `np.isnan()` function in NumPy checks whether each element of an array is `NaN` (Not a Number). This function is helpful for detecting missing or undefined values in datasets, allowing for proper handling or filtering during data analysis.

**Example:**
```python
import numpy as np

# Define a 2D array (matrix) with some NaN values
a = np.array([[1, 2, np.nan], [4, 5, 6]])

# Perform check for NaN values using np.isnan() function
result_function = np.isnan(a)

# Print Output
print("\n Check if elements are NaN using np.isnan():\n", result_function)
```

### 2.4 Is NaT (Not a Time) (np.isnat)
The `np.isnat()` function in NumPy checks whether each element in an array of datetime objects is a "Not a Time" (`NaT`) value. This is useful for detecting missing or invalid datetime entries in datasets, allowing for appropriate handling or filtering in time-based analyses.

**Example:**
```python
import numpy as np

# Define a 2D array (matrix) with some datetime values
a = np.array([['2024-01-01', '2024-02-01'], ['2024-03-01', 'NaT']], dtype='datetime64[D]')

# Perform check for "Not a Time" values using np.isnat() function
result_function = np.isnat(a)

# Print Output
print("\n Check if elements are 'Not a Time' using np.isnat():\n", result_function)
```

### 2.5 Is Complex (np.iscomplex)

The `np.iscomplex()` function in NumPy checks whether each element of an array is a complex number. This function is useful for identifying and handling complex-valued entries in datasets, especially when performing operations that require complex number detection.

**Example:**
```python
import numpy as np

# Define a 2D array (matrix) with complex numbers
a = np.array([[1+2j, 3, 5+6j], [7+8j, 9+10j, 11]])

# Perform check for complex numbers using np.iscomplex() function
result_function = np.iscomplex(a)

# Print Output
print("\n Check if elements are complex using np.iscomplex():\n", result_function)
```

### 2.6 Is Real (np.isreal)
The `np.isreal()` function in NumPy checks whether each element of an array is a real number, meaning it has no imaginary part. This function is useful for identifying and filtering real values from complex numbers in datasets when performing operations that only apply to real numbers.

**Example:**
```python
import numpy as np

# Define a 2D array (matrix) with both real and complex numbers
a = np.array([[1+2j, 3, 5+6j], [7, 9+10j, 11]])

# Perform check for real numbers using np.isreal() function
result_function = np.isreal(a)

# Print Output
print("\n Check if elements are real using np.isreal():\n", result_function)
```

### 2.7 Is Complex Obj (np.iscomplexobj)
The `np.iscomplexobj()` function in NumPy checks whether the given array contains complex numbers, returning `True` if any element is a complex number. This is useful for determining whether an array as a whole is of a complex type, which can influence how operations are performed on the array.

**Example:**
```python
import numpy as np

# Define a 2D array (matrix) with complex numbers
a = np.array([[1+2j, 3, 5+6j], [7, 9+10j, 11]])

# Perform check if the array contains complex numbers using np.iscomplexobj() function
result_function = np.iscomplexobj(a)

# Print Output
print("\n Check if the array contains complex numbers using np.iscomplexobj():\n", result_function)
```

### 2.8 Is Real Obj (np.isrealobj)
The `np.isrealobj()` function in NumPy checks whether the given array contains only real numbers, returning `True` if the array does not contain any complex values. This is useful for ensuring that operations are performed on arrays that are strictly real, and not complex, which can influence certain calculations and results.

**Example:**
```python
import numpy as np

# Define a 2D array (matrix) with real numbers
a = np.array([[1, 2, 3], [4, 5, 6]])

# Perform check if the array contains only real numbers using np.isrealobj() function
result_function = np.isrealobj(a)

# Print Output
print("\n Check if the array contains only real numbers using np.isrealobj():\n", result_function)

```

## 3. Array Type Testing

Array type testing in NumPy allows you to check the type or characteristics of an array's elements, such as whether they are scalar, complex, or real.

Functions like `np.isscalar()`, `np.iscomplexobj()`, and `np.isrealobj()` enable efficient checks to determine the array's data type properties and ensure compatibility with operations.

For more details, see the [Array Type Testing](https://numpy.org/doc/stable/reference/routines.logic.html#array-type-testing).

| Operation          | Function            | Description                                                              | Documentation                                                                 |
|--------------------|---------------------|--------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **Is Scalar**      | `np.isscalar()`     | Checks if the input is a scalar (not an array or sequence).              | [Link](https://numpy.org/doc/stable/reference/generated/numpy.isscalar.html)  |
| **Is Complex Obj** | `np.iscomplexobj()` | Checks if the input is a complex object (e.g., array with complex dtype). | [Link](https://numpy.org/doc/stable/reference/generated/numpy.iscomplexobj.html) |
| **Is Real Obj**    | `np.isrealobj()`    | Checks if the input is a real object (e.g., array with real dtype).       | [Link](https://numpy.org/doc/stable/reference/generated/numpy.isrealobj.html) |
| **Is Complex**     | `np.iscomplex()`    | Checks element-wise if numbers have an imaginary part.                   | [Link](https://numpy.org/doc/stable/reference/generated/numpy.iscomplex.html) |
| **Is Real**        | `np.isreal()`       | Checks element-wise if numbers are real (imaginary part is zero).         | [Link](https://numpy.org/doc/stable/reference/generated/numpy.isreal.html)    |

### 3.1 Is Scalar (np.isscalar)
The `np.isscalar()` function in NumPy checks whether the given input is a scalar (a single value, such as an integer, 
float, or string), rather than an array or other object. This is useful for validating inputs in functions or algorithms 
that require scalars instead of arrays or sequences.

**Example:**
```python
import numpy as np

# Define a scalar value
a = 42

# Perform check if the input is a scalar using np.isscalar() function
result_function = np.isscalar(a)

# Print Output
print("\n Check if the input is a scalar using np.isscalar():\n", result_function)

```

### 3.2 Is Complex Obj (np.iscomplexobj)
The `np.iscomplexobj()` function in NumPy checks whether an entire array is of a complex type, returning `True` if the 
array contains any complex numbers. This is particularly useful when working with datasets where you need to 
differentiate between real and complex-valued arrays for appropriate mathematical processing.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices), one with complex numbers
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([[7+1j, 8+2j, 9], [10, 11+3j, 12]])

# Check if the first array contains complex numbers using np.iscomplexobj() function
result_a = np.iscomplexobj(a)

# Check if the second array contains complex numbers using np.iscomplexobj() function
result_b = np.iscomplexobj(b)

# Print Output
print("\n Check if the first array contains complex numbers:\n", result_a)
print("\n Check if the second array contains complex numbers:\n", result_b)

```

### 3.3 Is Real Obj (np.isrealobj)
The `np.isrealobj()` function in NumPy checks whether an array contains only real numbers, returning `True` if the 
array does not include any complex numbers. This is useful for verifying that an array is strictly real-valued, 
especially when performing operations that require non-complex inputs.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices), one with only real numbers
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([[7, 8, 9], [10, 11, 12+1j]])

# Check if the first array contains only real numbers using np.isrealobj() function
result_a = np.isrealobj(a)

# Check if the second array contains only real numbers using np.isrealobj() function
result_b = np.isrealobj(b)

# Print Output
print("\n Check if the first array contains only real numbers:\n", result_a)
print("\n Check if the second array contains only real numbers:\n", result_b)
```


### 3.4 Is Complex (np.iscomplex)
The `np.iscomplex()` function in NumPy checks each element of an array to determine if it is a complex number, returning 
a Boolean array of the same shape. This is useful for identifying specific elements with an imaginary component in 
datasets, enabling targeted operations on complex-valued entries.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices), one with complex numbers
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([[7+1j, 8, 9], [10, 11+2j, 12]])

# Check for complex numbers element-wise in the first array using np.iscomplex() function
result_a = np.iscomplex(a)

# Check for complex numbers element-wise in the second array using np.iscomplex() function
result_b = np.iscomplex(b)

# Print Output
print("\n Check for complex numbers in the first array:\n", result_a)
print("\n Check for complex numbers in the second array:\n", result_b)

```

### 3.5 Is Real (np.isreal)
The `np.isreal()` function in NumPy checks each element of an array to determine if it is a real number (i.e., it has 
no imaginary component), returning a Boolean array of the same shape. This is particularly useful for distinguishing 
purely real values from complex numbers in arrays, especially in datasets that may contain mixed numerical types.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices), one with only real numbers
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([[7, 8+1j, 9], [10, 11, 12]])

# Check for real numbers element-wise in the first array using np.isreal() function
result_a = np.isreal(a)

# Check for real numbers element-wise in the second array using np.isreal() function
result_b = np.isreal(b)

# Print Output
print("\n Check for real numbers in the first array:\n", result_a)
print("\n Check for real numbers in the second array:\n", result_b)

```

## 4. Logical Operations

Logical operations in NumPy provide element-wise functionality to perform Boolean operations such as AND, OR, NOT, and XOR on arrays.

Functions like `np.logical_and()`, `np.logical_or()`, `np.logical_not()`, and `np.logical_xor()` are essential for evaluating conditions and creating masks for filtering or modifying data.

For more details, see the [Logical Operations](https://numpy.org/doc/stable/reference/routines.logic.html#logical-operations).

| Operation          | Function              | Operator | Description                                                     | Documentation                                                                 |
|--------------------|-----------------------|----------|-----------------------------------------------------------------|-------------------------------------------------------------------------------|
| **Logical AND**    | `np.logical_and()`    | &        | Computes the element-wise logical AND operation.                | [Link](https://numpy.org/doc/stable/reference/generated/numpy.logical_and.html) |
| **Logical OR**     | `np.logical_or()`     | \|       | Computes the element-wise logical OR operation.                 | [Link](https://numpy.org/doc/stable/reference/generated/numpy.logical_or.html)  |
| **Logical NOT**    | `np.logical_not()`    | ~        | Computes the element-wise logical NOT operation.                | [Link](https://numpy.org/doc/stable/reference/generated/numpy.logical_not.html) |
| **Logical XOR**    | `np.logical_xor()`    | ^        | Computes the element-wise logical XOR (exclusive OR) operation. | [Link](https://numpy.org/doc/stable/reference/generated/numpy.logical_xor.html) |


### 4.1 Logical AND (np.logical_and)
The `np.logical_and()` function in NumPy performs an element-wise logical `AND` operation, returning `True` only where 
both corresponding elements in the input arrays are True. This function is useful for combining conditions in datasets, 
especially when creating masks for filtering or processing data based on multiple criteria.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices) with Boolean values
a = np.array([[True, False, True], [False, True, False]])
b = np.array([[True, True, False], [False, False, True]])

# Perform logical AND operation using the & operator
result_operator = a & b

# Perform logical AND operation using np.logical_and function
result_function = np.logical_and(a, b)

# Print Output
print("\n Logical AND using & operator:\n", result_operator)
print("\n Logical AND using np.logical_and():\n", result_function)
```

### 4.2 Logical OR (np.logical_or)

The `np.logical_or()` function in NumPy performs an element-wise logical `OR` operation, returning True if at least one 
of the corresponding elements in the input arrays is True. This function is commonly used to combine conditions in 
datasets, enabling flexible filtering or decision-making based on multiple criteria.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices) with Boolean values
a = np.array([[True, False, True], [False, True, False]])
b = np.array([[False, True, False], [True, False, True]])

# Perform logical OR operation using the | operator
result_operator = a | b

# Perform logical OR operation using np.logical_or function
result_function = np.logical_or(a, b)

# Print Output
print("\n Logical OR using | operator:\n", result_operator)
print("\n Logical OR using np.logical_or():\n", result_function)
```

### 4.3 Logical NOT (np.logical_not)
The `np.logical_not()` function in NumPy performs an element-wise logical `NOT` operation, inverting the Boolean values 
in an array (True becomes False and vice versa). This is useful for creating masks or reversing conditions in datasets, 
enabling flexible logical operations for filtering or data manipulation.

**Example:**
```python
import numpy as np

# Define a 2D array (matrix) with Boolean values
a = np.array([[True, False, True], [False, True, False]])

# Perform logical NOT operation using the ~ operator
result_operator = ~a

# Perform logical NOT operation using np.logical_not function
result_function = np.logical_not(a)

# Print Output
print("\n Logical NOT using ~ operator:\n", result_operator)
print("\n Logical NOT using np.logical_not():\n", result_function)
```

### 4.4 Logical XOR (np.logical_xor)
The `np.logical_xor()` function in NumPy performs an element-wise logical `XOR` (exclusive OR) operation, returning 
`True` only if exactly one of the corresponding elements in the input arrays is True. This is useful for identifying 
mutually exclusive conditions in datasets, where a condition must hold in one array but not in the other.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices) with Boolean values
a = np.array([[True, False, True], [False, True, False]])
b = np.array([[False, True, True], [True, False, False]])

# Perform logical XOR operation using the ^ operator
result_operator = a ^ b

# Perform logical XOR operation using np.logical_xor function
result_function = np.logical_xor(a, b)

# Print Output
print("\n Logical XOR using ^ operator:\n", result_operator)
print("\n Logical XOR using np.logical_xor():\n", result_function)
```

## 5. Comparison

Comparisons in NumPy allow element-wise comparison of arrays, producing Boolean results based on relational operators like equal to, greater than, or less than.

Functions such as `np.equal()`, `np.not_equal()`, `np.less()`, and `np.greater()` are commonly used for these comparisons, enabling efficient filtering and conditional operations on arrays.

For more details, see the [Comparison](https://numpy.org/doc/stable/reference/routines.logic.html#comparison).

| Operation                 | Function               | Operator | Description                                                                         | Documentation                                                                     |
|---------------------------|------------------------|----------|-------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| **Equal**                 | `np.equal()`           | ==       | Tests element-wise if values are equal.                                             | [Link](https://numpy.org/doc/stable/reference/generated/numpy.equal.html)         |
| **Not Equal**             | `np.not_equal()`       | !=       | Tests element-wise if values are not equal.                                         | [Link](https://numpy.org/doc/stable/reference/generated/numpy.not_equal.html)     |
| **Less Than**             | `np.less()`            | <        | Tests element-wise if values are less than the given value.                         | [Link](https://numpy.org/doc/stable/reference/generated/numpy.less.html)          |
| **Less Than or Equal**    | `np.less_equal()`      | <=       | Tests element-wise if values are less than or equal to the given value.             | [Link](https://numpy.org/doc/stable/reference/generated/numpy.less_equal.html)    |
| **Greater Than**          | `np.greater()`         | >        | Tests element-wise if values are greater than the given value.                      | [Link](https://numpy.org/doc/stable/reference/generated/numpy.greater.html)       |
| **Greater Than or Equal** | `np.greater_equal()`   | >=       | Tests element-wise if values are greater than or equal to the given value.          | [Link](https://numpy.org/doc/stable/reference/generated/numpy.greater_equal.html) |
| **All Close**             | `np.allclose()`        |          | Returns True if two arrays are element-wise equal within a tolerance.               | [Link](https://numpy.org/doc/stable/reference/generated/numpy.allclose.html)      |
| **Is Close**              | `np.isclose()`         |          | Returns a boolean array where two arrays are element-wise equal within a tolerance. | [Link](https://numpy.org/doc/stable/reference/generated/numpy.isclose.html)       |
| **Array Equal**           | `np.array_equal()`     |          | True if two arrays have the same shape and elements, False otherwise.               | [Link](https://numpy.org/doc/stable/reference/generated/numpy.array_equal.html)   |
| **Array Equivalent**      | `np.array_equiv()`     |          | Returns True if input arrays are shape consistent and all elements equal.           | [Link](https://numpy.org/doc/stable/reference/generated/numpy.array_equiv.html)   |


### 5.1 Equal (np.equal)
The `np.equal()` function in NumPy performs an element-wise comparison between two arrays, returning `True` where the 
corresponding elements are equal and False otherwise. This is useful for identifying matches in datasets, enabling 
operations like filtering or validating data against reference values.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices)
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([[1, 8, 3], [10, 5, 6]])

# Perform element-wise equality check using the == operator
result_operator = a == b

# Perform element-wise equality check using np.equal function
result_function = np.equal(a, b)

# Print Output
print("\n Element-wise equality using == operator:\n", result_operator)
print("\n Element-wise equality using np.equal():\n", result_function)
```

### 5.2 Not Equal (np.not_equal)
The `np.not_equal()` function in NumPy performs an element-wise comparison between two arrays, returning `True` where 
the corresponding elements are not equal and `False` otherwise. This is useful for identifying mismatches in datasets, 
enabling operations like filtering or validating data against expected values.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices)
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([[1, 8, 3], [10, 5, 7]])

# Perform element-wise inequality check using the != operator
result_operator = a != b

# Perform element-wise inequality check using np.not_equal function
result_function = np.not_equal(a, b)

# Print Output
print("\n Element-wise inequality using != operator:\n", result_operator)
print("\n Element-wise inequality using np.not_equal():\n", result_function)
```

### 5.3 Less Than (np.less)
The `np.less()` function in NumPy performs an element-wise comparison between two arrays, returning `True` where the 
corresponding element in the first array is less than the element in the second array, and `False` otherwise. This is 
useful for identifying elements that meet a specific condition, such as finding values below a threshold or performing 
comparisons between datasets.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices)
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([[7, 2, 9], [3, 11, 6]])

# Perform element-wise less-than check using the < operator
result_operator = a < b

# Perform element-wise less-than check using np.less function
result_function = np.less(a, b)

# Print Output
print("\n Element-wise less-than using < operator:\n", result_operator)
print("\n Element-wise less-than using np.less():\n", result_function)
```

### 5.4 Less Than or Equal (np.less_equal)
The `np.less_equal()` function in NumPy performs an element-wise comparison between two arrays, returning `True` where 
the elements in the first array are less than or equal to the corresponding elements in the second array, and `False` 
otherwise. This is useful for checking conditions that involve both equality and inequality, such as identifying 
elements within a range or validating threshold limits.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices)
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([[3, 2, 9], [4, 11, 6]])

# Perform element-wise less-than-or-equal check using the <= operator
result_operator = a <= b

# Perform element-wise less-than-or-equal check using np.less_equal function
result_function = np.less_equal(a, b)

# Print Output
print("\n Element-wise less-than-or-equal using <= operator:\n", result_operator)
print("\n Element-wise less-than-or-equal using np.less_equal():\n", result_function)

```

### 5.5 Greater Than (np.greater)
The `np.greater()` function in NumPy performs an element-wise comparison between two arrays, returning `True` where the 
elements in the first array are greater than the corresponding elements in the second array, and `False` otherwise. This 
is useful for identifying elements that exceed a specific threshold or comparing datasets for conditions involving 
strict inequality.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices)
a = np.array([[1, 5, 3], [8, 5, 6]])
b = np.array([[7, 2, 9], [4, 11, 6]])

# Perform element-wise greater-than check using the > operator
result_operator = a > b

# Perform element-wise greater-than check using np.greater function
result_function = np.greater(a, b)

# Print Output
print("\n Element-wise greater-than using > operator:\n", result_operator)
print("\n Element-wise greater-than using np.greater():\n", result_function)
```

### 5.6 Greater Than or Equal (np.greater_equal)
The `np.greater_equal()` function in NumPy performs an element-wise comparison between two arrays, returning `True` 
where the elements in the first array are greater than or equal to the corresponding elements in the second array, and 
`False` otherwise. This is useful for identifying elements that meet or exceed a threshold or for validating conditions 
that include both equality and inequality.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices)
a = np.array([[1, 5, 3], [8, 5, 6]])
b = np.array([[7, 5, 3], [4, 11, 6]])

# Perform element-wise greater-than-or-equal check using the >= operator
result_operator = a >= b

# Perform element-wise greater-than-or-equal check using np.greater_equal function
result_function = np.greater_equal(a, b)

# Print Output
print("\n Element-wise greater-than-or-equal using >= operator:\n", result_operator)
print("\n Element-wise greater-than-or-equal using np.greater_equal():\n", result_function)

```

### 5.7 All Close (np.allclose)
The `np.allclose()` function in NumPy checks whether two arrays are element-wise equal within a specified tolerance, 
returning `True` if all elements are sufficiently close and `False` otherwise. This is particularly useful for 
comparing floating-point arrays where small numerical differences might exist due to rounding or computation errors.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices) with slight differences
a = np.array([[1.0, 2.0, 3.0], [4.0, 5.0, 6.0]])
b = np.array([[1.0, 2.0001, 3.0], [4.0, 5.0, 6.0001]])

# Check if all elements are close within a tolerance using np.allclose() function
result_function = np.allclose(a, b, rtol=1e-05, atol=1e-08)

# Print Output
print("\n Check if all elements are close using np.allclose():\n", result_function)

```

### 5.8 Is Close (np.isclose)
The `np.isclose()` function in NumPy performs an element-wise comparison between two arrays, returning a Boolean array 
indicating whether each pair of elements is approximately equal within a specified tolerance. This is useful for 
identifying individual differences between floating-point arrays where small variations may arise due to rounding or 
computation errors.

**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices) with slight differences
a = np.array([[1.0, 2.0, 3.0], [4.0, 5.0, 6.0]])
b = np.array([[1.0, 2.0001, 3.0], [4.0, 5.0, 6.0001]])

# Check element-wise closeness within a tolerance using np.isclose() function
result_function = np.isclose(a, b, rtol=1e-05, atol=1e-08)

# Print Output
print("\n Element-wise closeness using np.isclose():\n", result_function)

```

### 5.9 Array Equal (np.array_equal)
The `np.array_equal()` function in NumPy checks whether two arrays are exactly equal in both shape and content, 
returning `True` if they match and `False` otherwise. This is useful for validating that two arrays are identical, 
including their dimensions and all corresponding elements.


**Example:**
```python
import numpy as np

# Define two 2D arrays (matrices)
a = np.array([[1, 2, 3], [4, 5, 6]])
b = np.array([[1, 2, 3], [4, 5, 6]])

# Check if the arrays are exactly equal using np.array_equal() function
result_function = np.array_equal(a, b)

# Print Output
print("\n Check if arrays are exactly equal using np.array_equal():\n", result_function)

```

### 5.10 Array Equivalent (np.array_equiv)
The `np.array_equiv()` function in NumPy checks whether two arrays are equivalent, meaning they have the same shape or 
are broadcastable to the same shape, and all corresponding elements are equal. This is useful for validating array 
content consistency, even when the dimensions differ but can be aligned via broadcasting.

**Example:**
```python
import numpy as np

# Define two arrays
a = np.array([[1, 2, 3], [1, 2, 3]])
b = np.array([1, 2, 3])

# Check if the arrays are equivalent using np.array_equiv() function
result_function = np.array_equiv(a, b)

# Print Output
print("\n Check if arrays are equivalent using np.array_equiv():\n", result_function)

```


## Summary
NumPy's logical functions are integral when working with arrays that require conditional evaluations, filtering, or masking. These functions are commonly used in scenarios such as data cleaning, where elements need to be checked for specific conditions.

Logical operations like AND, OR, and NOT can be combined to create complex conditions for array manipulation. These tools are also valuable for efficient element-wise comparisons, handling Boolean arrays, and applying logical filters.

In conclusion, NumPy's logical functions streamline operations on large datasets, enabling precise control and manipulation based on conditions. 