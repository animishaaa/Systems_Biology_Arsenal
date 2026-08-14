# 🧭 Eigenvectors and Eigenvalues

Eigenvectors and eigenvalues are fundamental concepts in **linear algebra** and are especially important in **multivariate statistics, PCA, machine learning, and data analysis**.

---

# 1. ⭐ What Is an Eigenvector?

## 🔍 Core Idea

An **eigenvector** is a special non-zero vector whose **direction is preserved** when a matrix acts on it.

A matrix may:

- 📏 Stretch the vector
- 🤏 Shrink the vector
- 🔄 Reverse its direction

However, the transformed vector remains on the **same line** as the original vector.

> 💡 **Simple idea:** An eigenvector represents a direction that is preserved by a matrix transformation.

---

## 📐 Mathematical Definition

A non-zero vector **v** is an eigenvector of a square matrix **A** if:

```math
Av = \lambda v
```

where:

- 🔢 $A$ = square matrix
- 🏹 $v$ = eigenvector
- ⭐ $\lambda$ = eigenvalue

The eigenvector must satisfy:

```math
v \neq 0
```

because the zero vector is **not considered an eigenvector**.

---

## 🏭 Simple Intuition: Matrix as a Machine

Imagine a matrix as a transformation machine:

```text
                 MATRIX A
Vector v  ─────► [ MACHINE ] ─────► Transformed Vector
```

For most vectors:

```text
Direction before ≠ Direction after
```

For an eigenvector:

```text
Direction before = Same line after
```

Only its **magnitude or orientation along that line** may change.

### 🧒 Easy Analogy

- 🏭 **Matrix:** "I'm a machine that transforms arrows."
- 🏹 **Vector:** "I'm an arrow."
- ⭐ **Eigenvector:** "I'm a special arrow. You can stretch, shrink, or flip me, but I stay on the same line."
- 🔢 **Eigenvalue:** "I'm the number that tells you how much that special arrow is scaled."

---

# 2. 🏹 Vectors – Quick Revision

A **vector** is an ordered collection of numbers.

For example:

```math
v =
\begin{bmatrix}
2 \\
3
\end{bmatrix}
```

This is a two-dimensional vector.

A vector has two important properties:

- 📏 **Magnitude** = its length
- 🧭 **Direction** = where it points

For eigenvectors, the most important feature is the **direction**.

> 💡 Multiplying an eigenvector by a non-zero scalar changes its magnitude and may reverse its orientation, but it remains on the same eigendirection.

---

# 3. ✖️ Scaling a Vector

Suppose:

```math
v =
\begin{bmatrix}
1 \\
2
\end{bmatrix}
```

Multiplying it by 2 gives:

```math
2v =
\begin{bmatrix}
2 \\
4
\end{bmatrix}
```

Similarly:

```math
3v =
\begin{bmatrix}
3 \\
6
\end{bmatrix}
```

All these vectors lie on the same line.

```text
v  = (1, 2)
2v = (2, 4)
3v = (3, 6)
```

> 📌 **Important:** Multiplication by a positive scalar changes the magnitude but preserves the direction. Multiplication by a negative scalar reverses the orientation while keeping the vector on the same line.

This concept is fundamental to understanding eigenvectors.

---

# 4. 🧮 The Eigenvector Equation

The fundamental eigenvector equation is:

```math
Av = \lambda v
```

### 🔹 Left Side

```math
Av
```

means:

> Apply the matrix transformation $A$ to vector $v$.

### 🔸 Right Side

```math
\lambda v
```

means:

> Scale vector $v$ by the number $\lambda$.

Therefore:

```math
Av = \lambda v
```

means that applying matrix $A$ to $v$ produces the same result as simply **scaling $v$**.

---

## 🧠 Interpreting $\lambda$

If:

```math
Av = 2v
```

the eigenvector is stretched by a factor of 2.

If:

```math
Av = 0.5v
```

the eigenvector is shrunk to half its original magnitude.

If:

```math
Av = -v
```

the eigenvector is reversed while remaining on the same line.

---

# 5. 🧩 Example Matrix

Consider the matrix:

```math
A =
\begin{bmatrix}
1 & 1 \\
2 & 0
\end{bmatrix}
```

We will use this matrix to:

1. 🧪 Test vectors
2. 🔢 Find eigenvalues
3. 🏹 Find eigenvectors
4. 📏 Normalize eigenvectors
5. ⟂ Discuss orthogonality

---

# 6. 🧪 Testing Whether a Vector Is an Eigenvector

To determine whether $v$ is an eigenvector of $A$, calculate:

```math
Av
```

Then ask:

> ❓ Is $Av$ a scalar multiple of $v$?

If:

```math
Av = \lambda v
```

for some scalar $\lambda$, then $v$ is an eigenvector.

---

## ✅ Example: An Eigenvector

Consider:

```math
v =
\begin{bmatrix}
2 \\
2
\end{bmatrix}
```

Using:

```math
A =
\begin{bmatrix}
1 & 1 \\
2 & 0
\end{bmatrix}
```

calculate:

```math
Av =
\begin{bmatrix}
1 & 1 \\
2 & 0
\end{bmatrix}
\begin{bmatrix}
2 \\
2
\end{bmatrix}
```

Multiplying gives:

```math
Av =
\begin{bmatrix}
1(2)+1(2) \\
2(2)+0(2)
\end{bmatrix}
=
\begin{bmatrix}
4 \\
4
\end{bmatrix}
```

Now:

```math
2v =
2
\begin{bmatrix}
2 \\
2
\end{bmatrix}
=
\begin{bmatrix}
4 \\
4
\end{bmatrix}
```

Therefore:

```math
Av = 2v
```

✅ $v$ is an **eigenvector**.

Its eigenvalue is:

```math
\lambda = 2
```

---

## ❌ Example: Not an Eigenvector

Now consider:

```math
v =
\begin{bmatrix}
1 \\
0
\end{bmatrix}
```

Calculate:

```math
Av =
\begin{bmatrix}
1 & 1 \\
2 & 0
\end{bmatrix}
\begin{bmatrix}
1 \\
0
\end{bmatrix}
```

Multiplying gives:

```math
Av =
\begin{bmatrix}
1(1)+1(0) \\
2(1)+0(0)
\end{bmatrix}
=
\begin{bmatrix}
1 \\
2
\end{bmatrix}
```

For $v$ to be an eigenvector, there must be some scalar $\lambda$ such that:

```math
\begin{bmatrix}
1 \\
2
\end{bmatrix}
=
\lambda
\begin{bmatrix}
1 \\
0
\end{bmatrix}
```

But:

```math
\lambda
\begin{bmatrix}
1 \\
0
\end{bmatrix}
=
\begin{bmatrix}
\lambda \\
0
\end{bmatrix}
```

The second component is always zero, so it can never equal:

```math
\begin{bmatrix}
1 \\
2
\end{bmatrix}
```

Therefore:

- ❌ Direction changed
- ❌ $Av$ is not a scalar multiple of $v$
- ➡️ $v$ is **not an eigenvector**

---

# 7. 🔢 What Is an Eigenvalue?

An **eigenvalue** tells us how much the corresponding eigenvector is scaled.

The eigenvector equation is:

```math
Av = \lambda v
```

Here, $\lambda$ is the **eigenvalue**.

### 📌 Example

If:

```math
Av = 2v
```

then:

```math
\lambda = 2
```

➡️ The eigenvector is stretched by a factor of 2.

---

## 🔍 Interpreting Eigenvalues

| Eigenvalue | Effect |
|---|---|
| $\lambda > 1$ | 📈 Vector stretches |
| $0 < \lambda < 1$ | 📉 Vector shrinks |
| $\lambda = 1$ | ➡️ Vector remains unchanged |
| $\lambda = 0$ | 🔴 Vector collapses to zero |
| $\lambda < 0$ | 🔄 Vector reverses orientation and is scaled |

> 💡 The magnitude $|\lambda|$ describes the scaling factor. The sign indicates whether the orientation is reversed.

---

# 8. ♾️ Many Eigenvectors for One Eigenvalue

Suppose:

```math
Av = \lambda v
```

If $c$ is any non-zero scalar:

```math
A(cv) = cAv
```

Since:

```math
Av = \lambda v
```

we obtain:

```math
A(cv) = c\lambda v
```

Therefore:

```math
A(cv) = \lambda(cv)
```

Thus:

```math
\boxed{cv \text{ is also an eigenvector}}
```

### 📌 Example

If:

```math
v =
\begin{bmatrix}
1 \\
1
\end{bmatrix}
```

is an eigenvector, then:

```math
\begin{bmatrix}
2 \\
2
\end{bmatrix},
\qquad
\begin{bmatrix}
3 \\
3
\end{bmatrix},
\qquad
\begin{bmatrix}
-1 \\
-1
\end{bmatrix}
```

are also eigenvectors corresponding to the same eigenvalue.

> ⭐ Eigenvectors are not unique. Every non-zero scalar multiple of an eigenvector is another eigenvector for the same eigenvalue.

---

# 9. 📏 Normalized Eigenvectors

Eigenvectors are often converted to **unit vectors**.

A unit vector satisfies:

```math
\|v\| = 1
```

The notation:

```math
\|v\|
```

represents the **Euclidean norm**, or length, of vector $v$.

---

## 🧮 Step 1: Calculate the Length

For:

```math
v =
\begin{bmatrix}
a \\
b
\end{bmatrix}
```

the Euclidean norm is:

```math
\|v\|
=
\sqrt{a^2+b^2}
```

---

## 🧮 Step 2: Normalize the Vector

The normalized vector is:

```math
\hat{v}
=
\frac{v}{\|v\|}
```

### 📌 Example

Consider:

```math
v =
\begin{bmatrix}
1 \\
1
\end{bmatrix}
```

Its length is:

```math
\|v\|
=
\sqrt{1^2+1^2}
=
\sqrt{2}
```

Therefore:

```math
\hat{v}
=
\frac{v}{\|v\|}
=
\frac{1}{\sqrt{2}}
\begin{bmatrix}
1 \\
1
\end{bmatrix}
```

This can also be written as:

```math
\hat{v}
=
\begin{bmatrix}
\frac{1}{\sqrt{2}} \\
\frac{1}{\sqrt{2}}
\end{bmatrix}
```

Approximately:

```math
\hat{v}
\approx
\begin{bmatrix}
0.707 \\
0.707
\end{bmatrix}
```

Check the length:

```math
\|\hat{v}\|
=
\sqrt{(0.707)^2+(0.707)^2}
\approx 1
```

✅ The vector is normalized.

---

## 🎯 Why Normalize Eigenvectors?

Normalization is useful in:

- 📊 PCA
- 📈 Multivariate statistics
- 🧭 Direction comparison
- 💻 Numerical calculations
- 🔄 Coordinate transformations

---

# 10. 🔎 Finding Eigenvalues – Core Procedure

Start with:

```math
Av = \lambda v
```

## Step 1️⃣: Rearrange the Equation

```math
Av-\lambda v=0
```

Since:

```math
v=Iv
```

we can write:

```math
Av-\lambda Iv=0
```

Factor out $v$:

```math
(A-\lambda I)v=0
```

where $I$ is the identity matrix.

---

## Step 2️⃣: Characteristic Equation

For a non-zero solution $v$ to exist, $A-\lambda I$ must be singular.

Therefore:

```math
\boxed{\det(A-\lambda I)=0}
```

This is called the **characteristic equation**.

---

## Step 3️⃣: Apply It to Our Example

Recall:

```math
A =
\begin{bmatrix}
1 & 1 \\
2 & 0
\end{bmatrix}
```

The identity matrix is:

```math
I =
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
```

Multiply $I$ by $\lambda$:

```math
\lambda I =
\begin{bmatrix}
\lambda & 0 \\
0 & \lambda
\end{bmatrix}
```

Therefore:

```math
A-\lambda I
=
\begin{bmatrix}
1 & 1 \\
2 & 0
\end{bmatrix}
-
\begin{bmatrix}
\lambda & 0 \\
0 & \lambda
\end{bmatrix}
```

which gives:

```math
A-\lambda I
=
\begin{bmatrix}
1-\lambda & 1 \\
2 & -\lambda
\end{bmatrix}
```

---

## 🧮 Calculate the Determinant

For a $2\times2$ matrix:

```math
\begin{bmatrix}
a & b \\
c & d
\end{bmatrix}
```

the determinant is:

```math
ad-bc
```

Therefore:

```math
\det(A-\lambda I)
=
\begin{vmatrix}
1-\lambda & 1 \\
2 & -\lambda
\end{vmatrix}
```

So:

```math
\det(A-\lambda I)
=
(1-\lambda)(-\lambda)-(1)(2)
```

Expand:

```math
(1-\lambda)(-\lambda)
=
-\lambda+\lambda^2
```

Therefore:

```math
\lambda^2-\lambda-2=0
```

This is the **characteristic polynomial equation**.

---

## Step 4️⃣: Solve the Characteristic Polynomial

Factor:

```math
\lambda^2-\lambda-2
=
(\lambda-2)(\lambda+1)
```

Set equal to zero:

```math
(\lambda-2)(\lambda+1)=0
```

Therefore:

```math
\lambda-2=0
```

or:

```math
\lambda+1=0
```

Hence:

```math
\boxed{\lambda_1=2}
```

and:

```math
\boxed{\lambda_2=-1}
```

These are the eigenvalues of matrix $A$.

---

# 11. 🏹 Finding Eigenvectors for Each Eigenvalue

After finding the eigenvalues, substitute each eigenvalue into:

```math
(A-\lambda I)v=0
```

---

## ⭐ Eigenvector for $\lambda=2$

Substitute:

```math
\lambda=2
```

Then:

```math
A-2I
=
\begin{bmatrix}
1 & 1 \\
2 & 0
\end{bmatrix}
-
2
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
```

Therefore:

```math
A-2I
=
\begin{bmatrix}
1 & 1 \\
2 & 0
\end{bmatrix}
-
\begin{bmatrix}
2 & 0 \\
0 & 2
\end{bmatrix}
```

which gives:

```math
A-2I
=
\begin{bmatrix}
-1 & 1 \\
2 & -2
\end{bmatrix}
```

Let:

```math
v =
\begin{bmatrix}
x \\
y
\end{bmatrix}
```

Then:

```math
(A-2I)v=0
```

becomes:

```math
\begin{bmatrix}
-1 & 1 \\
2 & -2
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
=
\begin{bmatrix}
0 \\
0
\end{bmatrix}
```

Multiplying gives:

```math
\begin{bmatrix}
-x+y \\
2x-2y
\end{bmatrix}
=
\begin{bmatrix}
0 \\
0
\end{bmatrix}
```

Therefore:

```math
-x+y=0
```

and:

```math
2x-2y=0
```

Both equations give:

```math
y=x
```

Choose:

```math
x=1
```

Then:

```math
y=1
```

Therefore, one eigenvector is:

```math
\boxed{
v_1=
\begin{bmatrix}
1 \\
1
\end{bmatrix}
}
```

Any non-zero scalar multiple is also valid:

```math
c
\begin{bmatrix}
1 \\
1
\end{bmatrix},
\qquad c\neq0
```

---

## ⭐ Eigenvector for $\lambda=-1$

Substitute:

```math
\lambda=-1
```

Then:

```math
A-\lambda I
=
A-(-1)I
=
A+I
```

Therefore:

```math
A+I
=
\begin{bmatrix}
1 & 1 \\
2 & 0
\end{bmatrix}
+
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
```

which gives:

```math
A+I
=
\begin{bmatrix}
2 & 1 \\
2 & 1
\end{bmatrix}
```

Let:

```math
v =
\begin{bmatrix}
x \\
y
\end{bmatrix}
```

Then:

```math
(A+I)v=0
```

becomes:

```math
\begin{bmatrix}
2 & 1 \\
2 & 1
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
=
\begin{bmatrix}
0 \\
0
\end{bmatrix}
```

Multiplying gives:

```math
\begin{bmatrix}
2x+y \\
2x+y
\end{bmatrix}
=
\begin{bmatrix}
0 \\
0
\end{bmatrix}
```

Therefore:

```math
2x+y=0
```

Solve for $y$:

```math
y=-2x
```

Choose:

```math
x=1
```

Then:

```math
y=-2
```

Therefore:

```math
\boxed{
v_2=
\begin{bmatrix}
1 \\
-2
\end{bmatrix}
}
```

Any non-zero scalar multiple is also valid:

```math
c
\begin{bmatrix}
1 \\
-2
\end{bmatrix},
\qquad c\neq0
```

---

# 12. ✅ Verifying the Eigenvectors

Always verify an eigenvector using:

```math
Av=\lambda v
```

---

## 🔍 Check $\lambda=2$

We found:

```math
v_1=
\begin{bmatrix}
1 \\
1
\end{bmatrix}
```

Calculate:

```math
Av_1
=
\begin{bmatrix}
1 & 1 \\
2 & 0
\end{bmatrix}
\begin{bmatrix}
1 \\
1
\end{bmatrix}
```

Multiplying:

```math
Av_1
=
\begin{bmatrix}
1(1)+1(1) \\
2(1)+0(1)
\end{bmatrix}
=
\begin{bmatrix}
2 \\
2
\end{bmatrix}
```

Now:

```math
2v_1
=
2
\begin{bmatrix}
1 \\
1
\end{bmatrix}
=
\begin{bmatrix}
2 \\
2
\end{bmatrix}
```

Therefore:

```math
\boxed{Av_1=2v_1}
```

✅ **Correct**

---

## 🔍 Check $\lambda=-1$

We found:

```math
v_2=
\begin{bmatrix}
1 \\
-2
\end{bmatrix}
```

Calculate:

```math
Av_2
=
\begin{bmatrix}
1 & 1 \\
2 & 0
\end{bmatrix}
\begin{bmatrix}
1 \\
-2
\end{bmatrix}
```

Multiplying:

```math
Av_2
=
\begin{bmatrix}
1(1)+1(-2) \\
2(1)+0(-2)
\end{bmatrix}
=
\begin{bmatrix}
-1 \\
2
\end{bmatrix}
```

Now:

```math
-v_2
=
-
\begin{bmatrix}
1 \\
-2
\end{bmatrix}
=
\begin{bmatrix}
-1 \\
2
\end{bmatrix}
```

Therefore:

```math
\boxed{Av_2=-v_2}
```

✅ **Correct**

---

# 13. ⟂ Orthogonal Eigenvectors

## 📐 Definition

Two vectors are **orthogonal** when their dot product equals zero.

```math
v_1^T v_2=0
```

or:

```math
v_1\cdot v_2=0
```

---

## 📌 Simple Example

Consider:

```math
u=
\begin{bmatrix}
1 \\
1
\end{bmatrix}
```

and:

```math
w=
\begin{bmatrix}
1 \\
-1
\end{bmatrix}
```

Their dot product is:

```math
u\cdot w
=
(1)(1)+(1)(-1)
```

Therefore:

```math
u\cdot w
=
1-1
=
0
```

Hence:

```math
\boxed{u\perp w}
```

✅ The vectors are orthogonal.

---

## ⚠️ Are Our Eigenvectors Orthogonal?

Our eigenvectors are:

```math
v_1=
\begin{bmatrix}
1 \\
1
\end{bmatrix}
```

and:

```math
v_2=
\begin{bmatrix}
1 \\
-2
\end{bmatrix}
```

Calculate:

```math
v_1\cdot v_2
=
(1)(1)+(1)(-2)
```

Therefore:

```math
v_1\cdot v_2
=
1-2
=
-1
```

Since:

```math
-1\neq0
```

the eigenvectors are **not orthogonal**.

```math
v_1\not\perp v_2
```

> 💡 Eigenvectors corresponding to different eigenvalues are **not automatically orthogonal for every matrix**.

---

# 14. 📊 Eigenvectors and Symmetric Matrices

A symmetric matrix satisfies:

```math
A=A^T
```

For example:

```math
A=
\begin{bmatrix}
2 & 1 \\
1 & 2
\end{bmatrix}
```

A real symmetric matrix has several important properties:

- ✅ Its eigenvalues are real
- ⟂ Eigenvectors corresponding to distinct eigenvalues are orthogonal
- 📏 Eigenvectors can be normalized
- 🧭 An orthonormal eigenvector basis can be constructed

This is especially important because **covariance matrices and correlation matrices are symmetric**.

Therefore, these properties are fundamental to **PCA**.

---

# 15. 📏 Orthogonal vs. Orthonormal

## ⟂ Orthogonal

Vectors are orthogonal when:

```math
v_i^Tv_j=0
```

for:

```math
i\neq j
```

## 📏 Normalized

A vector is normalized when:

```math
\|v\|=1
```

## ⭐ Orthonormal

A collection of vectors is **orthonormal** when:

1. ⟂ The vectors are mutually orthogonal
2. 📏 Every vector has unit length

For an orthonormal set:

```math
v_i^Tv_j=
\begin{cases}
1, & i=j \\
0, & i\neq j
\end{cases}
```

In simple terms:

```text
Orthogonal
    +
Unit Length
    ↓
Orthonormal
```

---

# 16. 🧠 Complete Eigenvalue/Eigenvector Workflow

```text
                    MATRIX A
                       ↓
                 Av = λv
                       ↓
                (A-λI)v = 0
                       ↓
              det(A-λI) = 0
                       ↓
          Characteristic equation
                       ↓
                 Solve for λ
                       ↓
                  Eigenvalues
                       ↓
         Substitute each λ separately
                       ↓
                (A-λI)v = 0
                       ↓
               Solve for v
                       ↓
                  Eigenvectors
                       ↓
              Normalize if needed
                       ↓
                Verify Av = λv
                       ↓
          Check orthogonality if needed
```

> 🎯 **Exam tip:**  
> **Determinant → Eigenvalues → Eigenvectors → Normalize → Verify**

---

# 17. 📋 Key Formulas

## ⭐ Eigenvector Equation

```math
\boxed{Av=\lambda v}
```

## 🔎 Characteristic Equation

```math
\boxed{\det(A-\lambda I)=0}
```

## 🏹 Finding Eigenvectors

```math
\boxed{(A-\lambda I)v=0}
```

## 📏 Vector Length

For:

```math
v=
\begin{bmatrix}
v_1 \\
v_2 \\
\vdots \\
v_n
\end{bmatrix}
```

the Euclidean norm is:

```math
\boxed{
\|v\|
=
\sqrt{
v_1^2+v_2^2+\cdots+v_n^2
}
}
```

## 📐 Normalization

```math
\boxed{
\hat{v}
=
\frac{v}{\|v\|}
}
```

## ⟂ Orthogonality

```math
\boxed{
v_1^Tv_2=0
}
```

---

# 18. 📊 Why Eigenvectors Matter in PCA

Eigenvalues and eigenvectors form the mathematical foundation of **Principal Component Analysis (PCA)**.

PCA finds new directions that explain variation in multivariate data.

Suppose the original variables are:

```text
X₁
X₂
X₃
X₄
```

PCA transforms these variables into:

```text
PC1
PC2
PC3
PC4
```

These principal-component directions are obtained from the **eigenvectors of the covariance or correlation matrix**.

---

## 🏹 Eigenvectors in PCA

Eigenvectors determine:

> 🧭 **The directions of the principal components**

```text
Eigenvector 1 → Direction of PC1
Eigenvector 2 → Direction of PC2
Eigenvector 3 → Direction of PC3
```

---

## 🔢 Eigenvalues in PCA

Eigenvalues indicate how much variance is associated with each principal component.

Usually:

```math
\lambda_1
\geq
\lambda_2
\geq
\lambda_3
\geq
\cdots
```

Therefore:

```text
Largest eigenvalue
        ↓
Largest amount of variance
        ↓
First principal component (PC1)
```

> 💡 In PCA, **eigenvectors determine the directions**, while **eigenvalues quantify the variance associated with those directions**.

---

## 📊 Proportion of Variance Explained

If the eigenvalues are:

```math
\lambda_1,\lambda_2,\ldots,\lambda_p
```

then the proportion of variance explained by principal component $i$ is:

```math
\text{Proportion of Variance Explained by PC}_i
=
\frac{\lambda_i}
{\lambda_1+\lambda_2+\cdots+\lambda_p}
```

---

# 19. 🧬 Why This Matters in Biology and Data Analysis

Eigenvalues and eigenvectors are widely used in:

- 🧬 Gene expression analysis
- 📊 Principal Component Analysis
- 🔬 Feature extraction
- 📉 Dimensionality reduction
- 🧫 Systems biology
- 🧩 Pattern recognition
- 💻 Machine learning

### 🧬 Gene Expression Example

Gene-expression datasets may contain:

```text
Thousands of genes
       ↓
Hundreds of samples
       ↓
High-dimensional dataset
```

PCA can transform these correlated variables into a smaller number of principal components.

```text
Original Variables
X₁ X₂ X₃ X₄ X₅ ... Xₙ
          ↓
         PCA
          ↓
      PC1 PC2 PC3 ...
```

This can help:

- 📉 Reduce dimensionality
- 🔍 Reveal biological patterns
- 🧩 Identify sample clusters
- ⚠️ Detect unusual samples
- 📊 Visualize complex datasets
- 💻 Reduce computational complexity

---

# 20. 🧒 Eigenvectors Explained Like You're Five

### 🏭 Matrix

> "I'm a machine that transforms arrows."

### 🏹 Vector

> "I'm an arrow. I have a length and a direction."

### ⭐ Eigenvector

> "I'm a special arrow. When I enter the machine, I stay on the same line."

### 🔢 Eigenvalue

> "I'm the number that tells you how much that special arrow gets stretched, shrunk, or flipped."

### 🎨 Visual Idea

```text
Normal Vector

Before:  ↗
          │
          ▼
      [ MATRIX ]
          │
          ▼
After:   ➡

Direction changed ❌
Not an eigenvector


Eigenvector

Before:   ↗
           │
           ▼
       [ MATRIX ]
           │
           ▼
After:    ↗↗↗

Same line ✅
Eigenvector ⭐
```

---

# 21. 🧠 Key Takeaways

| Concept | 💡 Meaning |
|---|---|
| 🏹 **Vector** | Has magnitude and direction |
| ⭐ **Eigenvector** | Direction preserved under a matrix transformation |
| 🔢 **Eigenvalue** | Scaling factor associated with an eigenvector |
| 📏 **Normalized eigenvector** | Eigenvector with length 1 |
| ⟂ **Orthogonal vectors** | Vectors whose dot product equals zero |
| ⭐ **Orthonormal vectors** | Orthogonal vectors with unit length |
| 🧮 **Characteristic equation** | $\det(A-\lambda I)=0$ |
| 📊 **PCA eigenvectors** | Determine principal-component directions |
| 📈 **PCA eigenvalues** | Determine variance associated with principal components |

---

# 22. 🎯 Final Summary

The fundamental eigenvector equation is:

```math
\boxed{Av=\lambda v}
```

To calculate eigenvalues:

```math
\boxed{\det(A-\lambda I)=0}
```

To find an eigenvector:

```math
\boxed{(A-\lambda I)v=0}
```

To calculate vector length:

```math
\boxed{
\|v\|
=
\sqrt{v_1^2+v_2^2+\cdots+v_n^2}
}
```

To normalize an eigenvector:

```math
\boxed{
\hat{v}
=
\frac{v}{\|v\|}
}
```

To check orthogonality:

```math
\boxed{v_1^Tv_2=0}
```

---

## 🚀 The Big Picture

```text
                MATRIX
                   ↓
        Eigenvalues + Eigenvectors
                   ↓
       Understand transformation
                   ↓
        Find important directions
                   ↓
                  PCA
                   ↓
        Dimensionality Reduction
                   ↓
         Multivariate Analysis
                   ↓
      Machine Learning & Data Science
```

> 🌟 **Final takeaway:**  
> **Eigenvectors identify special directions preserved by a matrix transformation. Eigenvalues describe how strongly those directions are scaled. In PCA, eigenvectors define principal-component directions, while eigenvalues quantify the variance associated with those directions.**
