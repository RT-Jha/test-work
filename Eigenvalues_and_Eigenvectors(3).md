# 🏛️ Mathematics for IT Course - M.Tech. 1st Semester, IIIT Allahabad

## Unit 2: Eigen Analysis and Matrix Decomposition

### Current Topic: Eigenvalues and Eigenvectors — Concepts, Geometric Interpretation, Solved Examples, Applications, and Python Implementation

---

## 👥 Instructor Information

- **Edited by Instructor:** [Dr. Mohammed Javed](https://sites.google.com/site/mohammedjaved2016/)
- **Email:** [javed@iiita.ac.in](mailto:javed@iiita.ac.in)
- **Teaching Assistants:** Aarti Jha ([rsi2025509@iiita.ac.in](mailto:rsi2025509@iiita.ac.in))

---

## Learning Objectives

By the end of this material, you should be able to:

- Understand the meaning of **eigenvalues** and **eigenvectors**.
- Interpret eigenvectors geometrically as special directions of a linear transformation.
- Derive the **characteristic equation** of a matrix.
- Calculate eigenvalues and corresponding eigenvectors by hand.
- Understand algebraic and geometric multiplicity.
- Verify eigenpairs using the equation \(A\mathbf{v}=\lambda\mathbf{v}\).
- Understand diagonalization and its relationship with eigenvectors.
- Recognize important properties of eigenvalues.
- Use NumPy to calculate eigenvalues and eigenvectors.
- Visualize eigenvectors and matrix transformations using Python.
- Understand applications such as PCA, dynamical systems, graph analysis, and differential equations.

---

# 1. Why Do We Need Eigenvalues and Eigenvectors?

A matrix can be viewed as a **linear transformation**. When a vector is multiplied by a matrix, the vector may:

- rotate,
- stretch,
- shrink,
- reflect,
- or undergo a combination of these effects.

Most vectors change both their **magnitude** and **direction**.

However, certain special vectors do **not change their direction** after the transformation. They may only be stretched, shrunk, reversed, or collapsed.

These special vectors are called **eigenvectors**.

The amount by which an eigenvector is scaled is called its **eigenvalue**.

![Eigenvector intuition](figures/01_eigenvector_intuition.png)

**Figure 1.** Eigenvectors remain on the same line after transformation, while an ordinary vector generally changes direction.

---

# 2. Definition of Eigenvalue and Eigenvector

Let \(A\) be an \(n\times n\) square matrix.

A non-zero vector \(\mathbf{v}\) is called an **eigenvector** of \(A\) if

\[
A\mathbf{v}=\lambda\mathbf{v}
\]

for some scalar \(\lambda\).

The scalar \(\lambda\) is called the **eigenvalue corresponding to \(\mathbf{v}\)**.

### Important points

1. \(A\) must be square when discussing its ordinary eigenvalues.
2. An eigenvector can **never be the zero vector**.
3. An eigenvalue **can be zero**.
4. Multiples of an eigenvector are also eigenvectors associated with the same eigenvalue.

For example, if

\[
A\mathbf{v}=3\mathbf{v},
\]

then \(\mathbf{v}\) is an eigenvector and \(3\) is its eigenvalue.

---

# 3. Geometric Interpretation

Consider

\[
A=
\begin{bmatrix}
2&1\\
1&2
\end{bmatrix}.
\]

When this matrix acts on the plane, a unit circle is transformed into an ellipse.

![Circle to ellipse](figures/02_circle_to_ellipse.png)

**Figure 2.** The dashed directions are eigenvector directions. Points lying along these directions remain on the same line after transformation.

For this matrix:

\[
\lambda_1=3,\qquad \lambda_2=1.
\]

The corresponding eigenvector directions are

\[
\mathbf{v}_1=
\begin{bmatrix}
1\\1
\end{bmatrix},
\qquad
\mathbf{v}_2=
\begin{bmatrix}
1\\-1
\end{bmatrix}.
\]

Along \(\mathbf{v}_1\), the transformation stretches vectors by a factor of \(3\).

Along \(\mathbf{v}_2\), the scale factor is \(1\), so vectors on this direction retain their length.

---

# 4. Meaning of the Eigenvalue

From

\[
A\mathbf{v}=\lambda\mathbf{v},
\]

the eigenvalue tells us what happens to the eigenvector.

| Eigenvalue | Effect |
|---|---|
| \(\lambda>1\) | Vector is stretched |
| \(0<\lambda<1\) | Vector is shrunk |
| \(\lambda=1\) | Vector remains unchanged |
| \(\lambda=0\) | Vector collapses to zero |
| \(\lambda<0\) | Direction reverses and magnitude is scaled |
| \(|\lambda|=1\) | Magnitude is preserved |

![Eigenvalue effects](figures/03_eigenvalue_effects.png)

**Figure 3.** Geometric effects produced by different eigenvalue types.

---

# 5. How to Find Eigenvalues

Start with

\[
A\mathbf{v}=\lambda\mathbf{v}.
\]

Move everything to one side:

\[
A\mathbf{v}-\lambda\mathbf{v}=0.
\]

Since \(I\mathbf{v}=\mathbf{v}\),

\[
(A-\lambda I)\mathbf{v}=0.
\]

For a non-zero solution \(\mathbf{v}\) to exist, \(A-\lambda I\) must be singular. Therefore,

\[
\boxed{\det(A-\lambda I)=0}.
\]

This is called the **characteristic equation**.

The polynomial

\[
p(\lambda)=\det(A-\lambda I)
\]

is called the **characteristic polynomial**.

---

# 6. Solved Example 1 — Finding Eigenvalues

Consider

\[
A=
\begin{bmatrix}
2&1\\
1&2
\end{bmatrix}.
\]

### Step 1 — Form \(A-\lambda I\)

\[
A-\lambda I=
\begin{bmatrix}
2-\lambda&1\\
1&2-\lambda
\end{bmatrix}.
\]

### Step 2 — Set its determinant equal to zero

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
4-4\lambda+\lambda^2-1=0
\]

\[
\lambda^2-4\lambda+3=0.
\]

Factorizing,

\[
(\lambda-1)(\lambda-3)=0.
\]

Hence,

\[
\boxed{\lambda_1=3,\qquad\lambda_2=1}.
\]

---

# 7. How to Find Eigenvectors

After finding an eigenvalue \(\lambda\), substitute it into

\[
(A-\lambda I)\mathbf{v}=0.
\]

Then solve the resulting homogeneous system.

---

## 7.1 Eigenvector for \(\lambda=3\)

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
\begin{bmatrix}
-1&1\\
1&-1
\end{bmatrix}
\begin{bmatrix}
x\\y
\end{bmatrix}
=
\begin{bmatrix}
0\\0
\end{bmatrix}.
\]

This gives

\[
-x+y=0
\]

and therefore

\[
y=x.
\]

Taking \(x=1\),

\[
\boxed{
\mathbf{v}_1=
\begin{bmatrix}
1\\1
\end{bmatrix}
}.
\]

---

## 7.2 Eigenvector for \(\lambda=1\)

\[
A-I=
\begin{bmatrix}
1&1\\
1&1
\end{bmatrix}.
\]

Hence

\[
x+y=0,
\]

so

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

# 8. Verification of an Eigenpair

For

\[
\mathbf{v}_1=
\begin{bmatrix}
1\\1
\end{bmatrix},
\qquad \lambda_1=3,
\]

calculate

\[
A\mathbf{v}_1=
\begin{bmatrix}
2&1\\
1&2
\end{bmatrix}
\begin{bmatrix}
1\\1
\end{bmatrix}
=
\begin{bmatrix}
3\\3
\end{bmatrix}.
\]

Also,

\[
3\mathbf{v}_1=
3
\begin{bmatrix}
1\\1
\end{bmatrix}
=
\begin{bmatrix}
3\\3
\end{bmatrix}.
\]

Thus

\[
A\mathbf{v}_1=3\mathbf{v}_1.
\]

Therefore, the eigenpair is verified.

---

# 9. Python Implementation Using NumPy

NumPy provides `numpy.linalg.eig()`.

```python
import numpy as np

A = np.array([
    [2, 1],
    [1, 2]
], dtype=float)

eigenvalues, eigenvectors = np.linalg.eig(A)

print("Matrix A:")
print(A)

print("\nEigenvalues:")
print(eigenvalues)

print("\nEigenvectors:")
print(eigenvectors)
```

### Important

NumPy stores the eigenvectors as **columns**.

Therefore,

```python
eigenvectors[:, 0]
```

is the eigenvector corresponding to

```python
eigenvalues[0]
```

---

# 10. Verifying Eigenpairs in Python

```python
import numpy as np

A = np.array([
    [2, 1],
    [1, 2]
], dtype=float)

eigenvalues, eigenvectors = np.linalg.eig(A)

for i in range(len(eigenvalues)):
    lam = eigenvalues[i]
    v = eigenvectors[:, i]

    lhs = A @ v
    rhs = lam * v

    print(f"\nEigenvalue {i + 1}: {lam}")
    print("Eigenvector:", v)
    print("A @ v:", lhs)
    print("lambda * v:", rhs)
    print("Verified:", np.allclose(lhs, rhs))
```

`np.allclose()` is preferable to exact equality because floating-point calculations may contain tiny numerical errors.

---

# 11. Visualizing Eigenvectors with Python

```python
import numpy as np
import matplotlib.pyplot as plt

A = np.array([
    [2, 1],
    [1, 2]
])

eigenvalues, eigenvectors = np.linalg.eig(A)

plt.figure(figsize=(7, 7))

for i in range(2):
    v = eigenvectors[:, i]

    plt.quiver(
        0, 0,
        v[0], v[1],
        angles="xy",
        scale_units="xy",
        scale=1,
        label=f"Eigenvector {i+1}, λ={eigenvalues[i]:.2f}"
    )

plt.axhline(0)
plt.axvline(0)
plt.xlim(-1.5, 1.5)
plt.ylim(-1.5, 1.5)
plt.grid()
plt.legend()
plt.title("Eigenvectors of Matrix A")
plt.xlabel("x")
plt.ylabel("y")
plt.show()
```

---

# 12. Solved Example 2 — Triangular Matrix

Consider

\[
A=
\begin{bmatrix}
4&2\\
0&3
\end{bmatrix}.
\]

The characteristic equation is

\[
\det(A-\lambda I)=
\begin{vmatrix}
4-\lambda&2\\
0&3-\lambda
\end{vmatrix}=0.
\]

Therefore,

\[
(4-\lambda)(3-\lambda)=0.
\]

Hence,

\[
\boxed{\lambda_1=4,\qquad\lambda_2=3}.
\]

### Observation

For any triangular matrix, the eigenvalues are its **diagonal entries**.

---

# 13. Characteristic Polynomial for a \(2\times2\) Matrix

For

\[
A=
\begin{bmatrix}
a&b\\
c&d
\end{bmatrix},
\]

\[
\det(A-\lambda I)
=
(a-\lambda)(d-\lambda)-bc.
\]

Therefore,

\[
\lambda^2-(a+d)\lambda+(ad-bc)=0.
\]

Since

\[
\operatorname{tr}(A)=a+d
\]

and

\[
\det(A)=ad-bc,
\]

we obtain

\[
\boxed{
\lambda^2-\operatorname{tr}(A)\lambda+\det(A)=0
}.
\]

---

# 14. Trace and Determinant Relationship

If the eigenvalues of an \(n\times n\) matrix are

\[
\lambda_1,\lambda_2,\ldots,\lambda_n
\]

counting algebraic multiplicity, then

\[
\boxed{\operatorname{tr}(A)=\sum_{i=1}^{n}\lambda_i}
\]

and

\[
\boxed{\det(A)=\prod_{i=1}^{n}\lambda_i}.
\]

For the earlier matrix,

\[
A=
\begin{bmatrix}
2&1\\
1&2
\end{bmatrix},
\]

we have

\[
\operatorname{tr}(A)=4=3+1
\]

and

\[
\det(A)=3=3\times1.
\]

---

# 15. Eigenspace

For a particular eigenvalue \(\lambda\), all corresponding eigenvectors together with the zero vector form the **eigenspace**:

\[
E_\lambda=\ker(A-\lambda I).
\]

Thus, finding eigenvectors is equivalent to finding the null space of \(A-\lambda I\).

---

# 16. Algebraic and Geometric Multiplicity

## Algebraic Multiplicity

The number of times an eigenvalue occurs as a root of the characteristic polynomial.

Example:

\[
(\lambda-2)^2(\lambda-5)=0.
\]

The eigenvalue \(2\) has algebraic multiplicity \(2\).

## Geometric Multiplicity

The dimension of the eigenspace:

\[
\dim\ker(A-\lambda I).
\]

For every eigenvalue,

\[
1\leq \text{geometric multiplicity}
\leq \text{algebraic multiplicity}.
\]

This distinction is important when determining whether a matrix is diagonalizable.

---

# 17. Diagonalization

A matrix \(A\) is diagonalizable if it possesses enough linearly independent eigenvectors.

If

\[
P=
\begin{bmatrix}
|&|&&|\\
v_1&v_2&\cdots&v_n\\
|&|&&|
\end{bmatrix}
\]

contains independent eigenvectors, and

\[
D=
\begin{bmatrix}
\lambda_1&0&\cdots&0\\
0&\lambda_2&\cdots&0\\
\vdots&\vdots&\ddots&\vdots\\
0&0&\cdots&\lambda_n
\end{bmatrix},
\]

then

\[
\boxed{A=PDP^{-1}}.
\]

![Diagonalization](figures/04_diagonalization_flow.png)

**Figure 4.** Diagonalization expresses a transformation in its natural eigenvector coordinate system.

---

# 18. Diagonalization in Python

```python
import numpy as np

A = np.array([
    [2, 1],
    [1, 2]
], dtype=float)

eigenvalues, P = np.linalg.eig(A)

D = np.diag(eigenvalues)
P_inverse = np.linalg.inv(P)

A_reconstructed = P @ D @ P_inverse

print("P:")
print(P)

print("\nD:")
print(D)

print("\nP inverse:")
print(P_inverse)

print("\nP D P^-1:")
print(A_reconstructed)

print("\nMatches A:", np.allclose(A, A_reconstructed))
```

---

# 19. Why Is Diagonalization Useful?

Computing high powers such as

\[
A^{100}
\]

directly can be expensive.

If

\[
A=PDP^{-1},
\]

then

\[
A^k=PD^kP^{-1}.
\]

Since \(D\) is diagonal,

\[
D^k=
\begin{bmatrix}
\lambda_1^k&0&\cdots\\
0&\lambda_2^k&\cdots\\
\vdots&\vdots&\ddots
\end{bmatrix},
\]

which is easy to compute.

---

# 20. Important Properties of Eigenvalues

### Property 1 — Similar matrices have the same eigenvalues

If

\[
B=P^{-1}AP,
\]

then \(A\) and \(B\) have the same eigenvalues.

### Property 2 — Eigenvalues of \(A^k\)

If \(\lambda\) is an eigenvalue of \(A\), then

\[
\lambda^k
\]

is an eigenvalue of \(A^k\).

### Property 3 — Eigenvalues of \(A^{-1}\)

If \(A\) is invertible, the eigenvalues of \(A^{-1}\) are

\[
\frac{1}{\lambda_i}.
\]

### Property 4 — Eigenvalues of \(cA\)

The eigenvalues of \(cA\) are

\[
c\lambda_i.
\]

### Property 5 — Singular matrix

A matrix is singular if and only if \(0\) is one of its eigenvalues.

### Property 6 — Symmetric real matrix

A real symmetric matrix has:

- real eigenvalues,
- mutually orthogonal eigenvectors for distinct eigenvalues,
- an orthonormal eigenbasis.

---

# 21. Symmetric Matrices and `numpy.linalg.eigh`

For a real symmetric matrix, prefer `np.linalg.eigh()`.

```python
import numpy as np

A = np.array([
    [2, 1],
    [1, 2]
], dtype=float)

eigenvalues, eigenvectors = np.linalg.eigh(A)

print(eigenvalues)
print(eigenvectors)
```

`eigh()` exploits symmetry and is generally more appropriate for real symmetric or Hermitian matrices.

---

# 22. Complex Eigenvalues

Not every real matrix has real eigenvalues.

For example,

\[
A=
\begin{bmatrix}
0&-1\\
1&0
\end{bmatrix}
\]

represents a \(90^\circ\) rotation.

Its characteristic equation is

\[
\lambda^2+1=0.
\]

Hence,

\[
\lambda=\pm i.
\]

Python:

```python
import numpy as np

A = np.array([
    [0, -1],
    [1,  0]
])

values, vectors = np.linalg.eig(A)

print(values)
print(vectors)
```

This illustrates that eigenvalues and eigenvectors may be complex even when the matrix contains only real numbers.

---

# 23. Application — Principal Component Analysis (PCA)

One of the most important applications of eigenvalues and eigenvectors in machine learning is **Principal Component Analysis**.

PCA uses the eigenvectors of a covariance matrix to determine directions of maximum variance.

![PCA eigenvectors](figures/05_pca_eigenvectors.png)

**Figure 5.** The first principal component follows the direction with the largest variance.

Conceptually:

1. Center the dataset.
2. Calculate the covariance matrix.
3. Find its eigenvalues and eigenvectors.
4. Sort eigenvectors by decreasing eigenvalue.
5. Select the most important eigenvectors.
6. Project the data onto those directions.

---

# 24. PCA from Scratch Using Eigenvalues

```python
import numpy as np

X = np.array([
    [2.5, 2.4],
    [0.5, 0.7],
    [2.2, 2.9],
    [1.9, 2.2],
    [3.1, 3.0],
    [2.3, 2.7],
    [2.0, 1.6],
    [1.0, 1.1],
    [1.5, 1.6],
    [1.1, 0.9]
])

# Step 1: Center data
X_centered = X - np.mean(X, axis=0)

# Step 2: Covariance matrix
covariance_matrix = np.cov(X_centered, rowvar=False)

# Step 3: Eigenvalues/eigenvectors
eigenvalues, eigenvectors = np.linalg.eigh(covariance_matrix)

# Step 4: Sort in descending order
indices = np.argsort(eigenvalues)[::-1]
eigenvalues = eigenvalues[indices]
eigenvectors = eigenvectors[:, indices]

print("Covariance matrix:")
print(covariance_matrix)

print("\nEigenvalues:")
print(eigenvalues)

print("\nPrincipal directions:")
print(eigenvectors)

# Step 5: First principal component
principal_component = eigenvectors[:, 0]

# Step 6: Project
projected_data = X_centered @ principal_component

print("\n1-D projected data:")
print(projected_data)
```

---

# 25. Application — Dynamical Systems

Suppose

\[
x_{k+1}=Ax_k.
\]

Then

\[
x_k=A^kx_0.
\]

Eigenvalues determine long-term behavior.

- \(|\lambda|<1\): component tends to decay.
- \(|\lambda|>1\): component tends to grow.
- \(|\lambda|=1\): component may persist or oscillate.

This makes eigenvalues extremely important in **stability analysis**.

---

# 26. Application — Differential Equations

For

\[
\frac{d\mathbf{x}}{dt}=A\mathbf{x},
\]

solutions are closely related to eigenpairs.

If

\[
A\mathbf{v}=\lambda\mathbf{v},
\]

then

\[
\mathbf{x}(t)=e^{\lambda t}\mathbf{v}
\]

is a solution along that eigendirection.

Thus, the sign of the real part of \(\lambda\) helps determine whether the solution grows or decays.

---

# 27. Application — Graphs and PageRank

Eigenvectors are also used in graph analysis.

For an adjacency or transition matrix:

- eigenvalues provide information about graph structure,
- dominant eigenvectors can represent long-term importance,
- spectral methods are used in clustering and graph partitioning.

The basic idea behind PageRank is also related to finding a stationary vector associated with an eigenvalue of a transition matrix.

---

# 28. Power Iteration

For very large matrices, calculating every eigenvalue may be unnecessary.

**Power iteration** approximates the dominant eigenvector.

```python
import numpy as np

A = np.array([
    [2, 1],
    [1, 2]
], dtype=float)

v = np.array([1.0, 0.0])

for _ in range(20):
    v = A @ v
    v = v / np.linalg.norm(v)

lambda_estimate = (v @ A @ v) / (v @ v)

print("Dominant eigenvector:", v)
print("Dominant eigenvalue:", lambda_estimate)
```

For this example, the algorithm approaches the eigenvector associated with \(\lambda=3\).

---

# 29. Common Mistakes

### Mistake 1 — Allowing the zero vector as an eigenvector

The zero vector satisfies

\[
A0=\lambda0
\]

for every \(\lambda\), so it carries no useful directional information. It is therefore excluded by definition.

### Mistake 2 — Confusing eigenvalues with eigenvectors

An eigenvalue is a **scalar**; an eigenvector is a **non-zero vector**.

### Mistake 3 — Reading NumPy eigenvectors by row

With `np.linalg.eig(A)`, eigenvectors are stored in **columns**.

### Mistake 4 — Assuming every matrix is diagonalizable

A matrix may fail to have \(n\) linearly independent eigenvectors.

### Mistake 5 — Assuming eigenvalues must be positive

They may be positive, negative, zero, or complex.

---

# 30. Quick Revision Table

| Concept | Key Idea |
|---|---|
| Eigenvector | Special non-zero direction preserved by a transformation |
| Eigenvalue | Scaling factor associated with an eigenvector |
| Fundamental equation | \(A\mathbf{v}=\lambda\mathbf{v}\) |
| Characteristic equation | \(\det(A-\lambda I)=0\) |
| Eigenspace | \(\ker(A-\lambda I)\) |
| Trace | Sum of eigenvalues |
| Determinant | Product of eigenvalues |
| Diagonalization | \(A=PDP^{-1}\) |
| Symmetric matrix | Has real eigenvalues and orthogonal eigendirections |
| PCA | Uses covariance-matrix eigenvectors |
| Dominant eigenvalue | Eigenvalue with largest magnitude |

---

# 31. Practice Questions

### Conceptual Questions

1. What is an eigenvector?
2. Why is the zero vector not considered an eigenvector?
3. What does a negative eigenvalue mean geometrically?
4. What does an eigenvalue equal to zero indicate?
5. Why must \(\det(A-\lambda I)=0\)?
6. What is an eigenspace?
7. What is the difference between algebraic and geometric multiplicity?
8. When is a matrix diagonalizable?
9. Why are symmetric matrices especially important?
10. How are eigenvectors used in PCA?

### Numerical Problems

**Problem 1**

Find the eigenvalues and eigenvectors of

\[
A=
\begin{bmatrix}
3&1\\
0&2
\end{bmatrix}.
\]

**Problem 2**

Find the characteristic polynomial of

\[
A=
\begin{bmatrix}
4&2\\
1&3
\end{bmatrix}.
\]

**Problem 3**

Determine whether

\[
\mathbf{v}=
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

If it is, determine the eigenvalue.

---

# 32. Complete Python Example

```python
import numpy as np
import matplotlib.pyplot as plt

A = np.array([
    [2, 1],
    [1, 2]
], dtype=float)

# Compute eigenpairs
eigenvalues, eigenvectors = np.linalg.eig(A)

print("A:")
print(A)

print("\nEigenvalues:")
print(eigenvalues)

print("\nEigenvectors:")
print(eigenvectors)

# Verify each eigenpair
for i, lam in enumerate(eigenvalues):
    v = eigenvectors[:, i]

    print(f"\n--- Eigenpair {i + 1} ---")
    print("lambda =", lam)
    print("v =", v)
    print("A @ v =", A @ v)
    print("lambda * v =", lam * v)
    print("Verified =", np.allclose(A @ v, lam * v))

# Visualize
plt.figure(figsize=(7, 7))

for i in range(len(eigenvalues)):
    v = eigenvectors[:, i]

    plt.quiver(
        0, 0,
        v[0], v[1],
        angles="xy",
        scale_units="xy",
        scale=1,
        label=f"λ = {eigenvalues[i]:.2f}"
    )

plt.axhline(0)
plt.axvline(0)
plt.xlim(-1.5, 1.5)
plt.ylim(-1.5, 1.5)
plt.grid()
plt.legend()
plt.title("Eigenvectors")
plt.xlabel("x")
plt.ylabel("y")
plt.show()
```

---

# 33. Summary

Eigenvalues and eigenvectors provide a natural way to understand a linear transformation.

The central equation is

\[
\boxed{A\mathbf{v}=\lambda\mathbf{v}}.
\]

To calculate eigenvalues:

\[
\boxed{\det(A-\lambda I)=0}.
\]

After obtaining an eigenvalue, solve

\[
\boxed{(A-\lambda I)\mathbf{v}=0}
\]

to obtain its eigenvectors.

The most important ideas to remember are:

- Eigenvectors are special directions preserved by a transformation.
- Eigenvalues measure scaling along those directions.
- The determinant of \(A\) equals the product of its eigenvalues.
- The trace equals the sum of its eigenvalues.
- Diagonalization simplifies powers and many matrix computations.
- Symmetric matrices possess especially useful eigenvalue properties.
- Eigenvalues and eigenvectors are fundamental to PCA, dynamical systems, differential equations, graph algorithms, machine learning, and scientific computing.

---

## 📁 Figures Used in This Material

All figures are stored in the `figures/` directory so that the Markdown renders correctly on GitHub.

1. `figures/01_eigenvector_intuition.png`
2. `figures/02_circle_to_ellipse.png`
3. `figures/03_eigenvalue_effects.png`
4. `figures/04_diagonalization_flow.png`
5. `figures/05_pca_eigenvectors.png`

---

## Required Python Packages

```bash
pip install numpy matplotlib scikit-learn
```

---

**End of Reading Material**
