# 🧮 MATRICES 

> **Core idea:** A matrix is more than a table of numbers. It can also
> represent **data**, **instructions**, and **transformations**.

------------------------------------------------------------------------

## 📚 Table of Contents

1.  [What is a Matrix?](#1-what-is-a-matrix)
2.  [Matrix Dimensions](#2-matrix-dimensions-size)
3.  [Matrix Elements](#3-matrix-elements)
4.  [Vectors](#4-vectors)
5.  [Special Types of Matrices](#5-special-types-of-matrices)
6.  [Transpose of a Matrix](#6-transpose-of-a-matrix)
7.  [Symmetric Matrix](#7-symmetric-matrix)
8.  [Matrix Addition](#8-matrix-addition)
9.  [Matrix Subtraction](#9-matrix-subtraction)
10. [Scalar Multiplication](#10-scalar-multiplication)
11. [Matrix Multiplication](#11-matrix-multiplication)
12. [Identity Matrix in
    Multiplication](#12-identity-matrix-in-multiplication)
13. [Determinant of a Matrix](#13-determinant-of-a-matrix)
14. [Inverse of a Matrix](#14-inverse-of-a-matrix)
15. [Solving Linear Equations Using
    Matrices](#15-solving-linear-equations-using-matrices)
16. [Key Takeaways](#16-key-takeaways)
17. [The Deeper Idea](#17-the-deeper-idea)
18. [One Sentence to Remember](#18-one-sentence-to-remember)

------------------------------------------------------------------------

# 1. 🧩 What is a Matrix?

## Definition

A **matrix** is a rectangular arrangement of numbers organized into:

-   ➡️ **Rows** --- horizontal
-   ⬇️ **Columns** --- vertical

Example:

``` text
A = [ 10   20   30
      40   50   60 ]
```

Or mathematically:

$$
A =
\begin{bmatrix}
10 & 20 & 30 \\
40 & 50 & 60
\end{bmatrix}
$$

This matrix has:

-   **2 rows**
-   **3 columns**

Therefore, it is a **2 × 3 matrix**.

------------------------------------------------------------------------

## 🌍 Why Matrices Are Important

Matrices are used to:

-   🗃️ Store large amounts of related data
-   🔄 Perform mathematical transformations
-   🧮 Solve systems of equations
-   📊 Perform multivariate analysis
-   🤖 Represent datasets in statistics and machine learning
-   🧬 Store biological and biomedical measurements

### 🧬 Biology examples

A matrix can represent:

-   Gene expression data
-   Patient measurements
-   Sequencing data
-   Protein abundance
-   Metabolomics data
-   Clinical measurements

For example:

 | Patient | CRP | Weight | Age |
|:-------:|----:|-------:|----:|
| 1 | 40 | 107 | 40 |
| 2 | 30 | 104 | 32 |
| 3 | 35 | 66 | 55 |

The numerical part can be represented as:

$$
X =
\begin{bmatrix}
40 & 107 & 40 \\
30 & 104 & 32 \\
35 & 66 & 55
\end{bmatrix}
$$

Here:

-   Each **row** represents a patient.
-   Each **column** represents a variable.

------------------------------------------------------------------------

# 2. 📐 Matrix Dimensions (Size)

The dimension of a matrix is written as:

$$
\text{rows} \times \text{columns}
$$

Examples:

-   A **2 × 3** matrix has 2 rows and 3 columns.
-   A **3 × 2** matrix has 3 rows and 2 columns.
-   A **3 × 3** matrix is a square matrix.

Example:

$$
A =
\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6
\end{bmatrix}
$$

Therefore:

$$
A \in \mathbb{R}^{2 \times 3}
$$

📌 **Always count rows first, then columns.**

> **Rows × Columns**

------------------------------------------------------------------------

# 3. 🔢 Matrix Elements

Each value inside a matrix is called an **element** or **entry**.

The element in row `i` and column `j` is written as:

$$
a_{ij}
$$

Where:

-   `i` = row number
-   `j` = column number

Example:

$$
A =
\begin{bmatrix}
10 & 80 & 120 \\
15 & 90 & 150 \\
20 & 179 & 200
\end{bmatrix}
$$

Then:

``` text
A₁,₃ = 120
A₃,₂ = 179
```

Because:

-   `A₁,₃` means **row 1, column 3**
-   `A₃,₂` means **row 3, column 2**

------------------------------------------------------------------------

# 4. 🏹 Vectors

## Definition

A **vector** is a special matrix that has only:

-   one column, or
-   one row.

### Column vector

$$
\mathbf{x} =
\begin{bmatrix}
10 \\
20 \\
30
\end{bmatrix}
$$

Dimension:

$$
3 \times 1
$$

### Row vector

$$
\mathbf{x} =
\begin{bmatrix}
10 & 20 & 30
\end{bmatrix}
$$

Dimension:

$$
1 \times 3
$$

### 📌 Vectors can represent

-   🧑 Patient measurements
-   🧬 Gene expression values
-   🤖 Feature values in machine learning
-   📍 Position in space
-   🏹 Direction and magnitude

For example, one patient's measurements might be:

$$
\mathbf{x} =
\begin{bmatrix}
40 \\
107 \\
40
\end{bmatrix}
$$

representing:

``` text
CRP    = 40
Weight = 107
Age    = 40
```

------------------------------------------------------------------------

# 5. 🧱 Special Types of Matrices

## 5.1 ◼️ Square Matrix

A **square matrix** has the same number of rows and columns.

Example:

$$
A =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
$$

This is a:

$$
2 \times 2
$$

square matrix.

Another example:

$$
B =
\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{bmatrix}
$$

This is a **3 × 3 square matrix**.

------------------------------------------------------------------------

## 5.2 0️⃣ Zero Matrix

A **zero matrix** contains only zeros.

Example:

$$
O =
\begin{bmatrix}
0 & 0 \\
0 & 0
\end{bmatrix}
$$

------------------------------------------------------------------------

## 5.3 🪞 Identity Matrix

The **identity matrix** is a special square matrix where:

- diagonal elements = `1`
- all other elements = `0`

Example:

```math
I_3 =
\begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
```

📌 The identity matrix behaves like the number **1** in ordinary multiplication.

For a matrix `A`:

```math
AI = IA = A
```

------------------------------------------------------------------------

# 6. 🔄 Transpose of a Matrix

## Definition

The **transpose** of a matrix is obtained by converting:

> **rows into columns**

The transpose of matrix `A` is written:

$$
A^T
$$

Example:

$$
A =
\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6
\end{bmatrix}
$$

Then:

$$
A^T =
\begin{bmatrix}
1 & 4 \\
2 & 5 \\
3 & 6
\end{bmatrix}
$$

Notice:

``` text
A     = 2 × 3
Aᵀ    = 3 × 2
```

------------------------------------------------------------------------

## 🧬 Real-World Example: Patient Data

Original table:

| Patient | CRP | Weight | Age |
|:-------:|----:|-------:|----:|
| 1 | 40 | 107 | 40 |
| 2 | 30 | 104 | 32 |
| 3 | 35 | 66 | 55 |
| 4 | 100 | 77 | 66 |
| 5 | 125 | 70 | 87 |

Numerical matrix:

$$
X =
\begin{bmatrix}
40 & 107 & 40 \\
30 & 104 & 32 \\
35 & 66 & 55 \\
100 & 77 & 66 \\
125 & 70 & 87
\end{bmatrix}
$$

Here:

> **Rows = patients**
> **Columns = variables**

After transposing:

$$
X^T =
\begin{bmatrix}
40 & 30 & 35 & 100 & 125 \\
107 & 104 & 66 & 77 & 70 \\
40 & 32 & 55 & 66 & 87
\end{bmatrix}
$$

Now:

> **Rows = variables**\
> **Columns = patients**

------------------------------------------------------------------------

# 7. 🪞 Symmetric Matrix

## Definition

A matrix is **symmetric** if:

$$
A = A^T
$$

Example:

$$
A =
\begin{bmatrix}
1 & 2 & 3 \\
2 & 5 & 4 \\
3 & 4 & 6
\end{bmatrix}
$$

Its transpose is identical:

$$
A^T =
\begin{bmatrix}
1 & 2 & 3 \\
2 & 5 & 4 \\
3 & 4 & 6
\end{bmatrix}
$$

Therefore:

$$
A = A^T
$$

✅ The matrix is symmetric.

📌 Covariance and correlation matrices in statistics are important
examples of symmetric matrices.

------------------------------------------------------------------------

# 8. ➕ Matrix Addition

## Rule

Two matrices can be added **only if they have the same dimensions**.

Example:

$$
A =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
$$

and

$$
B =
\begin{bmatrix}
5 & 6 \\
7 & 8
\end{bmatrix}
$$

Then:

$$
A+B =
\begin{bmatrix}
1+5 & 2+6 \\
3+7 & 4+8
\end{bmatrix}
$$

Therefore:

$$
A+B =
\begin{bmatrix}
6 & 8 \\
10 & 12
\end{bmatrix}
$$

📌 Add elements **position by position**.

------------------------------------------------------------------------

# 9. ➖ Matrix Subtraction

Matrix subtraction follows the same dimension rule as addition.

$$
A-B
$$

is possible only when `A` and `B` have the same dimensions.

Example:

```math
\begin{bmatrix}
5 & 8 \\
10 & 12
\end{bmatrix}
-
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
=
\begin{bmatrix}
4 & 6 \\
7 & 8
\end{bmatrix}
```

------------------------------------------------------------------------

# 10. ✖️ Scalar Multiplication

A **scalar** is simply a single number.

Scalar multiplication means multiplying **every element** of the matrix
by that number.

Example:

$$
A =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
$$

Multiply by `3`:

$$
3A =
3
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
$$

Therefore:

$$
3A =
\begin{bmatrix}
3 & 6 \\
9 & 12
\end{bmatrix}
$$

------------------------------------------------------------------------

# 11. ⚙️ Matrix Multiplication

## 🚨 Key Rule

Matrix multiplication is **not normally element-wise**.

Suppose:

$$
A_{m \times n}
$$

and:

$$
B_{n \times p}
$$

Then:

$$
AB
$$

is possible because the **inside dimensions match**:

``` text
(m × n)(n × p)
     ↑  ↑
     must match
```

The result has dimension:

$$
m \times p
$$

### Easy memory trick 🧠

``` text
(2 × 3)(3 × 4) → (2 × 4)
       ✅
```

The inner `3`s match.

------------------------------------------------------------------------

## 🏹 Matrix × Vector Example

Let:

```math
A =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
```

and:

```math
\mathbf{x} =
\begin{bmatrix}
5 \\
6
\end{bmatrix}
```

Then:

```math
A\mathbf{x}
=
\begin{bmatrix}
1(5)+2(6) \\
3(5)+4(6)
\end{bmatrix}
```

Therefore:

```math
A\mathbf{x}
=
\begin{bmatrix}
17 \\
39
\end{bmatrix}
```

### 🧠 Interpretation

Each row tells us **how to combine the inputs**.

``` text
First output  = 1×5 + 2×6 = 17
Second output = 3×5 + 4×6 = 39
```

Think:

> ⚙️ **Matrix × input vector = output vector**

------------------------------------------------------------------------

## 🔢 Matrix × Matrix Example

Let:

$$
A =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
$$

and:

$$
B =
\begin{bmatrix}
5 & 6 \\
7 & 8
\end{bmatrix}
$$

Then:

$$
AB =
\begin{bmatrix}
1(5)+2(7) & 1(6)+2(8) \\
3(5)+4(7) & 3(6)+4(8)
\end{bmatrix}
$$

Therefore:

$$
AB =
\begin{bmatrix}
19 & 22 \\
43 & 50
\end{bmatrix}
$$

------------------------------------------------------------------------

## 🚫 Matrix Multiplication Is Not Commutative

In ordinary arithmetic:

$$
2 \times 3 = 3 \times 2
$$

But matrices generally do **not** satisfy:

$$
AB = BA
$$

Usually:

$$
AB \neq BA
$$

Sometimes `BA` may not even be dimensionally possible.

------------------------------------------------------------------------

# 12. 🪞 Identity Matrix in Multiplication

The identity matrix does not change the matrix or vector it multiplies.

For example:

$$
I =
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
$$

and:

$$
\mathbf{x} =
\begin{bmatrix}
5 \\
8
\end{bmatrix}
$$

Then:

$$
I\mathbf{x}
=
\begin{bmatrix}
5 \\
8
\end{bmatrix}
$$

Therefore:

$$
I\mathbf{x}=\mathbf{x}
$$

Similarly:

$$
AI = IA = A
$$

📌 **Identity matrix = matrix version of the number 1.**

------------------------------------------------------------------------

# 13. 📏 Determinant of a Matrix

The **determinant** is a single number calculated from a square matrix.

It gives important information about the transformation represented by
the matrix.

The determinant is written:

$$
\det(A)
$$

or:

$$
|A|
$$

------------------------------------------------------------------------

## 13.1 Determinant of a 2 × 2 Matrix

For:

$$
A =
\begin{bmatrix}
a & b \\
c & d
\end{bmatrix}
$$

the determinant is:

$$
\det(A)=ad-bc
$$

Example:

$$
A =
\begin{bmatrix}
3 & 2 \\
1 & 4
\end{bmatrix}
$$

Then:

$$
\det(A)=(3)(4)-(2)(1)
$$

$$
\det(A)=12-2=10
$$

------------------------------------------------------------------------

## 13.2 Determinant of a 3 × 3 Matrix

For:

```math
A =
\begin{bmatrix}
a & b & c \\
d & e & f \\
g & h & i
\end{bmatrix}
```

one expansion is:

```math
\det(A)
=
a(ei-fh)
-
b(di-fg)
+
c(dh-eg)
```

📌 Determinants become especially important when studying:

-   matrix inverses
-   systems of equations
-   linear independence
-   eigenvalues
-   transformations

------------------------------------------------------------------------

## 🧠 Geometric Meaning of the Determinant

The determinant tells us how much a matrix scales **area** or
**volume**.

For example:

-   `det(A) = 2` → area becomes 2× larger
-   `det(A) = 0.5` → area becomes half as large
-   `det(A) = -2` → area scales by 2 and orientation flips
-   `det(A) = 0` → the transformation collapses space into a lower
    dimension

If:

$$
\det(A)=0
$$

the matrix cannot be inverted.

------------------------------------------------------------------------

# 14. 🔁 Inverse of a Matrix

## Definition

The inverse of a matrix `A` is written:

$$
A^{-1}
$$

It satisfies:

$$
AA^{-1}=A^{-1}A=I
$$

Think of an inverse as an **undo operation**.

> Matrix `A` performs a transformation.\
> Matrix `A⁻¹` reverses that transformation.

------------------------------------------------------------------------

## 🧮 Inverse of a 2 × 2 Matrix

If:

```math
A =
\begin{bmatrix}
a & b \\
c & d
\end{bmatrix}
```

then:

```math
A^{-1}
=
\frac{1}{ad-bc}
\begin{bmatrix}
d & -b \\
-c & a
\end{bmatrix}
```

provided that:

```math
ad-bc \neq 0
```

### Steps

1.  🔄 Swap the diagonal elements `a` and `d`
2.  ➖ Change the signs of the off-diagonal elements `b` and `c`
3.  ➗ Divide everything by the determinant

------------------------------------------------------------------------

## 🚫 When the Inverse Does NOT Exist

If:

$$
\det(A)=0
$$

then:

-   ❌ `A⁻¹` does not exist
-   ⚠️ the matrix is called **singular**
-   📉 the transformation has collapsed at least one dimension

------------------------------------------------------------------------

# 15. 🧩 Solving Linear Equations Using Matrices

Consider the system:

```math
2x+y=5
```

```math
x+3y=6
```

This can be written as:

```math
A\mathbf{x}=\mathbf{b}
```

where:

```math
A =
\begin{bmatrix}
2 & 1 \\
1 & 3
\end{bmatrix}
```

```math
\mathbf{x} =
\begin{bmatrix}
x \\
y
\end{bmatrix}
```

and:

```math
\mathbf{b} =
\begin{bmatrix}
5 \\
6
\end{bmatrix}
```

Therefore:

```math
\begin{bmatrix}
2 & 1 \\
1 & 3
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
=
\begin{bmatrix}
5 \\
6
\end{bmatrix}
```

If `A` is invertible:

```math
A\mathbf{x}=\mathbf{b}
```

Multiply both sides by:

```math
A^{-1}
```

Then:

```math
A^{-1}A\mathbf{x}=A^{-1}\mathbf{b}
```

Since:

```math
A^{-1}A=I
```

we get:

```math
\mathbf{x}=A^{-1}\mathbf{b}
```
This is one reason matrix inverses are useful.

> 📌 In practical numerical computing, systems are usually solved with
> specialized algorithms rather than explicitly calculating the inverse.

------------------------------------------------------------------------

# 16. ✅ Key Takeaways

-   🗃️ Matrices organize multivariate data.
-   📐 Matrix dimensions are written as **rows × columns**.
-   🔢 Individual values are called matrix elements.
-   🏹 A vector is a one-row or one-column matrix.
-   🔄 Transpose converts rows into columns.
-   🪞 A symmetric matrix satisfies `A = Aᵀ`.
-   ➕ Addition requires matrices of the same size.
-   ✖️ Scalar multiplication multiplies every element.
-   ⚙️ Matrix multiplication follows strict dimension rules.
-   🚫 Matrix multiplication is generally not commutative.
-   🪞 The identity matrix behaves like the number `1`.
-   📏 The determinant provides information about scaling and
    invertibility.
-   🔁 An inverse matrix reverses a transformation.
-   ❌ If `det(A) = 0`, the inverse does not exist.
-   🧩 Matrix methods can solve systems of linear equations.

These concepts are foundational for:

-   📊 PCA
-   📈 Regression
-   🤖 Machine learning
-   🧬 Systems biology
-   🧪 Bioinformatics
-   🧠 Neural networks
-   🎮 Computer graphics
-   🦾 Robotics
-   📡 Signal processing

------------------------------------------------------------------------

# 17. 🧠 The Deeper Idea

There are really **three levels of understanding**.

## Level 1 --- 📋 Matrix as a Table

Think:

> **"Numbers arranged in rows and columns."**

Example:

$$
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
$$

This is useful, but it is only the beginning.

------------------------------------------------------------------------


## Level 2 — 📝 Matrix as Instructions

Think:

> **"These numbers tell me how to combine my inputs."**

Example:

```math
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
\begin{bmatrix}
5 \\
6
\end{bmatrix}
=
\begin{bmatrix}
17 \\
39
\end{bmatrix}
```

The matrix gives instructions for how the input values should be mixed
together.

------------------------------------------------------------------------

## Level 3 --- ⚙️ Matrix as a Transformation

Think:

> **"This matrix is a machine that transforms space or data."**

A matrix can:

``` text
stretch
   ↓
rotate
   ↓
squash
   ↓
reflect
   ↓
combine
   ↓
transform
```

vectors and datasets.

This perspective is central to **linear algebra**.

------------------------------------------------------------------------

# 18. ⭐ One Sentence to Remember

If you remember only one thing, remember this:

> 🏹 **A vector tells us "what we have."**  
> ⚙️ **A matrix tells us "what to do with it."**

Conceptually:

```math
\text{Matrix} \times \text{Vector}
=
\text{New Vector}
```
Think:

``` text
⚙️ MACHINE × 📥 INPUT = 📤 OUTPUT
```

Once this mental picture becomes clear, the following topics become much
easier:

``` text
Matrices
   ↓
Matrix multiplication
   ↓
Determinants
   ↓
Inverse matrices
   ↓
Eigenvalues & eigenvectors
   ↓
PCA
   ↓
Machine learning
   ↓
Neural networks
```

------------------------------------------------------------------------

# 💡 Final Mental Model

``` text
┌──────────────┐
│    VECTOR    │
│  What do I   │
│    have?     │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│    MATRIX    │
│ What should  │
│ I do to it?  │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ NEW VECTOR   │
│   Result     │
└──────────────┘
```

> 🎯 **Matrix = data structure + mathematical instructions +
> transformation machine**

------------------------------------------------------------------------
