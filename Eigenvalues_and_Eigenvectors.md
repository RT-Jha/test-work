# 🏛️ Mathematics for IT Course - M.Tech. 1st Semester, IIIT Allahabad

## Unit 1: Linear Algebra and Matrix Theory

### Current Topic: Eigenvalues and Eigenvectors — intuition, geometric interpretation, solved examples, applications, and Python implementation

---

## 👥 Instructor Information

- **Edited by Instructor:** [Dr. Mohammed Javed](https://sites.google.com/site/mohammedjaved2016/)
- **Email:** javed@iiita.ac.in
- **Teaching Assistant:** Mr. Apurba Chakraborty (rsi2024005@iiita.ac.in)

---

## Learning Objectives

By the end of this material, you should be able to:

- Understand the meaning of eigenvalues and eigenvectors.
- Explain their geometric interpretation.
- Form and solve the characteristic equation.
- Calculate eigenvalues and eigenvectors by hand.
- Understand eigenspaces, multiplicity, and diagonalization.
- Verify eigenpairs using Python/NumPy.
- Visualize eigenvectors and matrix transformations.
- Connect eigenvalues/eigenvectors with PCA and practical computing.

---

# 1. Motivation: Why Do We Need Eigenvalues and Eigenvectors?

A matrix can represent a **linear transformation**. Depending on the matrix, this transformation can stretch, compress, rotate, reflect, or shear vectors.

For an ordinary vector, both its **magnitude and direction** may change after matrix multiplication.

However, some special non-zero vectors do not change their direction. They may only become longer, shorter, or point in the opposite direction.

These special vectors are called **eigenvectors**.

The amount by which they are scaled is described by their **eigenvalues**.

![Matrix transformation](figures/01_linear_transformation.png)

**Figure 1:** A matrix transforms a unit circle into an ellipse. Special directions of this transformation are related to eigenvectors.

---

# 2. Definition of Eigenvalues and Eigenvectors

Let \(A\) be an \(n\times n\) square matrix.

A non-zero vector \(\mathbf{v}\) is an **eigenvector** of \(A\) if

\[
A\mathbf{v}=\lambda\mathbf{v}
\]

for some scalar \(\lambda\).

The scalar \(\lambda\) is called the **eigenvalue corresponding to \(\mathbf{v}\)**.

### Meaning of the equation

The equation

\[
A\mathbf{v}=\lambda\mathbf{v}
\]

says that applying transformation \(A\) to \(\mathbf{v}\) produces the same result as simply multiplying \(\mathbf{v}\) by the number \(\lambda\).

Therefore, the direction represented by the eigenvector is preserved.

![Eigenvector intuition](figures/02_eigenvector_intuition.png)

**Figure 2:** An eigenvector remains on its original line after transformation, whereas a general vector need not.

---

# 3. Understanding the Eigenvalue \(\lambda\)

The eigenvalue tells us what happens to an eigenvector's magnitude and orientation.

| Eigenvalue | Effect |
|---|---|
| \(\lambda>1\) | Vector is stretched |
| \(0<\lambda<1\) | Vector is compressed |
| \(\lambda=1\) | Vector remains unchanged |
| \(\lambda=0\) | Vector collapses to the zero vector |
| \(\lambda<0\) | Direction reverses, together with scaling |
| Complex \(\lambda\) | Can encode rotation/scaling behavior in an extended complex vector space |

![Eigenvalue scaling](figures/04_eigenvalue_scaling.png)

**Figure 3:** Positive, fractional, and negative eigenvalues produce different scaling behavior.

---

# 4. Deriving the Characteristic Equation

Starting from

\[
A\mathbf{v}=\lambda\mathbf{v},
\]

move everything to one side:

\[
A\mathbf{v}-\lambda\mathbf{v}=0.
\]

Since

\[
\mathbf{v}=I\mathbf{v},
\]

we obtain

\[
A\mathbf{v}-\lambda I\mathbf{v}=0,
\]

and hence

\[
(A-\lambda I)\mathbf{v}=0.
\]

Because an eigenvector must satisfy

\[
\mathbf{v}\neq0,
\]

this homogeneous system must possess a non-trivial solution.

Therefore \(A-\lambda I\) must be singular:

\[
\boxed{\det(A-\lambda I)=0}
\]

This equation is called the **characteristic equation**.

The polynomial

\[
p(\lambda)=\det(A-\lambda I)
\]

is the **characteristic polynomial**.

---

# 5. Solved Example 1 — Finding Eigenvalues

Consider

\[
A=
\begin{bmatrix}
2&1\\
1&2
\end{bmatrix}.
\]

### Step 1: Construct \(A-\lambda I\)

\[
A-\lambda I=
\begin{bmatrix}
2-\lambda&1\\
1&2-\lambda
\end{bmatrix}.
\]

### Step 2: Set its determinant equal to zero

\[
\begin{vmatrix}
2-\lambda&1\\
1&2-\lambda
\end{vmatrix}=0.
\]

Therefore,

\[
(2-\lambda)^2-1=0.
\]

Expanding,

\[
\lambda^2-4\lambda+3=0.
\]

Factorizing,

\[
(\lambda-1)(\lambda-3)=0.
\]

Hence,

\[
\boxed{\lambda_1=1,\qquad\lambda_2=3}.
\]

---

# 6. Solved Example 2 — Finding Eigenvectors

We now find an eigenvector for each eigenvalue.

## 6.1 Eigenvector corresponding to \(\lambda=3\)

Solve

\[
(A-3I)\mathbf{v}=0.
\]

Then

\[
A-3I=
\begin{bmatrix}
-1&1\\
1&-1
\end{bmatrix}.
\]

Let

\[
\mathbf{v}=
\begin{bmatrix}
x\\y
\end{bmatrix}.
\]

Then

\[
-x+y=0,
\]

so

\[
y=x.
\]

Choose \(x=1\):

\[
\boxed{
\mathbf{v}_1=
\begin{bmatrix}
1\\1
\end{bmatrix}
}.
\]

Any non-zero scalar multiple of this vector is also an eigenvector.

## 6.2 Eigenvector corresponding to \(\lambda=1\)

Solve

\[
(A-I)\mathbf{v}=0.
\]

We obtain

\[
A-I=
\begin{bmatrix}
1&1\\
1&1
\end{bmatrix}.
\]

Thus

\[
x+y=0,
\]

or

\[
y=-x.
\]

Taking \(x=1\),

\[
\boxed{
\mathbf{v}_2=
\begin{bmatrix}
1\\-1
\end{bmatrix}
}.
\]

---

# 7. Geometrical Interpretation

For

\[
A=
\begin{bmatrix}
2&1\\
1&2
\end{bmatrix},
\]

the two eigen-directions are

\[
\begin{bmatrix}1\\1\end{bmatrix}
\quad\text{and}\quad
\begin{bmatrix}1\\-1\end{bmatrix}.
\]

Along the first direction the transformation scales vectors by \(3\).

Along the second direction it scales vectors by \(1\).

![Eigen directions](figures/03_eigen_directions.png)

**Figure 4:** The two eigen-directions of the example matrix.

---

# 8. Important Properties

For an \(n\times n\) matrix \(A\):

1. Eigenvalues are roots of the characteristic polynomial.
2. A matrix may have real or complex eigenvalues.
3. Eigenvectors are never the zero vector.
4. Scalar multiples of an eigenvector remain eigenvectors for the same eigenvalue.
5. Eigenvectors corresponding to distinct eigenvalues are linearly independent.
6. For a triangular matrix, its eigenvalues are its diagonal entries.
7. The sum of eigenvalues, counting algebraic multiplicity, equals the trace:

\[
\operatorname{tr}(A)=\sum_i\lambda_i.
\]

8. The product of eigenvalues, counting multiplicity, equals the determinant:

\[
\det(A)=\prod_i\lambda_i.
\]

9. A matrix is singular exactly when \(0\) is one of its eigenvalues.

---

# 9. Eigenspace

For an eigenvalue \(\lambda\), all corresponding eigenvectors together with the zero vector form an **eigenspace**:

\[
E_\lambda=\ker(A-\lambda I).
\]

For the previous example,

\[
E_3=
\operatorname{span}
\left\{
\begin{bmatrix}
1\\1
\end{bmatrix}
\right\}.
\]

---

# 10. Algebraic and Geometric Multiplicity

## Algebraic Multiplicity

The number of times an eigenvalue occurs as a root of the characteristic polynomial.

For example,

\[
(\lambda-2)^2(\lambda-5)=0
\]

gives eigenvalue \(2\) algebraic multiplicity \(2\).

## Geometric Multiplicity

The dimension of the eigenspace:

\[
\dim\ker(A-\lambda I).
\]

For every eigenvalue,

\[
1\leq\text{geometric multiplicity}\leq\text{algebraic multiplicity}.
\]

---

# 11. Diagonalization

A square matrix is diagonalizable when it possesses enough linearly independent eigenvectors to form a basis.

Then

\[
\boxed{A=PDP^{-1}}
\]

where:

- \(P\) contains eigenvectors as columns.
- \(D\) contains corresponding eigenvalues on its diagonal.

For the example,

\[
P=
\begin{bmatrix}
1&1\\
1&-1
\end{bmatrix},
\qquad
D=
\begin{bmatrix}
3&0\\
0&1
\end{bmatrix}.
\]

Diagonalization is useful because powers become easy:

\[
A^k=PD^kP^{-1}.
\]

---

# 12. Python — Computing Eigenvalues and Eigenvectors

```python
import numpy as np

A = np.array([
    [2, 1],
    [1, 2]
])

eigenvalues, eigenvectors = np.linalg.eig(A)

print("Matrix A:")
print(A)

print("\nEigenvalues:")
print(eigenvalues)

print("\nEigenvectors:")
print(eigenvectors)
```

> NumPy stores the corresponding eigenvectors as **columns** of the returned eigenvector matrix.

---

# 13. Python — Verifying \(Av=\lambda v\)

```python
import numpy as np

A = np.array([
    [2, 1],
    [1, 2]
])

eigenvalues, eigenvectors = np.linalg.eig(A)

for i in range(len(eigenvalues)):
    eigenvalue = eigenvalues[i]
    eigenvector = eigenvectors[:, i]

    left_side = A @ eigenvector
    right_side = eigenvalue * eigenvector

    print("\nEigenvalue:", eigenvalue)
    print("Eigenvector:", eigenvector)
    print("A @ v:", left_side)
    print("lambda * v:", right_side)
    print("Verified:", np.allclose(left_side, right_side))
```

---

# 14. Python — Visualizing Eigenvectors

```python
import numpy as np
import matplotlib.pyplot as plt

A = np.array([
    [2, 1],
    [1, 2]
])

values, vectors = np.linalg.eig(A)

theta = np.linspace(0, 2*np.pi, 300)

circle = np.vstack([
    np.cos(theta),
    np.sin(theta)
])

transformed = A @ circle

plt.figure(figsize=(7, 6))

plt.plot(
    transformed[0],
    transformed[1],
    label="Transformed unit circle"
)

for i in range(len(values)):
    v = vectors[:, i]

    plt.quiver(
        0, 0,
        3*v[0], 3*v[1],
        angles="xy",
        scale_units="xy",
        scale=1,
        label=f"Eigenvector {i+1}"
    )

plt.axhline(0)
plt.axvline(0)
plt.axis("equal")
plt.grid(True)
plt.legend()
plt.title("Eigenvectors of a Linear Transformation")
plt.show()
```

---

# 15. Python — Diagonalization

```python
import numpy as np

A = np.array([
    [2, 1],
    [1, 2]
])

eigenvalues, P = np.linalg.eig(A)

D = np.diag(eigenvalues)

A_reconstructed = P @ D @ np.linalg.inv(P)

print("P:")
print(P)

print("\nD:")
print(D)

print("\nP D P^-1:")
print(A_reconstructed)

print(
    "\nCorrect reconstruction:",
    np.allclose(A, A_reconstructed)
)
```

---

# 16. Symmetric Matrices and the Spectral Theorem

A real symmetric matrix satisfies

\[
A=A^T.
\]

Such matrices have especially useful properties:

- All eigenvalues are real.
- Eigenvectors belonging to distinct eigenvalues are orthogonal.
- An orthonormal eigenvector basis can always be chosen.

Consequently,

\[
A=QDQ^T,
\]

where \(Q\) is orthogonal:

\[
Q^TQ=I.
\]

This result is the **spectral theorem** for real symmetric matrices.

---

# 17. Application — Principal Component Analysis

One of the best-known applications of eigenvectors is **Principal Component Analysis (PCA)**.

Given centered observations, PCA examines their covariance matrix.

The eigenvectors of the covariance matrix provide the principal directions, while the eigenvalues measure variance along those directions.

![PCA eigenvectors](figures/05_pca_eigenvectors.png)

**Figure 5:** PCA identifies directions of high and low variance using eigenvectors.

---

# 18. Python — PCA from Eigen-Decomposition

```python
import numpy as np

X = np.array([
    [2, 3],
    [3, 5],
    [4, 5],
    [5, 7],
    [6, 8]
], dtype=float)

# Center the dataset.
X_centered = X - X.mean(axis=0)

# Covariance matrix.
covariance = np.cov(
    X_centered,
    rowvar=False
)

# Covariance is symmetric, so eigh is convenient.
eigenvalues, eigenvectors = np.linalg.eigh(covariance)

# Sort from largest eigenvalue to smallest.
indices = np.argsort(eigenvalues)[::-1]

eigenvalues = eigenvalues[indices]
eigenvectors = eigenvectors[:, indices]

print("Covariance Matrix:")
print(covariance)

print("\nEigenvalues:")
print(eigenvalues)

print("\nPrincipal Directions:")
print(eigenvectors)
```

The eigenvector corresponding to the largest eigenvalue gives the direction containing the greatest variance.

---

# 19. Additional Applications

### Machine Learning

- PCA and dimensionality reduction
- Feature extraction
- Spectral clustering

### Computer Vision

- Eigenfaces
- Image compression
- Shape and covariance analysis

### Graphs and Networks

- Spectral graph theory
- Centrality measures
- PageRank-style stationary behavior

### Differential Equations

For

\[
\frac{d\mathbf{x}}{dt}=A\mathbf{x},
\]

eigenvalues help determine growth, decay, oscillation, and stability.

### Markov Chains

The stationary distribution is associated with an eigenvector corresponding to eigenvalue \(1\), under the appropriate stochastic-matrix convention.

---

# 20. Common Mistakes

### Mistake 1: Allowing the zero vector as an eigenvector

Incorrect:

\[
\mathbf{v}=0.
\]

An eigenvector must always be **non-zero**.

### Mistake 2: Solving only for eigenvalues

An eigenvalue and its corresponding eigenvector should be distinguished.

### Mistake 3: Using

\[
\det(A-\lambda I)\neq0.
\]

For eigenvalues the required condition is

\[
\boxed{\det(A-\lambda I)=0}.
\]

### Mistake 4: Assuming every matrix is diagonalizable

Some matrices do not possess enough linearly independent eigenvectors.

---

# 21. Practice Questions

### Question 1

Find the eigenvalues of

\[
A=
\begin{bmatrix}
4&0\\
0&2
\end{bmatrix}.
\]

### Question 2

Find the eigenvalues and eigenvectors of

\[
A=
\begin{bmatrix}
3&1\\
0&2
\end{bmatrix}.
\]

### Question 3

Determine whether

\[
\begin{bmatrix}
1\\1
\end{bmatrix}
\]

is an eigenvector of

\[
A=
\begin{bmatrix}
2&1\\
1&2
\end{bmatrix}.
\]

If yes, determine its eigenvalue.

### Question 4

Explain why eigenvectors corresponding to distinct eigenvalues are linearly independent.

### Question 5

Write Python code to verify every eigenpair produced by `numpy.linalg.eig()`.

---

# 22. Quick Revision Table

| Concept | Key Idea |
|---|---|
| Eigenvector | Special non-zero vector whose direction is preserved |
| Eigenvalue | Scaling factor associated with an eigenvector |
| Fundamental equation | \(A\mathbf{v}=\lambda\mathbf{v}\) |
| Characteristic equation | \(\det(A-\lambda I)=0\) |
| Eigenspace | \(\ker(A-\lambda I)\) |
| Trace | Sum of eigenvalues, counting multiplicity |
| Determinant | Product of eigenvalues, counting multiplicity |
| Diagonalization | \(A=PDP^{-1}\) |
| Symmetric matrix | Has real eigenvalues and an orthonormal eigenbasis |
| PCA | Uses eigenvectors/eigenvalues of a covariance matrix |

---

# 23. Final Summary

Eigenvalues and eigenvectors reveal the fundamental directions hidden inside a linear transformation.

The central equation is

\[
\boxed{A\mathbf{v}=\lambda\mathbf{v}}.
\]

To calculate eigenvalues, solve

\[
\boxed{\det(A-\lambda I)=0}.
\]

Then, for every eigenvalue, solve

\[
\boxed{(A-\lambda I)\mathbf{v}=0}
\]

to obtain its eigenspace and eigenvectors.

These concepts provide the foundation for diagonalization, spectral analysis, PCA, dynamical systems, graph algorithms, and many other areas of mathematics and computing.
