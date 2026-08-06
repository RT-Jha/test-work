# Linear Algebra: Matrix Operations and Matrix Inverses

## 1. Matrix Operations Fundamentals

Matrices are rectangular arrays of numbers that represent linear transformations, system of linear equations, and data structures.

### Basic Matrix Arithmetic
* **Addition and Subtraction**: For two matrices $A, B \in \mathbb{R}^{m \times n}$, addition is performed element-wise:
  $$(A + B)_{ij} = A_{ij} + B_{ij}$$
* **Scalar Multiplication**: Multiplying matrix $A$ by a scalar $c$:
  $$(cA)_{ij} = c \cdot A_{ij}$$
* **Transpose**: Swapping rows and columns of matrix $A \in \mathbb{R}^{m \times n}$ yields $A^T \in \mathbb{R}^{n \times m}$:
  $$(A^T)_{ij} = A_{ji}$$

---

## 2. Matrix Multiplication as Linear Transformation

Matrix multiplication $C = AB$ is **not** element-wise multiplication. For $A \in \mathbb{R}^{m \times k}$ and $B \in \mathbb{R}^{k \times n}$, the entry $C_{ij}$ is the dot product of row $i$ of $A$ and column $j$ of $B$:

$$C_{ij} = \sum_{l=1}^{k} A_{il} B_{lj}$$

Geometrically, multiplying a vector $\mathbf{x}$ by matrix $A$ transforms the vector (stretching, rotating, or shearing the coordinate grid).

![Linear Transformation](matrix_ops_figures/fig1_linear_transformation.png)

---

## 3. Matrix Inverses

An $n \times n$ square matrix $A$ is **invertible** (or non-singular) if there exists an $n \times n$ matrix $A^{-1}$ such that:

$$A A^{-1} = A^{-1} A = I_n$$

where $I_n$ is the $n \times n$ Identity matrix.

### Geometric Interpretation
If matrix $A$ applies a transformation to space, $A^{-1}$ **undoes** that transformation, bringing transformed vectors back to their original positions.

![Matrix Inverse](matrix_ops_figures/fig2_matrix_inverse.png)

---

## 4. Singular Matrices and Determinants

A square matrix $A$ is **non-invertible** (singular) if and only if its determinant is zero:

$$\det(A) = 0$$

Geometrically, a matrix with $\det(A) = 0$ collapses $n$-dimensional space into a lower dimension (e.g., collapsing a 2D plane into a 1D line). Information is lost, making it impossible to undo the operation.

![Singular Matrix Collapse](matrix_ops_figures/fig3_singular_matrix.png)

### Properties of Matrix Inverses
1. $(A^{-1})^{-1} = A$
2. $(AB)^{-1} = B^{-1} A^{-1}$ *(Reversal Rule)*
3. $(A^T)^{-1} = (A^{-1})^T$
4. $\det(A^{-1}) = \frac{1}{\det(A)}$

---

## 5. Python Implementation

The following Python code demonstrates basic matrix operations, solving linear systems, matrix inversion, and condition check using `numpy` and `scipy`.

```python
import numpy as np

# 1. Define Matrices
A = np.array([
    [2, 1],
    [1, 3]
], dtype=float)

B = np.array([
    [3, 2],
    [0, 1]
], dtype=float)

print("Matrix A:\n", A)
print("\nMatrix B:\n", B)

# 2. Matrix Arithmetic & Multiplication
A_plus_B = A + B
A_times_B = A @ B  # Matrix multiplication (or np.matmul)

print("\nA + B:\n", A_plus_B)
print("\nA @ B (Matrix Product):\n", A_times_B)

# 3. Transpose & Determinant
A_transpose = A.T
det_A = np.linalg.det(A)

print("\nTranspose of A:\n", A_transpose)
print(f"Determinant of A: {det_A:.4f}")

# 4. Matrix Inversion
if det_A != 0:
    A_inv = np.linalg.inv(A)
    print("\nInverse of A (A^-1):\n", A_inv)
    
    # Verification: A @ A_inv == I
    identity_check = np.allclose(A @ A_inv, np.eye(2))
    print(f"Verification (A @ A^-1 == Identity): {identity_check}")
else:
    print("\nMatrix A is singular and cannot be inverted!")

# 5. Solving Ax = b using Inverse vs Solve
b = np.array([5, 5], dtype=float)
x_inv = A_inv @ b                        # Method 1: x = A^-1 * b
x_solve = np.linalg.solve(A, b)          # Method 2: Numerical Solve (Preferred)

print(f"\nSolution x (via Inverse): {x_inv}")
print(f"Solution x (via np.linalg.solve): {x_solve}")