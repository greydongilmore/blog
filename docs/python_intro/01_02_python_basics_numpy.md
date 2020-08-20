---
title: Numpy
template: overrides/main.html
---

NumPy (or Numpy) is a Linear Algebra Library for Python, the reason it is so important for Data Science with Python is that almost all of the libraries in the PyData Ecosystem rely on NumPy as one of their main building blocks.

Numpy is also incredibly fast, as it has bindings to C libraries. For more info on why you would want to use Arrays instead of lists, check out this great [StackOverflow post](http://stackoverflow.com/questions/993984/why-numpy-instead-of-python-lists).

We will only learn the basics of NumPy, to get started we need to install it!

## Using NumPy

Once you've installed NumPy you can import it as a library:

```python
import numpy as np
```

Numpy has many built-in functions and capabilities. We won't cover them all but instead we will focus on some of the most important aspects of Numpy: vectors,arrays,matrices, and number generation. Let's start by discussing arrays.

## Numpy Arrays

NumPy arrays are the main way we will use Numpy throughout the course. Numpy arrays essentially come in two flavors: vectors and matrices. Vectors are strictly 1-d arrays and matrices are 2-d (but you should note a matrix can still have only one row or one column).

Let's begin our introduction by exploring how to create NumPy arrays.

### From a Python List

We can create an array by directly converting a list or list of lists:

```python
my_list = [1,2,3]
my_list
```

    [1, 2, 3]

```python
np.array(my_list)
```

    array([1, 2, 3])

```python
my_matrix = [[1,2,3],[4,5,6],[7,8,9]]
my_matrix
```

    [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

```python
np.array(my_matrix)
```

    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])

## Built-in Methods

There are lots of built-in ways to generate Arrays

### arange

Return evenly spaced values within a given interval.

```python
np.arange(0,10)
```

    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

```python
np.arange(0,11,2)
```

    array([ 0,  2,  4,  6,  8, 10])

### zeros and ones

Generate arrays of zeros or ones

```python
np.zeros(3)
```

    array([0., 0., 0.])

```python
np.zeros((5,5))
```

    array([[0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.],
           [0., 0., 0., 0., 0.]])

```python
np.ones(3)
```

    array([1., 1., 1.])

```python
np.ones((3,3))
```

    array([[1., 1., 1.],
           [1., 1., 1.],
           [1., 1., 1.]])

### linspace

Return evenly spaced numbers over a specified interval.

```python
np.linspace(0,10,3)
```

    array([ 0.,  5., 10.])

```python
np.linspace(0,10,50)
```

    array([ 0.        ,  0.20408163,  0.40816327,  0.6122449 ,  0.81632653,
            1.02040816,  1.2244898 ,  1.42857143,  1.63265306,  1.83673469,
            2.04081633,  2.24489796,  2.44897959,  2.65306122,  2.85714286,
            3.06122449,  3.26530612,  3.46938776,  3.67346939,  3.87755102,
            4.08163265,  4.28571429,  4.48979592,  4.69387755,  4.89795918,
            5.10204082,  5.30612245,  5.51020408,  5.71428571,  5.91836735,
            6.12244898,  6.32653061,  6.53061224,  6.73469388,  6.93877551,
            7.14285714,  7.34693878,  7.55102041,  7.75510204,  7.95918367,
            8.16326531,  8.36734694,  8.57142857,  8.7755102 ,  8.97959184,
            9.18367347,  9.3877551 ,  9.59183673,  9.79591837, 10.        ])

### eye

Creates an identity matrix

```python
np.eye(4)
```

    array([[1., 0., 0., 0.],
           [0., 1., 0., 0.],
           [0., 0., 1., 0.],
           [0., 0., 0., 1.]])

## Random 

Numpy also has lots of ways to create random number arrays:

### rand

Create an array of the given shape and populate it with random samples from a uniform distribution over ``[0, 1)``.

```python
np.random.rand(2)
```

    array([0.48986762, 0.01468397])

```python
np.random.rand(5,5)
```

    array([[0.49717583, 0.85567488, 0.94414447, 0.66025653, 0.85163724],
           [0.32891759, 0.74810469, 0.16001041, 0.77051371, 0.88918009],
           [0.74608104, 0.58533077, 0.40581863, 0.25006859, 0.79847227],
           [0.06457888, 0.14487206, 0.72442204, 0.62528167, 0.73544863],
           [0.38535387, 0.7203514 , 0.34161177, 0.99193526, 0.79151416]])

### randn

Return a sample (or samples) from the "standard normal" distribution. Unlike rand which is uniform:

```python
np.random.randn(2)
```

    array([-1.31222401,  1.20662849])

```python
np.random.randn(5,5)
```

    array([[ 0.05155323, -2.03255688,  1.09044905,  1.37866648, -0.43513118],
           [-0.113966  ,  0.06371491, -0.58679889,  0.32057308, -1.90984774],
           [ 0.44065855, -0.93779379,  1.61012331, -1.21481517,  1.65470737],
           [ 1.31027626,  0.15909068,  0.85816313, -0.91927387,  1.13879634],
           [-0.18915251, -0.48102558,  0.38557437,  1.03093896,  2.00252213]])

### randint

Return random integers from `low` (inclusive) to `high` (exclusive).

```python
np.random.randint(1,100)
```

    42

```python
np.random.randint(1,100,10)
```

    array([73, 70, 12, 99, 69, 26, 10, 41, 92,  6])

## Array Attributes and Methods

Let's discuss some useful attributes and methods or an array:

```python
arr = np.arange(25)
ranarr = np.random.randint(0,50,10)
```

```python
arr
```

    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
           17, 18, 19, 20, 21, 22, 23, 24])

```python
ranarr
```

    array([29, 42, 21, 45, 11, 47, 46, 43, 25, 19])

### Reshape

Returns an array containing the same data with a new shape.

```python
arr.reshape(5,5)
```

    array([[ 0,  1,  2,  3,  4],
           [ 5,  6,  7,  8,  9],
           [10, 11, 12, 13, 14],
           [15, 16, 17, 18, 19],
           [20, 21, 22, 23, 24]])

### max,min,argmax,argmin

These are useful methods for finding max or min values. Or to find their index locations using argmin or argmax

```python
ranarr
```

    array([29, 42, 21, 45, 11, 47, 46, 43, 25, 19])

```python
ranarr.max()
```

    47

```python
ranarr.argmax()
```

    5

```python
ranarr.min()
```

    11

```python
ranarr.argmin()
```

    4

### Shape

Shape is an attribute that arrays have (not a method):

```python
# Vector
arr.shape
```

    (25,)

```python
# Notice the two sets of brackets
arr.reshape(1,25)
```

    array([[ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15,
            16, 17, 18, 19, 20, 21, 22, 23, 24]])

```python
arr.reshape(1,25).shape
```

    (1, 25)

```python
arr.reshape(25,1)
```

    array([[ 0],
           [ 1],
           [ 2],
           [ 3],
           [ 4],
           [ 5],
           [ 6],
           [ 7],
           [ 8],
           [ 9],
           [10],
           [11],
           [12],
           [13],
           [14],
           [15],
           [16],
           [17],
           [18],
           [19],
           [20],
           [21],
           [22],
           [23],
           [24]])

```python
arr.reshape(25,1).shape
```

    (25, 1)

### dtype

You can also grab the data type of the object in the array:

```python
arr.dtype
```

    dtype('int64')

## NumPy Indexing and Selection

In this section we will discuss how to select elements or groups of elements from an array.

```python
import numpy as np
```

```python
#Creating sample array
arr = np.arange(0,11)
```

```python
#Show
arr
```

    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10])

### Bracket Indexing and Selection

The simplest way to pick one or some elements of an array looks very similar to python lists:

```python
#Get a value at an index
arr[8]
```

    8

```python
#Get values in a range
arr[1:5]
```

    array([1, 2, 3, 4])

```python
#Get values in a range
arr[0:5]
```

    array([0, 1, 2, 3, 4])

### Broadcasting

Numpy arrays differ from a normal Python list because of their ability to broadcast:

```python
#Setting a value with index range (Broadcasting)
arr[0:5]=100

#Show
arr
```

    array([100, 100, 100, 100, 100,   5,   6,   7,   8,   9,  10])

```python
# Reset array, we'll see why I had to reset in  a moment
arr = np.arange(0,11)

#Show
arr
```

    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10])

```python
#Important notes on Slices
slice_of_arr = arr[0:6]

#Show slice
slice_of_arr
```

    array([0, 1, 2, 3, 4, 5])

```python
#Change Slice
slice_of_arr[:]=99

#Show Slice again
slice_of_arr
```

    array([99, 99, 99, 99, 99, 99])

Now note the changes also occur in our original array!

```python
arr
```

    array([99, 99, 99, 99, 99, 99,  6,  7,  8,  9, 10])

Data is not copied, it's a view of the original array! This avoids memory problems!

```python
#To get a copy, need to be explicit
arr_copy = arr.copy()

arr_copy
```

    array([99, 99, 99, 99, 99, 99,  6,  7,  8,  9, 10])

### Indexing a 2D array (matrices)

The general format is **arr_2d[row][col]** or **arr_2d[row,col]**. I recommend usually using the comma notation for clarity.

```python
arr_2d = np.array(([5,10,15],[20,25,30],[35,40,45]))

#Show
arr_2d
```

    array([[ 5, 10, 15],
           [20, 25, 30],
           [35, 40, 45]])

```python
#Indexing row
arr_2d[1]

```
    array([20, 25, 30])

```python
# Format is arr_2d[row][col] or arr_2d[row,col]

# Getting individual element value
arr_2d[1][0]
```

20




```python
# Getting individual element value
arr_2d[1,0]
```




    20




```python
# 2D array slicing

#Shape (2,2) from top right corner
arr_2d[:2,1:]
```




    array([[10, 15],
           [25, 30]])




```python
#Shape bottom row
arr_2d[2]
```




    array([35, 40, 45])




```python
#Shape bottom row
arr_2d[2,:]
```




    array([35, 40, 45])



### Fancy Indexing

Fancy indexing allows you to select entire rows or columns out of order,to show this, let's quickly build out a numpy array:


```python
#Set up matrix
arr2d = np.zeros((10,10))
```


```python
#Length of array
arr_length = arr2d.shape[1]
```


```python
#Set up array

for i in range(arr_length):
    arr2d[i] = i
    
arr2d
```




    array([[0., 0., 0., 0., 0., 0., 0., 0., 0., 0.],
           [1., 1., 1., 1., 1., 1., 1., 1., 1., 1.],
           [2., 2., 2., 2., 2., 2., 2., 2., 2., 2.],
           [3., 3., 3., 3., 3., 3., 3., 3., 3., 3.],
           [4., 4., 4., 4., 4., 4., 4., 4., 4., 4.],
           [5., 5., 5., 5., 5., 5., 5., 5., 5., 5.],
           [6., 6., 6., 6., 6., 6., 6., 6., 6., 6.],
           [7., 7., 7., 7., 7., 7., 7., 7., 7., 7.],
           [8., 8., 8., 8., 8., 8., 8., 8., 8., 8.],
           [9., 9., 9., 9., 9., 9., 9., 9., 9., 9.]])



Fancy indexing allows the following


```python
arr2d[[2,4,6,8]]
```




    array([[2., 2., 2., 2., 2., 2., 2., 2., 2., 2.],
           [4., 4., 4., 4., 4., 4., 4., 4., 4., 4.],
           [6., 6., 6., 6., 6., 6., 6., 6., 6., 6.],
           [8., 8., 8., 8., 8., 8., 8., 8., 8., 8.]])




```python
#Allows in any order
arr2d[[6,4,2,7]]
```




    array([[6., 6., 6., 6., 6., 6., 6., 6., 6., 6.],
           [4., 4., 4., 4., 4., 4., 4., 4., 4., 4.],
           [2., 2., 2., 2., 2., 2., 2., 2., 2., 2.],
           [7., 7., 7., 7., 7., 7., 7., 7., 7., 7.]])



## More Indexing Help
Indexing a 2d matrix can be a bit confusing at first, especially when you start to add in step size. Try google image searching NumPy indexing to fins useful images, like this one:

<img src= 'http://memory.osu.edu/classes/python/_images/numpy_indexing.png' width=500/>

## Selection

Let's briefly go over how to use brackets for selection based off of comparison operators.


```python
arr = np.arange(1,11)
arr
```




    array([ 1,  2,  3,  4,  5,  6,  7,  8,  9, 10])




```python
arr > 4
```




    array([False, False, False, False,  True,  True,  True,  True,  True,
            True])




```python
bool_arr = arr>4
```


```python
bool_arr
```




    array([False, False, False, False,  True,  True,  True,  True,  True,
            True])




```python
arr[bool_arr]
```




    array([ 5,  6,  7,  8,  9, 10])




```python
arr[arr>2]
```




    array([ 3,  4,  5,  6,  7,  8,  9, 10])




```python
x = 2
arr[arr>x]
```




    array([ 3,  4,  5,  6,  7,  8,  9, 10])


## Arithmetic

You can easily perform array with array arithmetic, or scalar with array arithmetic. Let's see some examples:


```python
import numpy as np
arr = np.arange(0,10)
```


```python
arr + arr
```




    array([ 0,  2,  4,  6,  8, 10, 12, 14, 16, 18])




```python
arr * arr
```




    array([ 0,  1,  4,  9, 16, 25, 36, 49, 64, 81])




```python
arr - arr
```




    array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0])




```python
# Warning on division by zero, but not an error!
# Just replaced with nan
arr/arr
```

    /home/ggilmore/.local/lib/python3.6/site-packages/ipykernel_launcher.py:3: RuntimeWarning: invalid value encountered in true_divide
      This is separate from the ipykernel package so we can avoid doing imports until





    array([nan,  1.,  1.,  1.,  1.,  1.,  1.,  1.,  1.,  1.])




```python
# Also warning, but not an error instead infinity
1/arr
```

    /home/ggilmore/.local/lib/python3.6/site-packages/ipykernel_launcher.py:2: RuntimeWarning: divide by zero encountered in true_divide
      





    array([       inf, 1.        , 0.5       , 0.33333333, 0.25      ,
           0.2       , 0.16666667, 0.14285714, 0.125     , 0.11111111])




```python
arr**3
```




    array([  0,   1,   8,  27,  64, 125, 216, 343, 512, 729])



## Universal Array Functions

Numpy comes with many [universal array functions](http://docs.scipy.org/doc/numpy/reference/ufuncs.html), which are essentially just mathematical operations you can use to perform the operation across the array. Let's show some common ones:


```python
#Taking Square Roots
np.sqrt(arr)
```




    array([0.        , 1.        , 1.41421356, 1.73205081, 2.        ,
           2.23606798, 2.44948974, 2.64575131, 2.82842712, 3.        ])




```python
#Calcualting exponential (e^)
np.exp(arr)
```




    array([1.00000000e+00, 2.71828183e+00, 7.38905610e+00, 2.00855369e+01,
           5.45981500e+01, 1.48413159e+02, 4.03428793e+02, 1.09663316e+03,
           2.98095799e+03, 8.10308393e+03])




```python
np.max(arr) #same as arr.max()
```




    9




```python
np.sin(arr)
```




    array([ 0.        ,  0.84147098,  0.90929743,  0.14112001, -0.7568025 ,
           -0.95892427, -0.2794155 ,  0.6569866 ,  0.98935825,  0.41211849])




```python
np.log(arr)
```

    /home/ggilmore/.local/lib/python3.6/site-packages/ipykernel_launcher.py:1: RuntimeWarning: divide by zero encountered in log
      """Entry point for launching an IPython kernel.





    array([      -inf, 0.        , 0.69314718, 1.09861229, 1.38629436,
           1.60943791, 1.79175947, 1.94591015, 2.07944154, 2.19722458])


