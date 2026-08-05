# 🏛️ Mathematics for IT Course - M.Tech. 1st Semester, IIIT Allahabad

## Unit 2: 🎯 Eigen Analysis and Matrix Decomposition 🎯

### Current Topics

- 🔵 Eigenvalues and Eigenvectors
- 🔵 Characteristic Equations
- 🔵 Diagonalization of Matrices

---

## 👥 Instructor Information

- **Edited by Instructor:** Dr. Mohammed Javed
- **Email:** javed@iiita.ac.in
- **Teaching Assistant:** Mr. Apurba Chakraborty

---

## 🎯 Learning Objectives

By the end of this material, you should be able to:

- Understand the concept of eigenvalues and eigenvectors.
- Derive and solve the characteristic equation.
- Compute eigenvalues and eigenvectors manually and using Python.
- Verify eigenpairs.
- Understand matrix diagonalization.
- Determine whether a matrix is diagonalizable.
- Apply diagonalization to solve practical problems.
- Implement all concepts using NumPy.


# 1. Eigenvalues and Eigenvectors

...(your existing content)...

---

# 2. Characteristic Equation

## 2.1 Introduction

The characteristic equation is used to determine the eigenvalues of a square matrix.

Suppose

A v = λv

Then,

(A − λI)v = 0

For a non-zero solution to exist,

det(A − λI) = 0

This equation is called the **Characteristic Equation**.

---

## 2.2 Characteristic Polynomial

For a matrix

A = |a  b|
    |c  d|

the characteristic polynomial is

λ² − (a+d)λ + (ad−bc) = 0

where

- Trace(A) = a + d
- Determinant(A) = ad − bc

---

## 2.3 Steps to Find Characteristic Equation

1. Write matrix A.
2. Compute A − λI.
3. Find det(A − λI).
4. Equate determinant to zero.
5. Solve the polynomial.

---

## Example

For

A =
|2 1|
|1 2|

A − λI

=
|2−λ 1|
|1 2−λ|

Characteristic equation

(2−λ)²−1 = 0

λ²−4λ+3=0

Eigenvalues

λ₁ = 3

λ₂ = 1

---

## Python Code

```python
import numpy as np

A = np.array([[2,1],
              [1,2]])

characteristic = np.poly(A)

print(characteristic)
```

---

# 3. Diagonalization of Matrices

## 3.1 Introduction

A matrix is diagonalizable if it has enough linearly independent eigenvectors.

If

A = PDP⁻¹

where

- P contains eigenvectors
- D is the diagonal matrix of eigenvalues

then A is diagonalizable.

---

## 3.2 Steps

1. Find eigenvalues.
2. Find eigenvectors.
3. Form matrix P.
4. Construct diagonal matrix D.
5. Compute P⁻¹.
6. Verify

A = PDP⁻¹

---

## Example

Suppose

A =
|2 1|
|1 2|

Eigenvalues

3 and 1

Eigenvectors

[1 1]

[1 -1]

Therefore

P =
|1 1|
|1 -1|

D =
|3 0|
|0 1|

Verify

A = PDP⁻¹

---

## Python Implementation

```python
import numpy as np

A = np.array([[2,1],
              [1,2]])

eigenvalues, P = np.linalg.eig(A)

D = np.diag(eigenvalues)

P_inv = np.linalg.inv(P)

A_new = P @ D @ P_inv

print(A_new)

print(np.allclose(A, A_new))
```

---

## Advantages of Diagonalization

- Fast computation of Aⁿ
- Matrix exponential
- Solving differential equations
- Principal Component Analysis
- Quantum Mechanics
- Control Systems

---

## Practice Questions

1. Find the characteristic equation of

|3 2|
|1 4|

2. Find eigenvalues.

3. Find eigenvectors.

4. Determine whether the matrix is diagonalizable.

5. Verify A = PDP⁻¹ using Python.

---

## Summary

- Eigenvalues measure scaling.
- Eigenvectors preserve direction.
- Characteristic equation determines eigenvalues.
- Eigenvectors are obtained from (A−λI)v=0.
- Diagonalization converts a matrix into a simpler diagonal form.
- NumPy provides efficient implementations using `np.linalg.eig()`.