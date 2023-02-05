---
title: Matrices and Portfolio Variance
description: Portfolio Variance in matrix form and implementation in R, Julia, and Python
author: Mehmet Dogan
date: '2023-02-05'
slug: matrices-and-portfolio-variance

categories:
  - R
  - Julia
  - Python
tags:
  - Applied Finance
  - R
  - Julia
  - Python
  - Portfolio Variance
output: 
  html_document: 
---

<img src="/img/gadfly_plot.PNG" alt="TSLA and NFLX stock performance 2022, image by author" width="670"/>

Matrices are widely used in portfolio theory, financial economics, and econometrics because of the need to manipulate significant data inputs. 

In this article, you will learn core matrix operations and how [***portfolio variance***](https://www.investopedia.com/terms/p/portfolio-variance.asp), widely used in *portfolio allocation* decisions, can be represented in the *matrix form* and implementations in R, Julia, and Python languages. 

------------------------------------------------------------------------

1\. Matrix operations

2\. Portfolio variance in matrix form

3\. Implementation in R, Julia, and Python

------------------------------------------------------------------------

### 1. Matrix Operations

Matrices are valuable and essential ways of organizing data sets, which makes manipulating and transforming them much more straightforward.

**Terminology**

-   Scalar: a single number. E.g., 3, 5.5

-   Vector: one-dimensional array of numbers

-   Matrix: a 2D collection of arrays

A vector is a special matrix case with only one column or row.

-   If a matrix has only one row, it's known as a row vector with a dimension of 1 x C

-   If a matrix has only one column, it's known as a column vector with a dimension of R x 1

#### Matrix Definition

Let\'s start by defining two matrices and one vector we will use throughout this section.

<img src="https://cdn-images-1.medium.com/max/800/1*Cuh0hPFhMXhJVpVWiFFleQ.png" alt="Image by author" width="469"/>

``` python

### R
A = matrix(c(1, 2, 3, 4), nrow = 2, ncol = 2, byrow = TRUE)
B = matrix(c(5, 10, 15, 20), nrow = 2, ncol = 2, byrow = TRUE)
V = c(5, 10)

### Julia
A = [1 2;  3 4] # 2x2 matrix
B = [5 10; 15 20] # 2x2 matrix
V = [5, 10] # vector

### Python
import numpy as np
A = np.array([[1, 2], [3,4]]) # 2x2 matrix
B = np.array([[5, 10], [15,20]]) # 2x2 matrix
V = np.array([5, 10]) # vector
```

#### **Addition**

<img src="https://cdn-images-1.medium.com/max/800/1*N0ndCfZbSVcycx-tb7p9Gw.png" alt="$$$$" width="325"/>

``` r
# You can add matrices with the same size

### R, Julia, Python
A + B
```

#### Subtraction

<img src="https://cdn-images-1.medium.com/max/800/1*GGgNeHj5K4CXmhTf2kW1kA.png" width="357"/>

``` r
# You can subtract matrices with the same size

### R, Julia, Python
A - B
```

#### Multiplication

<img src="https://cdn-images-1.medium.com/max/800/1*e-4oPvRAjPEE-8TrZn9xxA.png" width="451"/>

``` r
### R
A %*% B # Not A * B

### Julia
A * B

### Python
np.dot(A, B)
```

#### Matrix-Scalar Multiplication

<img src="https://cdn-images-1.medium.com/max/800/1*PT6JuOVHBM_EJR4mRGPfEw.png" width="292"/>

``` r
### R, Julia, Python
3 * A
# + 3A in Julia
```

#### Matrix-Vector (Transposed) Multiplication

<img src="https://cdn-images-1.medium.com/max/800/1*_rOXMOJfqKRAXYqHxmJZsg.png" width="416"/>

``` r
### R
t(V) %*% A

### Julia
V' * A

### Python
np.dot(V.T, A) 
```

#### Matrix-Vector Multiplication

<img src="https://cdn-images-1.medium.com/max/800/1*0hrfFX5xN4PgAC3RtyhouA.png" width="286"/>

``` r
### R
A %*% V

### Julia
A * V

### Python
np.dot(A, V)
```

### 2. Portfolio Variance in Matrix Form

[Modern portfolio theory](https://www.investopedia.com/terms/m/modernportfoliotheory.asp) (MPT) states that portfolio variance can be reduced by selecting securities with low or negative correlations in which to invest, such as stocks and bonds. ([Investopedia](https://www.investopedia.com/ask/answers/071515/how-can-i-measure-portfolio-variance.asp#:~:text=Portfolio%20variance%20is%20a%20measure,between%20securities%20in%20the%20portfolio.))

Modern Portfolio Theory is not the main subject of this article, therefore skipping its details here. In another post, I will explain modern portfolio theory in detail with R, Julia, and Python implementation.

#### Matrix form of two-asset portfolio variance

<img src="https://cdn-images-1.medium.com/max/800/1*A73h5pYUjfH0ZrMlJNf--w.png" alt="image by author" width="480"/>

The illustration in the image above is for the two-asset portfolio, but using the same matrix form, you can extend it to any number of assets.

In more plain language, what we need to calculate is:

***Portfolio variance = Weights transposed \* Covariance matrix \*Weights***

### 3. Implementation in R, Julia, and Python

#### *R* Implementation

``` r
weights = c(0.6, 0.4)

covMatrix = matrix(
  c(0.000738889, 0.000538889, 0.000538889, 0.00549889),
  nrow = 2,
  ncol = 2,
  byrow = TRUE
)

portVar = t(weights) %*% covMatrix %*% weights
portStd = sqrt(portVar)

print(paste("Portfolio Variance is: ", portVar))
print(paste("Portfolio Risk (Std) is: ", portStd))
```

#### *Julia* Implementation

``` julia
weights = [0.6, 0.4]

covMatrix = [0.000738889 0.000538889; 0.000538889 0.00549889]
portVar = weights' * covMatrix * weights
portStd = sqrt(portVar)

print("Portfolio Variance is $portVar")
print("Portfolio Risk (Std) is $portStd")
```

#### *Python* Implementation

``` python

import numpy as np
weights = np.array([0.6, 0.4])
covMatrix = [[0.000738889, 0.000538889],
             [0.000538889, 0.00549889]]

portVar = np.dot(np.dot(weights, covMatrix), weights.T)
portStd = np.sqrt(portVar)
print("Portfolio Variance: ", portVar)
print("Portfolio Risk (Std): ", portStd)
```
