# 🧭 Eigenvectors and Eigenvalues 

Eigenvectors and eigenvalues are fundamental concepts in **linear algebra** and are especially important in **multivariate statistics**, **PCA**, **machine learning**, and **data analysis**.

---

# 1. ⭐ What Is an Eigenvector?

## 🔍 Core Idea

An **eigenvector** is a special vector whose **direction is preserved** when a matrix acts on it.

When a matrix transforms an eigenvector, the matrix may:

* 📏 Stretch it
* 🤏 Shrink it
* 🔄 Flip its direction

But the resulting vector remains on the **same line** as the original vector.

> 💡 **Simple idea:** An eigenvector is a direction that is preserved by a matrix transformation.

---

## 📐 Mathematical Definition

A non-zero vector **v** is an eigenvector of a square matrix **A** if:

$$
Av = \lambda v
$$

where:

* 🔢 **A** = square matrix
* 🏹 **v** = eigenvector
* ⭐ **λ (lambda)** = eigenvalue

The vector must satisfy:

$$
v \neq 0
$$

because the zero vector is **not considered an eigenvector**.

---

## 🏭 Simple Intuition: Matrix as a Machine

Imagine a matrix as a **transformation machine**.

```text
                 MATRIX A
Vector v  ─────► [ MACHINE ] ─────► New Vector
```

For most vectors:

```text
Direction before ≠ Direction after
```

But for an eigenvector:

```text
Direction before = Same line after
```

Only its **size or orientation along that line** may change.

### 🧒 Easy Analogy

* 🏭 **Matrix:** "I'm a machine that transforms arrows."
* 🏹 **Vector:** "I'm an arrow."
* ⭐ **Eigenvector:** "I'm a special arrow. You can stretch, shrink, or flip me, but I stay on my special line."
* 🔢 **Eigenvalue:** "I'm the number that tells you how much that special arrow changes."

---

# 2. 🏹 Vectors – Quick Revision

A **vector** is an ordered collection of numbers.

For example:

$$
v =
\begin{bmatrix}
2\
3
\end{bmatrix}
$$

This is a two-dimensional vector.

A vector has two important properties:

* 📏 **Magnitude** = its length
* 🧭 **Direction** = where it points

For eigenvectors, the important feature is primarily the **direction**.

> 💡 Multiplying an eigenvector by a non-zero constant changes its length, but it still represents the same eigendirection.

---

# 3. ✖️ Scaling a Vector

A vector can be multiplied by a scalar.

Suppose:

$$
v =
\begin{bmatrix}
1\
2
\end{bmatrix}
$$

Multiply it by 2:

$$
2v =
\begin{bmatrix}
2\
4
\end{bmatrix}
$$

The vector becomes longer, but its direction remains the same.

```text
v   = (1, 2)

2v  = (2, 4)

3v  = (3, 6)
```

All these vectors lie along the **same line**.

> 📌 **Important:** Scaling changes the magnitude of a vector, but multiplication by a positive scalar does not change its direction. Multiplication by a negative scalar reverses its orientation while keeping it on the same line.

This idea is the foundation of the eigenvector equation.

---

# 4. 🧮 Eigenvector Equation Explained

The fundamental equation is:

$$
Av = \lambda v
$$

Let's break it down.

### Left Side

$$
Av
$$

means:

> Apply the matrix transformation **A** to vector **v**.

### Right Side

$$
\lambda v
$$

means:

> Multiply vector **v** by the scalar **λ**.

Therefore:

$$
Av = \lambda v
$$

means that applying the matrix produces exactly the same result as simply **scaling the vector**.

---

## 🧠 Interpretation

If:

$$
Av = 2v
$$

then the matrix doubles the eigenvector.

If:

$$
Av = 0.5v
$$

then the matrix shrinks the eigenvector to half its size.

If:

$$
Av = -v
$$

then the vector is flipped to the opposite direction along the same line.

---

# 5. 🧩 Example Matrix

Consider the matrix:

$$
A =
\begin{bmatrix}
1 & 1\
2 & 0
\end{bmatrix}
$$

We will use this example to understand how to:

1. 🧪 Test vectors
2. 🔢 Find eigenvalues
3. 🏹 Find eigenvectors
4. 📏 Normalize eigenvectors
5. ⟂ Check orthogonality

> 📌 The exact calculations below demonstrate the general procedure used for eigenvalue and eigenvector problems.

---

# 6. 🧪 Testing Whether a Vector Is an Eigenvector

To determine whether a vector **v** is an eigenvector of **A**, calculate:

$$
Av
$$

Then ask:

> ❓ Is the resulting vector a scalar multiple of the original vector?

---

## ❌ Example: Not an Eigenvector

Consider:

$$
v =
\begin{bmatrix}
2\
2
\end{bmatrix}
$$

Using:

$$
A =
\begin{bmatrix}
1 & 1\
2 & 0
\end{bmatrix}
$$

calculate:

$$
Av =
\begin{bmatrix}
1 & 1\
2 & 0
\end{bmatrix}
\begin{bmatrix}
2\
2
\end{bmatrix}
$$

Therefore:

$$
Av =
\begin{bmatrix}
4\
4
\end{bmatrix}
$$

Notice:

$$
Av = 2v
$$

So for this particular matrix, **v actually is an eigenvector**.

Its eigenvalue is:

$$
\lambda = 2
$$

---

## ❌ Example of a True Non-Eigenvector

Instead consider:

$$
v =
\begin{bmatrix}
1\
0
\end{bmatrix}
$$

Then:

$$
Av =
\begin{bmatrix}
1\
2
\end{bmatrix}
$$

There is no scalar **λ** such that:

$$
\begin{bmatrix}
1\
2
\end{bmatrix}
=============

\lambda
\begin{bmatrix}
1\
0
\end{bmatrix}
$$

Therefore:

❌ Direction changed
❌ Result is not a scalar multiple of the original vector
➡️ **Not an eigenvector**

---

# 7. 🔢 What Is an Eigenvalue?

An **eigenvalue** tells us how much the corresponding eigenvector is scaled by the matrix transformation.

If:

$$
Av = \lambda v
$$

then **λ** is the eigenvalue.

---

## 📌 Example

Suppose:

$$
Av = 2v
$$

Then:

$$
\lambda = 2
$$

Meaning:

➡️ The eigenvector becomes **twice as large**.

---

## 🔍 Interpreting Eigenvalues

|        Eigenvalue | Effect                                    |
| ----------------: | ----------------------------------------- |
|     $\lambda > 1$ | 📈 Vector stretches                       |
| $0 < \lambda < 1$ | 📉 Vector shrinks                         |
|     $\lambda = 1$ | ➡️ Vector unchanged                       |
|     $\lambda = 0$ | 🔴 Vector collapses to zero               |
|     $\lambda < 0$ | 🔄 Vector flips orientation and is scaled |

> 💡 The **magnitude** $|\lambda|$ describes the scaling, while the sign tells us whether the orientation along the eigenvector line is reversed.

---

# 8. ♾️ Many Eigenvectors for One Eigenvalue

Suppose **v** is an eigenvector:

$$
Av = \lambda v
$$

Multiply **v** by any non-zero scalar **c**.

Then:

$$
A(cv)
$$

Using linearity:

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

or:

$$
A(cv) = \lambda(cv)
$$

Therefore:

$$
\boxed{cv \text{ is also an eigenvector}}
$$

---

## 📌 Example

If:

$$
v =
\begin{bmatrix}
1\
1
\end{bmatrix}
$$

is an eigenvector, then all of these are also eigenvectors:

$$
\begin{bmatrix}
2\
2
\end{bmatrix},
\quad
\begin{bmatrix}
3\
3
\end{bmatrix},
\quad
\begin{bmatrix}
-1\
-1
\end{bmatrix}
$$

They all represent the same **eigendirection**.

> ⭐ An eigenvalue therefore usually corresponds to infinitely many scalar multiples of an eigenvector.

---

# 9. 📏 Unit-Length / Normalized Eigenvectors

Because eigenvectors can have different lengths, we often convert them to **unit vectors**.

A unit vector has:

$$
|v| = 1
$$

This process is called **normalization**.

---

## 🧮 Step 1: Calculate Vector Length

For:

$$
v =
\begin{bmatrix}
a\
b
\end{bmatrix}
$$

the Euclidean length is:

$$
|v| = \sqrt{a^2+b^2}
$$

---

## 🧮 Step 2: Divide by the Length

The normalized vector is:

$$
\hat{v} = \frac{v}{|v|}
$$

---

## 📌 Example

Suppose:

$$
v =
\begin{bmatrix}
1\
1
\end{bmatrix}
$$

Its length is:

$$
|v| = \sqrt{1^2+1^2}
$$

$$
= \sqrt{2}
$$

Therefore:

$$
\hat{v}
=======

\frac{1}{\sqrt{2}}
\begin{bmatrix}
1\
1
\end{bmatrix}
$$

or:

$$
\hat{v}
=======

\begin{bmatrix}
1/\sqrt{2}\
1/\sqrt{2}
\end{bmatrix}
$$

Approximately:

$$
\hat{v}
=======

\begin{bmatrix}
0.707\
0.707
\end{bmatrix}
$$

---

## 🎯 Why Normalize Eigenvectors?

Normalization is useful for:

* 📊 PCA
* 📈 Multivariate analysis
* 🧭 Comparing directions
* 💻 Numerical computation
* 🔄 Coordinate transformations

---

# 10. 🔎 Finding Eigenvalues – Core Procedure

This is one of the most important procedures to remember.

We start with:

$$
Av = \lambda v
$$

---

## Step 1️⃣: Rearrange the Equation

Move everything to one side:

$$
Av-\lambda v=0
$$

Since:

$$
v = Iv
$$

we can write:

$$
Av-\lambda Iv=0
$$

Factor out **v**:

$$
(A-\lambda I)v=0
$$

where **I** is the identity matrix.

---

## Step 2️⃣: Set the Determinant Equal to Zero

For a **non-zero solution** for $v$ to exist:

$$
\boxed{\det(A-\lambda I)=0}
$$

This is called the **characteristic equation**.

> 🧠 **Very important formula:**
> To find eigenvalues, calculate $\det(A-\lambda I)$ and set it equal to zero.

---

## Step 3️⃣: Apply It to Our Example

Recall:

$$
A =
\begin{bmatrix}
1 & 1\
2 & 0
\end{bmatrix}
$$

Then:

$$
A-\lambda I
===========

\begin{bmatrix}
1-\lambda & 1\
2 & -\lambda
\end{bmatrix}
$$

Calculate the determinant:

$$
\det(A-\lambda I)
=================

(1-\lambda)(-\lambda)-(1)(2)
$$

Therefore:

$$
-\lambda+\lambda^2-2=0
$$

Rearrange:

$$
\lambda^2-\lambda-2=0
$$

---

## Step 4️⃣: Solve the Polynomial

Factor:

$$
\lambda^2-\lambda-2=0
$$

$$
(\lambda-2)(\lambda+1)=0
$$

Therefore:

$$
\boxed{\lambda_1=2}
$$

and:

$$
\boxed{\lambda_2=-1}
$$

These are the **eigenvalues** of matrix **A**.

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

> 🖼️ **Figure:** Add characteristic polynomial graph from **PDF page 6**.

---

# 11. 🏹 Finding Eigenvectors for Each Eigenvalue

Once the eigenvalues are known, substitute each value into:

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
-1 & 1\
2 & -2
\end{bmatrix}
$$

Let:

$$
v =
\begin{bmatrix}
x\
y
\end{bmatrix}
$$

Then:

$$
\begin{bmatrix}
-1 & 1\
2 & -2
\end{bmatrix}
\begin{bmatrix}
x\
y
\end{bmatrix}
=============

\begin{bmatrix}
0\
0
\end{bmatrix}
$$

The first equation gives:

$$
-x+y=0
$$

Therefore:

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
1\
1
\end{bmatrix}
}
$$

---

## ⭐ Eigenvector for $\lambda=-1$

Now substitute:

$$
\lambda=-1
$$

Then:

$$
A+I
===

\begin{bmatrix}
2 & 1\
2 & 1
\end{bmatrix}
$$

Solve:

$$
2x+y=0
$$

Therefore:

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
1\
-2
\end{bmatrix}
}
$$

---

# 12. ✅ Verifying Eigenvectors

Always verify your answer using:

$$
Av=\lambda v
$$

---

## 🔍 Check $\lambda=2$

Eigenvector:

$$
v_1=
\begin{bmatrix}
1\
1
\end{bmatrix}
$$

Calculate:

$$
Av_1
====

\begin{bmatrix}
1 & 1\
2 & 0
\end{bmatrix}
\begin{bmatrix}
1\
1
\end{bmatrix}
$$

# $$

\begin{bmatrix}
2\
2
\end{bmatrix}
$$

Meanwhile:

$$
2v_1
====

2
\begin{bmatrix}
1\
1
\end{bmatrix}
=============

\begin{bmatrix}
2\
2
\end{bmatrix}
$$

Therefore:

$$
Av_1=2v_1
$$

✅ **Correct**

---

## 🔍 Check $\lambda=-1$

Eigenvector:

$$
v_2=
\begin{bmatrix}
1\
-2
\end{bmatrix}
$$

Calculate:

$$
Av_2
====

\begin{bmatrix}
1 & 1\
2 & 0
\end{bmatrix}
\begin{bmatrix}
1\
-2
\end{bmatrix}
$$

# $$

\begin{bmatrix}
-1\
2
\end{bmatrix}
$$

Meanwhile:

$$
-v_2
====

\begin{bmatrix}
-1\
2
\end{bmatrix}
$$

Therefore:

$$
Av_2=-v_2
$$

✅ **Correct**

---

# 13. ⟂ Orthogonal Eigenvectors

## 📐 Definition

Two vectors are **orthogonal** when they meet at a **90° angle**.

Mathematically, their dot product must equal zero:

$$
v_1^Tv_2=0
$$

or:

$$
v_1\cdot v_2=0
$$

---

## 📌 Example

Consider:

$$
v_1=
\begin{bmatrix}
1\
1
\end{bmatrix}
$$

and:

$$
v_2=
\begin{bmatrix}
1\
-1
\end{bmatrix}
$$

Calculate their dot product:

$$
v_1\cdot v_2
============

(1)(1)+(1)(-1)
$$

$$
=1-1
$$

$$
=0
$$

Therefore:

$$
\boxed{v_1\perp v_2}
$$

✅ The vectors are **orthogonal**.

---

## ⚠️ Important Note About Our Example Matrix

For our example matrix:

$$
A =
\begin{bmatrix}
1 & 1\
2 & 0
\end{bmatrix}
$$

the eigenvectors were:

$$
v_1=
\begin{bmatrix}
1\
1
\end{bmatrix},
\qquad
v_2=
\begin{bmatrix}
1\
-2
\end{bmatrix}
$$

Their dot product is:

$$
(1)(1)+(1)(-2)=-1
$$

Therefore:

❌ These particular eigenvectors are **not orthogonal**.

> 💡 Eigenvectors corresponding to different eigenvalues are **not automatically orthogonal for every matrix**.

A particularly important result is:

> ⭐ For a **real symmetric matrix**, eigenvectors corresponding to distinct eigenvalues can be chosen to be orthogonal.

This property is extremely important in **PCA**.

---

# 14. 📊 Eigenvectors and Symmetric Matrices

A symmetric matrix satisfies:

$$
A=A^T
$$

Example:

$$
A=
\begin{bmatrix}
2 & 1\
1 & 2
\end{bmatrix}
$$

Notice that the matrix is mirrored across its main diagonal.

Symmetric matrices have several useful properties:

* ✅ Eigenvalues are real
* ⟂ Eigenvectors associated with distinct eigenvalues are orthogonal
* 📏 Eigenvectors can be normalized
* 🧭 An orthonormal eigenvector basis can be constructed

This matters because **covariance matrices and correlation matrices are symmetric**.

Therefore, PCA benefits directly from these properties.

---

# 15. 📏 Orthogonal vs. Orthonormal

These terms are related but not identical.

### ⟂ Orthogonal

Vectors are orthogonal when:

$$
v_i^Tv_j=0
$$

for different vectors.

### 📏 Normalized

A vector is normalized when:

$$
|v|=1
$$

### ⭐ Orthonormal

Vectors are **orthonormal** when they are:

1. ⟂ Orthogonal to each other
2. 📏 Each has unit length

So:

```text
Orthogonal
     +
Normalized
     ↓
Orthonormal
```

This is particularly important in **PCA**.

---

# 16. 🧠 Complete Eigenvalue/Eigenvector Workflow

When given a matrix **A**, follow this procedure:

```text
                    MATRIX A
                       ↓
              Write Av = λv
                       ↓
              (A - λI)v = 0
                       ↓
             det(A - λI) = 0
                       ↓
          Characteristic equation
                       ↓
              Solve for λ
                       ↓
                 Eigenvalues
                       ↓
        Substitute each λ separately
                       ↓
              (A - λI)v = 0
                       ↓
             Solve for vector v
                       ↓
                 Eigenvectors
                       ↓
             Normalize if needed
                       ↓
             Verify Av = λv
                       ↓
        Check orthogonality if relevant
```

> 🎯 **Exam tip:** Remember the sequence:
> **Determinant → Eigenvalues → Eigenvectors → Normalize → Verify**

---

# 17. 📋 Key Formulas

## ⭐ Eigenvector Equation

$$
\boxed{Av=\lambda v}
$$

---

## 🔎 Characteristic Equation

$$
\boxed{\det(A-\lambda I)=0}
$$

---

## 🏹 Finding Eigenvectors

$$
\boxed{(A-\lambda I)v=0}
$$

---

## 📏 Vector Length

For:

$$
v=
\begin{bmatrix}
v_1\
v_2\
\vdots\
v_n
\end{bmatrix}
$$

the length is:

$$
\boxed{
|v|=
\sqrt{
v_1^2+v_2^2+\cdots+v_n^2
}
}
$$

---

## 📐 Normalization

$$
\boxed{
\hat{v}=\frac{v}{|v|}
}
$$

---

## ⟂ Orthogonality

$$
\boxed{
v_1^Tv_2=0
}
$$

---

# 18. 📊 Why Eigenvectors Matter in PCA

Eigenvalues and eigenvectors are the mathematical foundation of **Principal Component Analysis (PCA)**.

PCA attempts to find new directions that explain the variation in a multivariate dataset.

Suppose our original variables are:

```text
X₁
X₂
X₃
X₄
```

PCA creates new directions:

```text
PC1
PC2
PC3
PC4
```

These directions are determined from **eigenvectors** of a covariance or correlation matrix.

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

Eigenvalues tell us:

> 📊 **How much variance is captured along each principal-component direction**

Typically:

$$
\lambda_1 \geq \lambda_2 \geq \lambda_3 \geq \cdots
$$

The largest eigenvalue corresponds to the direction containing the greatest variance.

Therefore:

```text
Largest eigenvalue
        ↓
Most variance explained
        ↓
Most important principal component
```

---

# 19. 🧬 Why This Matters in Biology and Data Analysis

Eigenvectors and eigenvalues are widely used in biological and biomedical data analysis.

### 🧬 Gene Expression Analysis

Gene-expression datasets can contain:

```text
Thousands of genes
        ↓
Hundreds of samples
        ↓
Very high-dimensional data
```

PCA uses eigenvectors to identify major patterns in these data.

---

## 🔬 Feature Extraction

Eigenvector-based methods can transform many correlated variables into a smaller number of informative features.

```text
Original variables
X₁ X₂ X₃ X₄ X₅ ... Xₙ
          ↓
         PCA
          ↓
       PC1 PC2 PC3
```

---

## 📉 Dimensionality Reduction

Instead of analyzing hundreds or thousands of variables, we may retain only the most informative principal components.

This can:

* 📉 Reduce dimensionality
* 🔍 Reveal hidden patterns
* 🧩 Identify clusters
* ⚠️ Detect unusual samples
* 💻 Reduce computational complexity
* 📊 Improve visualization

---

## 🧫 Systems Biology

Eigenvalues and eigenvectors can also appear in:

* 🧬 Gene regulatory network analysis
* 🦠 Population models
* 💊 Pharmacological modeling
* 🧪 Dynamic biological systems
* 📈 Stability analysis

---

# 20. 🧒 Eigenvectors Explained Like You're Five

Imagine you have a machine and lots of arrows.

🏭 **Matrix**

> "I'm a machine that transforms arrows."

🏹 **Vector**

> "I'm an arrow. I have a length and a direction."

⭐ **Eigenvector**

> "I'm a special arrow. When I enter the machine, I stay on the same special line."

🔢 **Eigenvalue**

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

Before:  ↗
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

| Concept                        | 💡 Meaning                                             |
| ------------------------------ | ------------------------------------------------------ |
| 🏹 **Vector**                  | Has magnitude and direction                            |
| ⭐ **Eigenvector**              | Special direction preserved by a matrix transformation |
| 🔢 **Eigenvalue**              | Scaling factor associated with an eigenvector          |
| 📏 **Normalized eigenvector**  | Eigenvector with length 1                              |
| ⟂ **Orthogonal vectors**       | Vectors with dot product 0                             |
| ⭐ **Orthonormal vectors**      | Orthogonal vectors that also have unit length          |
| 🧮 **Characteristic equation** | Equation used to calculate eigenvalues                 |
| 📊 **PCA eigenvectors**        | Determine principal-component directions               |
| 📈 **PCA eigenvalues**         | Measure variance captured by principal components      |

---

# 22. 🎯 Final Summary

The fundamental equation is:

$$
\boxed{Av=\lambda v}
$$

It tells us that when matrix **A** acts on an eigenvector **v**, the resulting vector remains on the **same line** and is scaled by the eigenvalue **λ**.

To calculate eigenvalues:

$$
\boxed{\det(A-\lambda I)=0}
$$

To calculate an eigenvector for a known eigenvalue:

$$
\boxed{(A-\lambda I)v=0}
$$

To normalize an eigenvector:

$$
\boxed{\hat{v}=\frac{v}{|v|}}
$$

To test whether two vectors are orthogonal:

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
> **Eigenvectors tell us the important directions. Eigenvalues tell us how important or strongly scaled those directions are. Together, they form the mathematical backbone of PCA and many multivariate statistical methods.**
