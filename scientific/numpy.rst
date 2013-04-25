Numpy basics
============

Numpy is a package that allows us to create multi-dimensional arrays, and a
large fraction of Numpy is written in C, providing very fast array operations
within Python.

Making arrays
-------------

Arrays can be created in different ways::

  >>> import numpy as np

  >>> a = np.array([10, 20, 30, 40])  # create an array from a list of values
  >>> a
  array([10, 20, 30, 40]

  >>> b = np.arange(4)  # create an array of 4 integers, from 0 to 3
  >>> b
  array([0, 1, 2, 3]),

  >>> np.arange(0.0, 10.0, 0.1)  # create a float array from 0 to 100 stepping by 0.1
  array([ 0. ,  0.1,  0.2,  0.3,  0.4,  0.5,  0.6,  0.7,  0.8,  0.9,  1. ,
          1.1,  1.2,  1.3,  1.4,  1.5,  1.6,  1.7,  1.8,  1.9,  2. ,  2.1,
          2.2,  2.3,  2.4,  2.5,  2.6,  2.7,  2.8,  2.9,  3. ,  3.1,  3.2,
          3.3,  3.4,  3.5,  3.6,  3.7,  3.8,  3.9,  4. ,  4.1,  4.2,  4.3,
          4.4,  4.5,  4.6,  4.7,  4.8,  4.9,  5. ,  5.1,  5.2,  5.3,  5.4,
          5.5,  5.6,  5.7,  5.8,  5.9,  6. ,  6.1,  6.2,  6.3,  6.4,  6.5,
          6.6,  6.7,  6.8,  6.9,  7. ,  7.1,  7.2,  7.3,  7.4,  7.5,  7.6,
          7.7,  7.8,  7.9,  8. ,  8.1,  8.2,  8.3,  8.4,  8.5,  8.6,  8.7,
          8.8,  8.9,  9. ,  9.1,  9.2,  9.3,  9.4,  9.5,  9.6,  9.7,  9.8,
          9.9]),

  >>> np.linspace(-np.pi, np.pi, 5)  # create an array of 5 evenly spaced samples from -pi to pi
  array([-3.14159265, -1.57079633,  0.        ,  1.57079633,  3.14159265]))

New arrays can be obtained by operating with existing arrays::

  >>> a + b**2  # elementwise operations
  array([10, 21, 34, 49])

Arrays may have more than one dimension::

  >>> f = np.ones([3, 4])  # 3 x 4 float array of ones
  >>> f
  array([[ 1.,  1.,  1.,  1.],
         [ 1.,  1.,  1.,  1.],
         [ 1.,  1.,  1.,  1.]]),

  >>> g = np.zeros([2, 3, 4], dtype=int)  # 3 x 4 x 5 int array of zeros
  array([[[0, 0, 0, 0],
          [0, 0, 0, 0],
          [0, 0, 0, 0]],
         [[0, 0, 0, 0],
          [0, 0, 0, 0],
          [0, 0, 0, 0]]]),

  >>> i = np.zeros_like(f)  # array of zeros with same shape/type as f
  array([[ 0.,  0.,  0.,  0.],
         [ 0.,  0.,  0.,  0.],
         [ 0.,  0.,  0.,  0.]]))

You can change the dimensions of existing arrays::

  >>> w = np.arange(12)
  >>> w.shape = [3, 4]  # does not modify the total number of elements
  array([[ 0,  1,  2,  3],
         [ 4,  5,  6,  7],
         [ 8,  9, 10, 11]]),

  >>> x = np.arange(5)
  >>> x
  array([0, 1, 2, 3, 4]),

  >>> y = x.reshape(5, 1)
  >>> y = x.reshape(-1, 1)  # Same thing but Numpy figures out correct length
  >>> y
  array([[0],
         [1],
         [2],
         [3],
         [4]]))

It is possible to operate with arrays of different dimensions as long as they fit well (broadcasting)::

  >>> x + y * 10
  array([[ 0,  1,  2,  3,  4],
         [10, 11, 12, 13, 14],
         [20, 21, 22, 23, 24],
         [30, 31, 32, 33, 34],
         [40, 41, 42, 43, 44]])

Array access and slicing
------------------------

Numpy provides powerful methods for accessing array elements or particular subsets of an array,
e.g. the 4th column or every other row.  This is called slicing.  The outputs
below illustrate basic slicing, but you don't need to type these examples.
The ">>>" indicates the input to Python::

   >>> a = np.arange(20).reshape(4,5)
   >>> a
   array([[ 0,  1,  2,  3,  4],
         [ 5,  6,  7,  8,  9],
         [10, 11, 12, 13, 14],
         [15, 16, 17, 18, 19]])

   >>> a[2, 3]  # select element in row 2, col 3 (counting from 0)
   13

   >>> a[2, :]  # select every element in row 2
   array([10, 11, 12, 13, 14])

   >>> a[:, 0]  # select every element in col 0
   array([ 0,  5, 10, 15])

   >>> a[0:3, 1:3]
   array([[ 1,  2],
          [ 6,  7],
          [11, 12]])

Numpy arrays vs Python lists
----------------------------

The main differences between Numpy arrays and Python lists are the following:

    * Python lists can contain anything, including other lists, objects, or
      complex data structures.
    * When you slice a Python list it returns a copy, whereas slicing a Numpy
      array returns a reference
    * Vector math does not work on lists. For example, multiplying a list by
      an int ``n`` gives ``n`` copies of the list, adding another list
      concatentates, and multiplying by a float gives an error.
