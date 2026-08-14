# 🧭 Eigenvectors and Eigenvalues

Eigenvectors and eigenvalues are fundamental concepts in **linear algebra** and are especially important in **multivariate statistics, PCA, machine learning, and data analysis**.

---

# 1. ⭐ What Is an Eigenvector?

## 🔍 Core Idea

An **eigenvector** is a special non-zero vector whose **direction is preserved** when a matrix acts on it.

A matrix may:

* 📏 Stretch the vector
* 🤏 Shrink the vector
* 🔄 Reverse its direction

However, the transformed vector remains on the **same line** as the original vector.

> 💡 **Simple idea:** An eigenvector represents a direction that is preserved by a matrix transformation.

---

## 📐 Mathematical Definition

A non-zero vector **v** is an eigenvector of a square matrix **A** if:

$$
Av = \lambda v
$$

where:

* 🔢 $A$ = square matrix
* 🏹 $v$ = eigenvector
* ⭐ $\lambda$ = eigenvalue

The eigenvector must satisfy:

$$
v \neq 0
$$

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

* 🏭 **Matrix:** "I'm a machine that transforms arrows."
* 🏹 **Vector:** "I'm an arrow."
* ⭐ **Eigenvector:** "I'm a special arrow. You can stretch, shrink, or flip me, but I stay on the same line."
* 🔢 **Eigenvalue:** "I'm the number that tells you how much that special arrow is scaled."

---

# 2. 🏹 Vectors – Quick Revision

A **vector** is an ordered collection of numbers.

For example:

$$
v =
\begin{bmatrix}
2 \
3
\end{bmatrix}
$$

This is a two-dimensional vector.

A vector has two important properties:

* 📏 **Magnitude** = its length
* 🧭 **Direction** = where it points

For eigenvectors, the most important feature is the **direction**.

> 💡 Multiplying an eigenvector by any non-zero scalar changes its magnitude and possibly its orientation, but it remains on the same eigendirection.

---

# 3. ✖️ Scaling a Vector

Suppose:

$$
v =
\begin{bmatrix}
1 \
2
\end{bmatrix}
$$

Multiplying it by 2 gives:

$$
2v =
\begin{bmatrix}
2 \
4
\end{bmatrix}
$$

Similarly:

$$
3v =
\begin{bmatrix}
3 \
6
\end{bmatrix}
$$

All these vectors lie on the same line.

```text
v  = (1, 2)
2v = (2, 4)
3v = (3, 6)
```

> 📌 **Important:** Multiplication by a positive scalar changes the magnitude but preserves the direction. A negative scalar reverses the orientation while keeping the vector on the same line.

This idea is fundamental to understanding eigenvectors.

---

# 4. 🧮 The Eigenvector Equation

The fundamental equation is:

$$
Av = \lambda v
$$

### Left Side

$$
Av
$$

means:

> Apply the matrix transformation $A$ to vector $v$.

### Right Side

$$
\lambda v
$$

means:

> Scale vector $v$ by the number $\lambda$.

Therefore:

$$
Av = \lambda v
$$

means that applying the matrix to $v$ produces the same result as simply **scaling $v$**.

---

## 🧠 Interpreting $\lambda$

If:

$$
Av = 2v
$$

the vector is stretched by a factor of 2.

If:

$$
Av = 0.5v
$$

the vector is shrunk to half its original magnitude.

If:

$$
Av = -v
$$

the vector is reversed while remaining on the same line.

---

# 5. 🧩 Example Matrix

Consider:

$$
A =
\begin{bmatrix}
1 & 1 \
2 & 0
\end{bmatrix}
$$

We will use this matrix to:

1. 🧪 Test vectors
2. 🔢 Find eigenvalues
3. 🏹 Find eigenvectors
4. 📏 Normalize eigenvectors
5. ⟂ Discuss orthogonality

---

# 6. 🧪 Testing Whether a Vector Is an Eigenvector

To determine whether $v$ is an eigenvector of $A$, calculate:

$$
Av
$$

Then ask:

> ❓ Is $Av$ a scalar multiple of $v$?

If:

$$
Av = \lambda v
$$

for some scalar $\lambda$, then $v$ is an eigenvector.

---

## ✅ Example: An Eigenvector

Consider:

$$
v =
\begin{bmatrix}
2 \
2
\end{bmatrix}
$$

Then:

$$
Av =
\begin{bmatrix}
1 & 1 \
2 & 0
\end{bmatrix}
\begin{bmatrix}
2 \
2
\end{bmatrix}
$$

Therefore:

$$
Av =
\begin{bmatrix}
4 \
4
\end{bmatrix}
$$

But:

$$
2v =
2
\begin{bmatrix}
2 \
2
\end{bmatrix}
=============

\begin{bmatrix}
4 \
4
\end{bmatrix}
$$

Therefore:

$$
Av = 2v
$$

✅ $v$ is an **eigenvector**.

⭐ Its eigenvalue is:

$$
\lambda = 2
$$

---

## ❌ Example: Not an Eigenvector

Now consider:

$$
v =
\begin{bmatrix}
1 \
0
\end{bmatrix}
$$

Then:

$$
Av =
\begin{bmatrix}
1 & 1 \
2 & 0
\end{bmatrix}
\begin{bmatrix}
1 \
0
\end{bmatrix}
=============

\begin{bmatrix}
1 \
2
\end{bmatrix}
$$

There is no scalar $\lambda$ such that:

$$
\begin{bmatrix}
1 \
2
\end{bmatrix}
=============

\lambda
\begin{bmatrix}
1 \
0
\end{bmatrix}
$$

Therefore:

* ❌ Direction changed
* ❌ $Av$ is not a scalar multiple of $v$
* ➡️ $v$ is **not an eigenvector**

---

# 7. 🔢 What Is an Eigenvalue?

The **eigenvalue** tells us how much the corresponding eigenvector is scaled.

If:

$$
Av = \lambda v
$$

then $\lambda$ is the eigenvalue.

### 📌 Example

If:

$$
Av = 2v
$$

then:

$$
\lambda = 2
$$

➡️ The eigenvector is stretched by a factor of 2.

---

## 🔍 Interpreting Eigenvalues

| Eigenvalue        | Effect                             |
| ----------------- | ---------------------------------- |
| $\lambda > 1$     | 📈 Stretches                       |
| $0 < \lambda < 1$ | 📉 Shrinks                         |
| $\lambda = 1$     | ➡️ Unchanged                       |
| $\lambda = 0$     | 🔴 Collapses to the zero vector    |
| $\lambda < 0$     | 🔄 Reverses orientation and scales |

> 💡 The magnitude $|\lambda|$ determines the scaling factor, while the sign indicates whether the orientation is reversed.

---

# 8. ♾️ Many Eigenvectors for One Eigenvalue

Suppose:

$$
Av = \lambda v
$$

If $c$ is any non-zero scalar, then:

$$
A(cv) = cAv
$$

Since:

$$
Av = \lambda v
$$

we obtain:

$$
A(cv) = c\lambda v
$$

and therefore:

$$
A(cv) = \lambda(cv)
$$

Thus:

$$
\boxed{cv \text{ is also an eigenvector}}
$$

### 📌 Example

If:

$$
v =
\begin{bmatrix}
1 \
1
\end{bmatrix}
$$

is an eigenvector, then:

$$
\begin{bmatrix}
2 \
2
\end{bmatrix},
\qquad
\begin{bmatrix}
3 \
3
\end{bmatrix},
\qquad
\begin{bmatrix}
-1 \
-1
\end{bmatrix}
$$

are also eigenvectors corresponding to the same eigenvalue.

> ⭐ Eigenvectors are therefore not unique. Any non-zero scalar multiple of an eigenvector is another eigenvector for the same eigenvalue.

---

# 9. 📏 Normalized Eigenvectors

Eigenvectors are often normalized so that their length equals 1.

A normalized vector satisfies:

$$
|v| = 1
$$

---

## 🧮 Step 1: Calculate the Length

For:

$$
v =
\begin{bmatrix}
a \
b
\end{bmatrix}
$$

the Euclidean norm is:

$$
|v| = \sqrt{a^2+b^2}
$$

---

## 🧮 Step 2: Normalize

The normalized eigenvector is:

$$
\hat{v} = \frac{v}{|v|}
$$

### 📌 Example

For:

$$
v =
\begin{bmatrix}
1 \
1
\end{bmatrix}
$$

the length is:

$$
|v|
===

# \sqrt{1^2+1^2}

\sqrt{2}
$$

Therefore:

$$
\hat{v}
=======

\frac{1}{\sqrt{2}}
\begin{bmatrix}
1 \
1
\end{bmatrix}
$$

or:

$$
\hat{v}
=======

\begin{bmatrix}
\frac{1}{\sqrt{2}} \
\frac{1}{\sqrt{2}}
\end{bmatrix}
$$

Approximately:

$$
\hat{v}
\approx
\begin{bmatrix}
0.707 \
0.707
\end{bmatrix}
$$

### 🎯 Why Normalize?

Normalization is useful in:

* 📊 PCA
* 📈 Multivariate statistics
* 🧭 Direction comparison
* 💻 Numerical calculations
* 🔄 Coordinate transformations

---

# 10. 🔎 Finding Eigenvalues – Core Procedure

We start with:

$$
Av = \lambda v
$$

## Step 1️⃣: Rearrange

$$
Av - \lambda v = 0
$$

Because:

$$
v = Iv
$$

we can write:

$$
Av - \lambda Iv = 0
$$

Factor out $v$:

$$
(A-\lambda I)v = 0
$$

where $I$ is the identity matrix.

---

## Step 2️⃣: Characteristic Equation

For a non-zero solution $v$ to exist, the matrix $A-\lambda I$ must be singular.

Therefore:

$$
\boxed{\det(A-\lambda I)=0}
$$

This is the **characteristic equation**.

---

## Step 3️⃣: Apply It to Our Matrix

Recall:

$$
A =
\begin{bmatrix}
1 & 1 \
2 & 0
\end{bmatrix}
$$

The identity matrix is:

$$
I =
\begin{bmatrix}
1 & 0 \
0 & 1
\end{bmatrix}
$$

Therefore:

$$
A-\lambda I
===========

\begin{bmatrix}
1-\lambda & 1 \
2 & -\lambda
\end{bmatrix}
$$

Now calculate the determinant:

$$
\det(A-\lambda I)
=================

(1-\lambda)(-\lambda)-(1)(2)
$$

Expanding:

$$
-\lambda+\lambda^2-2=0
$$

Rearrange:

$$
\lambda^2-\lambda-2=0
$$

---

## Step 4️⃣: Solve the Characteristic Polynomial

Factor:

$$
\lambda^2-\lambda-2
===================

(\lambda-2)(\lambda+1)
$$

Therefore:

$$
(\lambda-2)(\lambda+1)=0
$$

So:

$$
\boxed{\lambda_1=2}
$$

and:

$$
\boxed{\lambda_2=-1}
$$

These are the two eigenvalues of $A$.

---

## 🧠 Eigenvalue Workflow

```text
Av = λv
   ↓
Av - λv = 0
   ↓
(A - λI)v = 0
   ↓
det(A - λI) = 0
   ↓
Characteristic polynomial
   ↓
Solve for λ
   ↓
Eigenvalues
```

---

# 11. 🏹 Finding Eigenvectors for Each Eigenvalue

Once the eigenvalues are known, substitute each eigenvalue into:

$$
(A-\lambda I)v=0
$$

---

## ⭐ Eigenvector for $\lambda=2$

Substitute:

$$
\lambda=2
$$

Then:

$$
A-2I
====

\begin{bmatrix}
-1 & 1 \
2 & -2
\end{bmatrix}
$$

Let:

$$
v =
\begin{bmatrix}
x \
y
\end{bmatrix}
$$

Then:

$$
\begin{bmatrix}
-1 & 1 \
2 & -2
\end{bmatrix}
\begin{bmatrix}
x \
y
\end{bmatrix}
=============

\begin{bmatrix}
0 \
0
\end{bmatrix}
$$

Multiplying gives:

$$
\begin{bmatrix}
-x+y \
2x-2y
\end{bmatrix}
=============

\begin{bmatrix}
0 \
0
\end{bmatrix}
$$

Therefore:

$$
-x+y=0
$$

and:

$$
2x-2y=0
$$

Both equations give the same relationship:

$$
y=x
$$

Choose:

$$
x=1
$$

Then:

$$
y=1
$$

Therefore, one eigenvector is:

$$
\boxed{
v_1=
\begin{bmatrix}
1 \
1
\end{bmatrix}
}
$$

Any non-zero scalar multiple of this vector is also an eigenvector.

---

## ⭐ Eigenvector for $\lambda=-1$

Substitute:

$$
\lambda=-1
$$

Since:

$$
A-(-1)I=A+I
$$

we obtain:

$$
A+I
===

\begin{bmatrix}
2 & 1 \
2 & 1
\end{bmatrix}
$$

Again let:

$$
v =
\begin{bmatrix}
x \
y
\end{bmatrix}
$$

Then:

$$
\begin{bmatrix}
2 & 1 \
2 & 1
\end{bmatrix}
\begin{bmatrix}
x \
y
\end{bmatrix}
=============

\begin{bmatrix}
0 \
0
\end{bmatrix}
$$

Multiplying gives:

$$
\begin{bmatrix}
2x+y \
2x+y
\end{bmatrix}
=============

\begin{bmatrix}
0 \
0
\end{bmatrix}
$$

Therefore:

$$
2x+y=0
$$

Solve for $y$:

$$
y=-2x
$$

Choose:

$$
x=1
$$

Then:

$$
y=-2
$$

Therefore:

$$
\boxed{
v_2=
\begin{bmatrix}
1 \
-2
\end{bmatrix}
}
$$

---

# 12. ✅ Verifying the Eigenvectors

Always verify an eigenvector using:

$$
Av=\lambda v
$$

---

## 🔍 Check $\lambda=2$

We found:

$$
v_1=
\begin{bmatrix}
1 \
1
\end{bmatrix}
$$

Calculate:

$$
Av_1
====

\begin{bmatrix}
1 & 1 \
2 & 0
\end{bmatrix}
\begin{bmatrix}
1 \
1
\end{bmatrix}
=============

\begin{bmatrix}
2 \
2
\end{bmatrix}
$$

Now calculate:

$$
2v_1
====

2
\begin{bmatrix}
1 \
1
\end{bmatrix}
=============

\begin{bmatrix}
2 \
2
\end{bmatrix}
$$

Therefore:

$$
\boxed{Av_1=2v_1}
$$

✅ **Correct**

---

## 🔍 Check $\lambda=-1$

We found:

$$
v_2=
\begin{bmatrix}
1 \
-2
\end{bmatrix}
$$

Calculate:

$$
Av_2
====

\begin{bmatrix}
1 & 1 \
2 & 0
\end{bmatrix}
\begin{bmatrix}
1 \
-2
\end{bmatrix}
=============

\begin{bmatrix}
-1 \
2
\end{bmatrix}
$$

Now:

$$
-v_2
====

*

\begin{bmatrix}
1 \
-2
\end{bmatrix}
=============

\begin{bmatrix}
-1 \
2
\end{bmatrix}
$$

Therefore:

$$
\boxed{Av_2=-v_2}
$$

✅ **Correct**

---

# 13. ⟂ Orthogonal Eigenvectors

## 📐 Definition

Two vectors are **orthogonal** if their dot product is zero:

$$
v_1^Tv_2=0
$$

or equivalently:

$$
v_1\cdot v_2=0
$$

---

## 📌 Simple Example

Consider:

$$
u=
\begin{bmatrix}
1 \
1
\end{bmatrix}
$$

and:

$$
w=
\begin{bmatrix}
1 \
-1
\end{bmatrix}
$$

Their dot product is:

$$
u\cdot w
========

(1)(1)+(1)(-1)
$$

Therefore:

$$
u\cdot w=1-1=0
$$

So:

$$
\boxed{u\perp w}
$$

✅ The vectors are orthogonal.

---

## ⚠️ Are the Eigenvectors of Our Matrix Orthogonal?

Our eigenvectors are:

$$
v_1=
\begin{bmatrix}
1 \
1
\end{bmatrix}
$$

and:

$$
v_2=
\begin{bmatrix}
1 \
-2
\end{bmatrix}
$$

Calculate their dot product:

$$
v_1\cdot v_2
============

# (1)(1)+(1)(-2)

-1
$$

Since:

$$
-1\neq0
$$

the eigenvectors are **not orthogonal**.

❌ Therefore:

$$
v_1 \not\perp v_2
$$

> 💡 Eigenvectors associated with different eigenvalues are **not automatically orthogonal for every matrix**.

However, for a **real symmetric matrix**, eigenvectors corresponding to distinct eigenvalues are orthogonal.

This property is extremely important in **PCA**.

---

# 14. 📊 Eigenvectors and Symmetric Matrices

A symmetric matrix satisfies:

$$
A=A^T
$$

For example:

$$
A=
\begin{bmatrix}
2 & 1 \
1 & 2
\end{bmatrix}
$$

A real symmetric matrix has several important properties:

* ✅ Its eigenvalues are real
* ⟂ Eigenvectors corresponding to distinct eigenvalues are orthogonal
* 📏 Eigenvectors can be normalized
* 🧭 An orthonormal eigenvector basis can be constructed

This is especially important because **covariance and correlation matrices are symmetric**.

Therefore, these properties are fundamental to PCA.

---

# 15. 📏 Orthogonal vs. Orthonormal

### ⟂ Orthogonal

Two vectors are orthogonal if:

$$
v_i^Tv_j=0
$$

for:

$$
i\neq j
$$

### 📏 Normalized

A vector is normalized when:

$$
|v|=1
$$

### ⭐ Orthonormal

A set of vectors is **orthonormal** when the vectors are:

1. ⟂ Orthogonal to one another
2. 📏 Each normalized to unit length

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

$$
\boxed{Av=\lambda v}
$$

## 🔎 Characteristic Equation

$$
\boxed{\det(A-\lambda I)=0}
$$

## 🏹 Finding Eigenvectors

$$
\boxed{(A-\lambda I)v=0}
$$

## 📏 Vector Length

For:

$$
v=
\begin{bmatrix}
v_1 \
v_2 \
\vdots \
v_n
\end{bmatrix}
$$

the Euclidean norm is:

$$
\boxed{
|v|
===

\sqrt{v_1^2+v_2^2+\cdots+v_n^2}
}
$$

## 📐 Normalization

$$
\boxed{
\hat{v}
=======

\frac{v}{|v|}
}
$$

## ⟂ Orthogonality

$$
\boxed{
v_1^Tv_2=0
}
$$

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

PCA transforms them into principal components:

```text
PC1
PC2
PC3
PC4
```

These principal-component directions are determined from the **eigenvectors of the covariance or correlation matrix**.

---

## 🏹 Eigenvectors in PCA

Eigenvectors determine:

> 🧭 **The directions of the principal components**

For example:

```text
Eigenvector 1 → Direction of PC1
Eigenvector 2 → Direction of PC2
Eigenvector 3 → Direction of PC3
```

---

## 🔢 Eigenvalues in PCA

Eigenvalues indicate how much variance is associated with each principal component.

Usually:

$$
\lambda_1 \geq \lambda_2 \geq \lambda_3 \geq \cdots
$$

Therefore:

```text
Largest eigenvalue
        ↓
Largest amount of variance
        ↓
First principal component (PC1)
```

> 💡 In PCA, eigenvectors determine the **directions**, while eigenvalues quantify the **variance explained along those directions**.

---

# 19. 🧬 Why This Matters in Biology and Data Analysis

Eigenvalues and eigenvectors are widely used in:

* 🧬 Gene expression analysis
* 📊 Principal Component Analysis
* 🔬 Feature extraction
* 📉 Dimensionality reduction
* 🧫 Systems biology
* 🧩 Pattern recognition
* 💻 Machine learning

---

## 🧬 Gene Expression Example

Gene-expression datasets may contain:

```text
Thousands of genes
       ↓
Hundreds of samples
       ↓
High-dimensional dataset
```

PCA can transform these thousands of correlated variables into a smaller number of principal components.

```text
Original Variables
X₁ X₂ X₃ X₄ X₅ ... Xₙ
          ↓
         PCA
          ↓
      PC1 PC2 PC3 ...
```

This can help:

* 📉 Reduce dimensionality
* 🔍 Reveal biological patterns
* 🧩 Identify sample clusters
* ⚠️ Detect unusual samples
* 📊 Visualize complex datasets
* 💻 Reduce computational complexity

---

# 20. 🧒 Eigenvectors Explained Like You're Five

Imagine you have a machine and many arrows.

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

| Concept                        | 💡 Meaning                                              |
| ------------------------------ | ------------------------------------------------------- |
| 🏹 **Vector**                  | Has magnitude and direction                             |
| ⭐ **Eigenvector**              | Direction preserved under a matrix transformation       |
| 🔢 **Eigenvalue**              | Scaling factor associated with an eigenvector           |
| 📏 **Normalized eigenvector**  | Eigenvector with length 1                               |
| ⟂ **Orthogonal vectors**       | Vectors whose dot product is zero                       |
| ⭐ **Orthonormal vectors**      | Orthogonal unit vectors                                 |
| 🧮 **Characteristic equation** | $\det(A-\lambda I)=0$                                   |
| 📊 **PCA eigenvectors**        | Determine principal-component directions                |
| 📈 **PCA eigenvalues**         | Determine variance associated with principal components |

---

# 22. 🎯 Final Summary

The fundamental eigenvector equation is:

$$
\boxed{Av=\lambda v}
$$

To calculate the eigenvalues:

$$
\boxed{\det(A-\lambda I)=0}
$$

To find an eigenvector corresponding to an eigenvalue:

$$
\boxed{(A-\lambda I)v=0}
$$

To normalize an eigenvector:

$$
\boxed{\hat{v}=\frac{v}{|v|}}
$$

To check orthogonality:

$$
\boxed{v_1^Tv_2=0}
$$

### 🚀 The Big Picture

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
> **Eigenvectors identify special directions preserved by a matrix transformation. Eigenvalues describe how strongly those directions are scaled. In PCA, eigenvectors define the principal-component directions, while eigenvalues quantify the variance associated with those components.**
