# 🐍 Multivariate Statistics in Python

## Complete Notes: Matrices, Eigenvectors, DataFrames, Random Data & Plotting

These notes introduce the basic **Python programming and linear algebra tools** required for multivariate statistics.

Before studying advanced techniques such as **Principal Component Analysis (PCA)**, clustering, classification, and other multivariate methods, it is important to understand:

1. 🔢 Arrays, matrices, and matrix operations
2. ⭐ Eigenvectors and eigenvalues
3. 📋 DataFrames in Python
4. 🎲 Generating random data
5. 📈 Graphical visualization of multivariate data

> 💡 **Important:** The examples in these notes are designed for learning and demonstration. They should not be interpreted as real biological conclusions.

---

# 1. 📚 About These Notes

Multivariate statistics deals with datasets where **multiple variables are measured for each observation**.

For example, a biological dataset may contain:

* 🧬 Gene expression
* ⚖️ Weight
* 📏 Height
* 🌡️ Temperature
* 🩸 Blood pressure
* 🧪 Biomarker concentrations

Python provides several important libraries for working with this type of data.

The most commonly used are:

* 🔢 **NumPy** → numerical arrays and matrix operations
* 📋 **pandas** → DataFrames and data manipulation
* 📈 **Matplotlib** → plotting
* 🎨 **Seaborn** → statistical visualization
* 🔬 **SciPy** → scientific and statistical calculations
* 🤖 **scikit-learn** → machine learning and multivariate methods

---

# 2. 📦 Installing Python Packages

Python packages can be installed using `pip`.

For example:

```bash
pip install numpy
pip install pandas
pip install matplotlib
pip install seaborn
pip install scipy
pip install scikit-learn
```

Inside a Jupyter Notebook, you may also use:

```python
%pip install numpy pandas matplotlib seaborn scipy scikit-learn
```

---

# 3. 📚 Importing Python Libraries

Once installed, libraries must be imported.

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

For statistical graphics:

```python
import seaborn as sns
```

For scientific calculations:

```python
import scipy
```

For machine learning:

```python
import sklearn
```

---

## 🧠 Common Abbreviations

These aliases are widely used in Python:

| Library           | Standard Alias |
| ----------------- | -------------- |
| NumPy             | `np`           |
| pandas            | `pd`           |
| Matplotlib pyplot | `plt`          |
| Seaborn           | `sns`          |

Therefore:

```python
import numpy as np
```

allows us to write:

```python
np.array(...)
```

instead of:

```python
numpy.array(...)
```

---

# 4. 🔢 Arrays and Matrices in Python

## What Is a Matrix?

A **matrix** is a rectangular arrangement of numbers organized into:

* ➡️ Rows
* ⬇️ Columns

For example:

```math
A =
\begin{bmatrix}
3 & 1 & 0 \\
5 & 3 & 8
\end{bmatrix}
```

This matrix contains:

```text
2 rows
3 columns
```

Therefore, its dimension is:

```math
2 \times 3
```

In Python, matrices are usually represented using **NumPy arrays**.

---

# 5. 💻 Creating a Matrix with NumPy

Import NumPy:

```python
import numpy as np
```

Create a matrix:

```python
A = np.array([
    [3, 1, 0],
    [5, 3, 8]
])
```

The matrix is:

```math
A =
\begin{bmatrix}
3 & 1 & 0 \\
5 & 3 & 8
\end{bmatrix}
```

Display it:

```python
print(A)
```

Output:

```text
[[3 1 0]
 [5 3 8]]
```

---

## 📐 Matrix Shape

Use:

```python
A.shape
```

Result:

```text
(2, 3)
```

Meaning:

```text
2 rows
3 columns
```

---

# 6. 🔍 Extracting Elements from a Matrix

Consider:

```python
A = np.array([
    [67, 170, 120],
    [77, 173, 123],
    [89, 179, 130]
])
```

Mathematically:

```math
A =
\begin{bmatrix}
67 & 170 & 120 \\
77 & 173 & 123 \\
89 & 179 & 130
\end{bmatrix}
```

> ⚠️ **Important:** Python indexing starts at **0**, not 1.

Therefore:

```text
First row    → index 0
Second row   → index 1
Third row    → index 2
```

---

## 🔹 Extract a Single Element

First row, third column:

```python
A[0, 2]
```

Result:

```text
120
```

Third row, second column:

```python
A[2, 1]
```

Result:

```text
179
```

---

## ➡️ Extract an Entire Row

```python
A[0, :]
```

or simply:

```python
A[0]
```

Result:

```text
[67 170 120]
```

---

## ⬇️ Extract an Entire Column

```python
A[:, 1]
```

Result:

```text
[170 173 179]
```

---

# 7. 🧩 Extracting Sub-Matrices

Suppose:

```python
A = np.array([
    [67, 170, 120],
    [77, 173, 123],
    [89, 179, 130]
])
```

Extract columns 2 and 3:

```python
G = A[:, 1:3]
```

Result:

```math
G =
\begin{bmatrix}
170 & 120 \\
173 & 123 \\
179 & 130
\end{bmatrix}
```

---

## 🧠 Understanding Python Slicing

```python
A[:, 1:3]
```

means:

```text
:    → all rows
1:3  → columns with indices 1 and 2
```

Python excludes the final index.

Therefore:

```python
1:3
```

selects:

```text
1 and 2
```

but not `3`.

---

# 8. 🏹 Vectors in Python

A one-dimensional vector can be created using:

```python
v = np.array([2, 3, 5, 1])
```

Output:

```text
[2 3 5 1]
```

---

## ⬇️ Column Vector

A column vector can be represented as:

```python
v = np.array([
    [2],
    [3],
    [5],
    [1]
])
```

Mathematically:

```math
v =
\begin{bmatrix}
2 \\
3 \\
5 \\
1
\end{bmatrix}
```

Shape:

```python
v.shape
```

Result:

```text
(4, 1)
```

---

## ➡️ Row Vector

```python
v = np.array([[2, 3, 5, 1]])
```

Mathematically:

```math
v =
\begin{bmatrix}
2 & 3 & 5 & 1
\end{bmatrix}
```

Shape:

```text
(1, 4)
```

---

# 9. 0️⃣ Zero Matrix

Create a zero matrix using:

```python
A = np.zeros((3, 3))
```

Result:

```math
A =
\begin{bmatrix}
0 & 0 & 0 \\
0 & 0 & 0 \\
0 & 0 & 0
\end{bmatrix}
```

---

# 10. 🔳 Identity Matrix

Create an identity matrix using:

```python
I = np.eye(3)
```

Result:

```math
I =
\begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
```

The identity matrix satisfies:

```math
AI = IA = A
```

It behaves similarly to the number **1** in ordinary multiplication.

---

# 11. 🔄 Transpose of a Matrix

Consider:

```python
A = np.array([
    [1, 3, 5],
    [2, 4, 6]
])
```

Mathematically:

```math
A =
\begin{bmatrix}
1 & 3 & 5 \\
2 & 4 & 6
\end{bmatrix}
```

Transpose:

```python
A.T
```

Result:

```math
A^T =
\begin{bmatrix}
1 & 2 \\
3 & 4 \\
5 & 6
\end{bmatrix}
```

The transpose changes:

```math
A_{m\times n}
\rightarrow
A^T_{n\times m}
```

---

# 12. 🪞 Symmetric Matrices

A matrix is **symmetric** when:

```math
A=A^T
```

For example:

```python
A = np.array([
    [2, 1],
    [1, 3]
])
```

Mathematically:

```math
A =
\begin{bmatrix}
2 & 1 \\
1 & 3
\end{bmatrix}
```

Check:

```python
A.T
```

---

## ✅ Checking Symmetry Automatically

For exact values:

```python
np.array_equal(A, A.T)
```

For numerical calculations, a safer method is:

```python
np.allclose(A, A.T)
```

> 💡 `np.allclose()` allows for small floating-point rounding differences.

Symmetric matrices are extremely important because **covariance and correlation matrices are symmetric**.

---

# 13. ➕ Matrix Addition and Subtraction

Suppose:

```python
A = np.array([
    [1, 2],
    [3, 4]
])

B = np.array([
    [2, 2],
    [2, 2]
])
```

Then:

```math
A =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
```

and:

```math
B =
\begin{bmatrix}
2 & 2 \\
2 & 2
\end{bmatrix}
```

Addition:

```python
A + B
```

Result:

```math
A+B =
\begin{bmatrix}
3 & 4 \\
5 & 6
\end{bmatrix}
```

Subtraction:

```python
A - B
```

Result:

```math
A-B =
\begin{bmatrix}
-1 & 0 \\
1 & 2
\end{bmatrix}
```

> 📌 For straightforward element-by-element addition and subtraction, matrices should have compatible shapes.

---

# 14. ✖️ Scalar Multiplication

Multiply a matrix by 3:

```python
3 * A
```

If:

```math
A =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
```

then:

```math
3A =
\begin{bmatrix}
3 & 6 \\
9 & 12
\end{bmatrix}
```

---

# 15. ✖️ Matrix Multiplication

Suppose:

```python
A = np.array([
    [1, 2],
    [3, 4]
])

v = np.array([
    [3],
    [4]
])
```

Then:

```math
A =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
```

and:

```math
v =
\begin{bmatrix}
3 \\
4
\end{bmatrix}
```

Use:

```python
A @ v
```

Result:

```math
Av =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
\begin{bmatrix}
3 \\
4
\end{bmatrix}
```

Therefore:

```math
Av =
\begin{bmatrix}
1(3)+2(4) \\
3(3)+4(4)
\end{bmatrix}
=
\begin{bmatrix}
11 \\
25
\end{bmatrix}
```

---

## 🔹 Alternative

NumPy also provides:

```python
np.matmul(A, v)
```

or:

```python
np.dot(A, v)
```

For ordinary modern NumPy matrix multiplication, the clearest notation is generally:

```python
A @ v
```

---

## ⚠️ `*` vs `@`

This distinction is extremely important.

### Element-Wise Multiplication

```python
A * B
```

multiplies corresponding elements.

### Matrix Multiplication

```python
A @ B
```

performs linear algebra matrix multiplication.

> 🧠 **Remember:**
> `*` = element-wise multiplication
> `@` = matrix multiplication

---

# 16. 🔁 Order Matters in Matrix Multiplication

In general:

```math
AB \neq BA
```

In Python:

```python
A @ B
```

and:

```python
B @ A
```

may produce different results.

> 📌 Matrix multiplication is generally **not commutative**.

---

# 17. 🔳 Identity Matrix Property

Create:

```python
I = np.eye(2)
```

For:

```python
v = np.array([
    [3],
    [4]
])
```

calculate:

```python
I @ v
```

The result is:

```math
Iv=v
```

Therefore:

```math
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
\begin{bmatrix}
3 \\
4
\end{bmatrix}
=
\begin{bmatrix}
3 \\
4
\end{bmatrix}
```

---

# 18. 📐 Matrix Dimension Compatibility

Suppose:

```math
A_{m\times n}
```

and:

```math
B_{n\times p}
```

Then:

```math
AB
```

is valid.

The result has dimensions:

```math
m\times p
```

### 🧠 Easy Rule

```text
(m × n)(n × p)
     ↑  ↑
These must match
```

Result:

```text
m × p
```

Example:

```math
(2\times3)(3\times4)
\rightarrow
(2\times4)
```

---

# 19. 🧮 Determinant of a Matrix

For a $2\times2$ matrix:

```math
A =
\begin{bmatrix}
a & b \\
c & d
\end{bmatrix}
```

the determinant is:

```math
\det(A)=ad-bc
```

In Python:

```python
A = np.array([
    [3, 2],
    [2, 4]
])

np.linalg.det(A)
```

Mathematically:

```math
\det(A)
=
(3)(4)-(2)(2)
=
8
```

Because numerical computation uses floating-point arithmetic, Python may return a value extremely close to 8 rather than displaying it exactly as an integer.

---

# 20. 🔢 3 × 3 Determinant

Create:

```python
A = np.array([
    [1, 2, 3],
    [4, 5, 5],
    [3, 2, 3]
])
```

Calculate:

```python
np.linalg.det(A)
```

NumPy calculates the determinant automatically.

---

# 21. 🔁 Inverse of a Matrix

The inverse of matrix $A$ is written:

```math
A^{-1}
```

It satisfies:

```math
AA^{-1}=I
```

and:

```math
A^{-1}A=I
```

In Python:

```python
A = np.array([
    [3, 1],
    [4, 2]
])

A_inv = np.linalg.inv(A)
```

Display:

```python
A_inv
```

---

## ✅ Identity Check

Check:

```python
A @ A_inv
```

The result should be approximately:

```math
I =
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
```

A better numerical check is:

```python
np.allclose(A @ A_inv, np.eye(2))
```

---

# 22. ❌ Singular Matrix

Consider:

```python
B = np.array([
    [3, 2],
    [3, 2]
])
```

The rows are linearly dependent.

Therefore:

```math
\det(B)=0
```

and $B$ is **singular**.

Trying:

```python
np.linalg.inv(B)
```

will fail because the matrix has no inverse.

> 📌 A square matrix is invertible only when its determinant is non-zero.

---

# 23. 🧩 Solving Linear Equations

Consider:

```math
3a+b=4
```

```math
4a+2b=6
```

Write this as:

```math
\begin{bmatrix}
3 & 1 \\
4 & 2
\end{bmatrix}
\begin{bmatrix}
a \\
b
\end{bmatrix}
=
\begin{bmatrix}
4 \\
6
\end{bmatrix}
```

In matrix notation:

```math
Ax=b
```

In Python:

```python
A = np.array([
    [3, 1],
    [4, 2]
])

b = np.array([4, 6])

x = np.linalg.solve(A, b)
```

Display:

```python
x
```

Result:

```text
[1. 1.]
```

Therefore:

```math
a=1
```

and:

```math
b=1
```

---

# 24. ⭐ Eigenvectors and Eigenvalues

The fundamental eigenvector equation is:

```math
Av=\lambda v
```

where:

* $A$ = matrix
* $v$ = eigenvector
* $\lambda$ = eigenvalue

An **eigenvector** is a special vector whose direction remains on the same line after transformation by $A$.

The **eigenvalue** tells us how much the eigenvector is scaled.

---

# 25. 🏹 Creating a Vector for Plotting

Define:

```python
v = np.array([3, 3])
```

The vector is:

```math
v =
\begin{bmatrix}
3 \\
3
\end{bmatrix}
```

To draw the vector:

```python
import matplotlib.pyplot as plt

plt.figure()

plt.quiver(
    0, 0,
    v[0], v[1],
    angles="xy",
    scale_units="xy",
    scale=1
)

plt.xlim(0, 5)
plt.ylim(0, 5)

plt.grid()
plt.xlabel("x")
plt.ylabel("y")

plt.show()
```

The arrow starts at:

```math
(0,0)
```

and ends at:

```math
(3,3)
```

---

# 26. 📏 Vector Length

For:

```math
v =
\begin{bmatrix}
v_1 \\
v_2 \\
\vdots \\
v_n
\end{bmatrix}
```

the Euclidean norm is:

```math
\|v\|
=
\sqrt{
v_1^2+v_2^2+\cdots+v_n^2
}
```

In NumPy:

```python
np.linalg.norm(v)
```

For:

```python
v = np.array([3, 3])
```

the length is:

```math
\|v\|
=
\sqrt{3^2+3^2}
=
\sqrt{18}
```

---

# 27. 🔍 Checking an Eigenvector

Consider:

```python
A = np.array([
    [1, 2],
    [1, 0]
])

v = np.array([2, 1])
```

Calculate:

```python
Av = A @ v
```

Mathematically:

```math
Av =
\begin{bmatrix}
1 & 2 \\
1 & 0
\end{bmatrix}
\begin{bmatrix}
2 \\
1
\end{bmatrix}
```

Therefore:

```math
Av =
\begin{bmatrix}
4 \\
2
\end{bmatrix}
```

But:

```math
2v =
2
\begin{bmatrix}
2 \\
1
\end{bmatrix}
=
\begin{bmatrix}
4 \\
2
\end{bmatrix}
```

Therefore:

```math
Av=2v
```

✅ $v$ is an eigenvector.

The corresponding eigenvalue is:

```math
\lambda=2
```

---

# 28. 🔢 Estimating the Eigenvalue from Vector Length

For a positive eigenvalue:

```python
np.linalg.norm(Av) / np.linalg.norm(v)
```

In this example:

```math
\frac{\|Av\|}{\|v\|}
=
2
```

Therefore:

```math
\lambda=2
```

> ⚠️ This ratio gives $|\lambda|$. If the eigenvalue is negative, the transformed eigenvector points in the opposite orientation, and the sign must be determined separately.

A more direct verification is:

```python
Av / v
```

when all components of `v` are non-zero and the ratios are well-defined.

---

# 29. 📏 Normalizing an Eigenvector

To normalize a vector:

```python
v_normalized = v / np.linalg.norm(v)
```

Mathematically:

```math
\hat{v}
=
\frac{v}{\|v\|}
```

The normalized vector satisfies:

```math
\|\hat{v}\|=1
```

Check:

```python
np.linalg.norm(v_normalized)
```

The result should be:

```text
1.0
```

---

# 30. 💻 Eigenvalues and Eigenvectors in Python

NumPy calculates eigenvalues and eigenvectors using:

```python
np.linalg.eig(A)
```

For example:

```python
A = np.array([
    [1, 2],
    [1, 0]
])

eigenvalues, eigenvectors = np.linalg.eig(A)
```

View the eigenvalues:

```python
eigenvalues
```

View the eigenvectors:

```python
eigenvectors
```

> 📌 The eigenvectors are stored as **columns** of the returned eigenvector matrix.

Therefore:

```python
eigenvectors[:, 0]
```

is the first eigenvector.

And:

```python
eigenvectors[:, 1]
```

is the second eigenvector.

---

# 31. 🪞 Eigenvalues of Symmetric Matrices

For real symmetric matrices, NumPy provides:

```python
np.linalg.eigh(A)
```

rather than:

```python
np.linalg.eig(A)
```

For example:

```python
A = np.array([
    [2, 1],
    [1, 2]
])

eigenvalues, eigenvectors = np.linalg.eigh(A)
```

`eigh()` is specifically designed for **real symmetric or complex Hermitian matrices**.

This is especially relevant in PCA because covariance matrices are symmetric.

---

# 32. 📈 Plotting Eigenvectors

Calculate:

```python
A = np.array([
    [1, 2],
    [1, 0]
])

eigenvalues, eigenvectors = np.linalg.eig(A)
```

Plot:

```python
plt.figure()

plt.quiver(
    0, 0,
    eigenvectors[0, 0],
    eigenvectors[1, 0],
    angles="xy",
    scale_units="xy",
    scale=1
)

plt.quiver(
    0, 0,
    eigenvectors[0, 1],
    eigenvectors[1, 1],
    angles="xy",
    scale_units="xy",
    scale=1
)

plt.xlim(-1, 1)
plt.ylim(-1, 1)

plt.axhline(0)
plt.axvline(0)
plt.grid()

plt.xlabel("x")
plt.ylabel("y")

plt.show()
```

This visualizes the special directions associated with the matrix.

---

# 33. 📋 Working with pandas DataFrames

A **DataFrame** is one of the most important data structures in Python data analysis.

Typically:

* ➡️ Rows represent observations
* ⬇️ Columns represent variables

Import pandas:

```python
import pandas as pd
```

Create the data:

```python
data = {
    "Gender": ["M", "F", "F", "F", "M", "M", "F"],
    "Weight": [80, 58, 65, 70, 90, 100, 50],
    "Height": [190, 171, 175, 169, 182, 183, 165],
    "Temp": [37.5, 38.3, 37.0, 37.9, 38.6, 40.1, 36.7]
}
```

Create a DataFrame:

```python
df = pd.DataFrame(data)
```

Display:

```python
df
```

Conceptually:

| Gender | Weight | Height | Temp |
| ------ | -----: | -----: | ---: |
| M      |     80 |    190 | 37.5 |
| F      |     58 |    171 | 38.3 |
| F      |     65 |    175 | 37.0 |
| F      |     70 |    169 | 37.9 |
| M      |     90 |    182 | 38.6 |
| M      |    100 |    183 | 40.1 |
| F      |     50 |    165 | 36.7 |

---

# 34. 🔍 Inspecting a DataFrame

View the first five rows:

```python
df.head()
```

View the final five rows:

```python
df.tail()
```

Check shape:

```python
df.shape
```

Result:

```text
(7, 4)
```

Meaning:

```text
7 rows
4 columns
```

---

# 35. 🧬 Data Types

Check column data types:

```python
df.dtypes
```

You may see something similar to:

```text
Gender     object
Weight      int64
Height      int64
Temp      float64
```

---

## 📋 DataFrame Information

Use:

```python
df.info()
```

This displays:

* Column names
* Number of observations
* Missing values
* Data types
* Memory usage

---

# 36. 📊 Summarizing a DataFrame

Use:

```python
df.describe()
```

For numerical variables, this gives:

* `count`
* `mean`
* `std`
* `min`
* `25%`
* `50%`
* `75%`
* `max`

To include categorical columns as well:

```python
df.describe(include="all")
```

---

# 37. 🔍 Selecting Columns

Select one column:

```python
df["Weight"]
```

Select several columns:

```python
df[["Weight", "Height", "Temp"]]
```

---

# 38. 🔍 Filtering Rows

Select only females:

```python
df[df["Gender"] == "F"]
```

This is conceptually similar to R:

```r
filter(df, Gender == "F")
```

---

## Multiple Conditions

For example:

```python
df[
    (df["Gender"] == "F") &
    (df["Weight"] > 60)
]
```

> 📌 With pandas filtering, use `&` for AND and `|` for OR between conditions, with each condition enclosed in parentheses.

---

# 39. 📍 `.loc` and `.iloc`

Two important pandas indexing methods are:

```text
.loc   → label-based selection
.iloc  → position-based selection
```

---

## `.loc`

Example:

```python
df.loc[:, ["Weight", "Height"]]
```

Select rows based on a condition:

```python
df.loc[df["Gender"] == "F"]
```

---

## `.iloc`

Select by position:

```python
df.iloc[0, 1]
```

means:

```text
First row
Second column
```

Select first three rows:

```python
df.iloc[0:3]
```

---

# 40. ➕ Creating a New Variable

Create a new column:

```python
df["BMI_example"] = df["Weight"] / (df["Height"] / 100) ** 2
```

This is conceptually similar to `mutate()` in R.

---

# 41. ↕️ Sorting Data

Sort by weight:

```python
df.sort_values("Weight")
```

Descending order:

```python
df.sort_values(
    "Weight",
    ascending=False
)
```

This is conceptually similar to `arrange()` in R.

---

# 42. 👥 Grouping Data

Calculate mean weight by gender:

```python
df.groupby("Gender")["Weight"].mean()
```

Calculate means for several numeric variables:

```python
df.groupby("Gender")[["Weight", "Height", "Temp"]].mean()
```

This is similar to combining:

```text
group_by()
+
summarise()
```

in R.

---

# 43. 🧮 Applying Functions

Calculate means:

```python
df[["Weight", "Height", "Temp"]].mean()
```

Calculate median:

```python
df[["Weight", "Height", "Temp"]].median()
```

Calculate standard deviation:

```python
df[["Weight", "Height", "Temp"]].std()
```

---

# 44. 🛠️ Creating Custom Python Functions

Define a function for the area of a circle:

```python
def circle_area(r):
    area = r**2 * np.pi
    return area
```

Use:

```python
circle_area(5)
```

The mathematical formula is:

```math
A=\pi r^2
```

---

# 45. 📏 Creating a Normalization Function

Define:

```python
def normalize(x):
    return x / x.max()
```

Apply it:

```python
normalized_df = df[
    ["Weight", "Height", "Temp"]
].apply(normalize)
```

The transformation is:

```math
x_i^*
=
\frac{x_i}{\max(x)}
```

> 📌 This is **max normalization**. It is not the same as z-score standardization.

---

# 46. 📐 Z-Score Standardization

A common transformation in multivariate statistics is:

```math
z =
\frac{x-\mu}{\sigma}
```

Using pandas:

```python
standardized = (
    df[["Weight", "Height", "Temp"]]
    - df[["Weight", "Height", "Temp"]].mean()
) / df[["Weight", "Height", "Temp"]].std()
```

In machine learning, this is commonly performed with:

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

standardized = scaler.fit_transform(
    df[["Weight", "Height", "Temp"]]
)
```

> 💡 Standardization becomes particularly important when variables have very different measurement scales.

---

# 47. 🎲 Generating Random Data with NumPy

Modern NumPy code commonly uses a random number generator:

```python
rng = np.random.default_rng()
```

Generate four observations from a standard normal distribution:

```python
rng.normal(
    loc=0,
    scale=1,
    size=4
)
```

where:

```text
loc   = mean
scale = standard deviation
size  = number of observations
```

---

# 48. 🌱 Setting a Random Seed

For reproducible results:

```python
rng = np.random.default_rng(12)
```

Now:

```python
rng.normal(
    loc=0,
    scale=1,
    size=4
)
```

produces a reproducible pseudo-random sequence.

> 💡 Reproducibility is extremely important in scientific computing.

---

# 49. 👥 Simulating Population Data

Suppose we want to simulate 40 heights with:

```text
Mean = 175
Standard deviation = 7
```

Use:

```python
rng = np.random.default_rng(12)

sim_data = rng.normal(
    loc=175,
    scale=7,
    size=40
)
```

Mathematically:

```math
X \sim N(175,7^2)
```

Calculate the mean:

```python
sim_data.mean()
```

or:

```python
np.mean(sim_data)
```

---

# 50. 📊 Histogram of Simulated Data

Plot:

```python
plt.figure()

plt.hist(sim_data)

plt.xlabel("Height")
plt.ylabel("Frequency")
plt.title("Simulated Heights")

plt.show()
```

The histogram shows the distribution of the simulated observations.

---

# 51. 🎲 Uniform Distribution

Generate values between 0 and 1:

```python
rng.uniform(
    low=0,
    high=1,
    size=100000
)
```

Mathematically:

```math
X\sim U(0,1)
```

Generate 100 numbers between 5 and 10:

```python
rng.uniform(
    low=5,
    high=10,
    size=100
)
```

---

# 52. 📚 Built-In / Example Data Sets

Python libraries contain several datasets useful for learning statistics and machine learning.

One of the most famous is the **Iris dataset**.

---

# 53. 🌸 Loading the Iris Dataset

Using scikit-learn:

```python
from sklearn.datasets import load_iris

iris = load_iris()
```

The data matrix is:

```python
iris.data
```

The target labels are:

```python
iris.target
```

Feature names:

```python
iris.feature_names
```

Species names:

```python
iris.target_names
```

---

# 54. 🌸 Convert Iris to a pandas DataFrame

Create a DataFrame:

```python
iris_df = pd.DataFrame(
    iris.data,
    columns=iris.feature_names
)
```

Add species:

```python
iris_df["species"] = iris.target
```

For readable species names:

```python
iris_df["species"] = iris_df["species"].map(
    dict(enumerate(iris.target_names))
)
```

View:

```python
iris_df.head()
```

---

# 55. 📊 Species-Specific Means

Calculate:

```python
iris_df.groupby("species").mean()
```

This calculates the mean of each numerical feature separately for each Iris species.

Conceptually:

```text
Species
   ↓
Group observations
   ↓
Calculate feature means
```

---

# 56. 📈 Graphical Illustration of Multivariate Data

Visualization should be an important early step in statistical analysis.

Plots can reveal:

* 🔗 Relationships
* 👥 Groups
* 📈 Trends
* ⚠️ Outliers
* 🧩 Clusters
* 📊 Distribution differences

---

# 57. 🔵 Scatter Plot

Plot petal width against petal length.

With the scikit-learn Iris column names:

```python
plt.figure()

plt.scatter(
    iris_df["petal width (cm)"],
    iris_df["petal length (cm)"]
)

plt.xlabel("Petal Width (cm)")
plt.ylabel("Petal Length (cm)")
plt.title("Petal Width vs Petal Length")

plt.show()
```

Each point represents one flower.

---

# 58. 🎨 Colored Scatter Plot by Species

Using Matplotlib:

```python
plt.figure()

for species in iris_df["species"].unique():

    subset = iris_df[
        iris_df["species"] == species
    ]

    plt.scatter(
        subset["petal width (cm)"],
        subset["petal length (cm)"],
        label=species
    )

plt.xlabel("Petal Width (cm)")
plt.ylabel("Petal Length (cm)")
plt.title("Iris Petal Measurements")

plt.legend()

plt.show()
```

This can reveal **species-specific clustering**.

---

## 🎨 Using Seaborn

A shorter statistical plotting approach is:

```python
sns.scatterplot(
    data=iris_df,
    x="petal width (cm)",
    y="petal length (cm)",
    hue="species"
)

plt.show()
```

---

# 59. 📦 Boxplots

Use Seaborn:

```python
sns.boxplot(
    data=iris_df,
    x="species",
    y="petal length (cm)"
)

plt.show()
```

The boxplot displays information about:

* Median
* Quartiles
* Spread
* Potential outliers

---

# 60. 📍 Boxplot + Individual Observations

Add individual observations:

```python
sns.boxplot(
    data=iris_df,
    x="species",
    y="petal length (cm)"
)

sns.stripplot(
    data=iris_df,
    x="species",
    y="petal length (cm)",
    jitter=True
)

plt.show()
```

This combines a statistical summary with the raw observations.

---

# 61. 📍 Strip Plot

A strip plot can be created directly:

```python
sns.stripplot(
    data=iris_df,
    x="species",
    y="petal length (cm)",
    jitter=True
)

plt.show()
```

This helps visualize:

* Sample density
* Variation
* Individual observations
* Group differences

---

# 62. 🔢 Scatter Plot Matrix

A scatterplot matrix is an important exploratory tool for multivariate data.

Using pandas:

```python
pd.plotting.scatter_matrix(
    iris_df.iloc[:, 0:4]
)

plt.show()
```

A more informative version can be created with Seaborn:

```python
sns.pairplot(
    iris_df,
    hue="species"
)

plt.show()
```

This compares all numerical variables pairwise.

It can reveal:

* 🔗 Correlations
* 🌸 Species separation
* 🧩 Clusters
* ⚠️ Outliers
* 📈 Linear relationships

---

# 63. 📉 Parallel Coordinates / Profile Plot

Python can produce a multivariate profile plot using pandas.

Import:

```python
from pandas.plotting import parallel_coordinates
```

Then:

```python
parallel_coordinates(
    iris_df,
    class_column="species"
)

plt.show()
```

Each line represents one flower.

The axes represent the numerical variables.

This allows us to compare multivariate profiles across species.

---

# 64. 🔗 Correlation Matrix

Correlation matrices are extremely important in multivariate statistics.

Calculate:

```python
corr = iris_df.iloc[:, 0:4].corr()
```

Display:

```python
corr
```

A correlation matrix has the general form:

```math
R =
\begin{bmatrix}
1 & r_{12} & r_{13} & \cdots \\
r_{21} & 1 & r_{23} & \cdots \\
r_{31} & r_{32} & 1 & \cdots \\
\vdots & \vdots & \vdots & \ddots
\end{bmatrix}
```

Notice that:

```math
R=R^T
```

Therefore, a correlation matrix is **symmetric**.

---

# 65. 🔥 Correlation Heatmap

Using Seaborn:

```python
corr = iris_df.iloc[:, 0:4].corr()

sns.heatmap(
    corr,
    annot=True
)

plt.title("Iris Correlation Matrix")

plt.show()
```

This provides a visual representation of relationships among variables.

---

# 66. 📊 Covariance Matrix

Calculate the covariance matrix:

```python
cov_matrix = iris_df.iloc[:, 0:4].cov()
```

Display:

```python
cov_matrix
```

Alternatively, using NumPy:

```python
X = iris_df.iloc[:, 0:4].to_numpy()

cov_matrix = np.cov(
    X,
    rowvar=False
)
```

> 📌 `rowvar=False` tells NumPy that the **columns are variables** and rows are observations.

---

# 67. 🪞 Covariance Matrices Are Symmetric

A covariance matrix satisfies:

```math
C=C^T
```

Check:

```python
np.allclose(
    cov_matrix,
    cov_matrix.T
)
```

This should return:

```text
True
```

This symmetry is one reason eigenvalue decomposition works especially well in PCA.

---

# 68. ⭐ Eigenvalues of a Covariance Matrix

Calculate:

```python
eigenvalues, eigenvectors = np.linalg.eigh(
    cov_matrix
)
```

View eigenvalues:

```python
eigenvalues
```

View eigenvectors:

```python
eigenvectors
```

Since covariance matrices are symmetric, their eigenvalues are real and their eigenvectors can be chosen orthonormally.

---

# 69. 📊 Connection to PCA

The basic PCA workflow is:

```text
Data Matrix
     ↓
Center / Standardize Variables
     ↓
Covariance or Correlation Matrix
     ↓
Eigenvalues + Eigenvectors
     ↓
Principal Components
     ↓
Dimensionality Reduction
```

---

## 🏹 Eigenvectors in PCA

Eigenvectors determine:

> 🧭 **The directions of the principal components**

Conceptually:

```text
Eigenvector 1 → Direction of PC1
Eigenvector 2 → Direction of PC2
Eigenvector 3 → Direction of PC3
```

---

## 🔢 Eigenvalues in PCA

Eigenvalues indicate how much variance is associated with each principal component.

Conceptually:

```text
Largest Eigenvalue
        ↓
Largest Variance
        ↓
PC1
```

---

# 70. 🤖 PCA with scikit-learn

Import:

```python
from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler
```

Select numerical variables:

```python
X = iris_df.iloc[:, 0:4]
```

Standardize:

```python
scaler = StandardScaler()

X_scaled = scaler.fit_transform(X)
```

Create PCA:

```python
pca = PCA()
```

Fit PCA:

```python
X_pca = pca.fit_transform(X_scaled)
```

---

## 📊 Explained Variance

View:

```python
pca.explained_variance_
```

These are related to the eigenvalues of the covariance matrix of the standardized data.

---

## 📈 Explained Variance Ratio

View:

```python
pca.explained_variance_ratio_
```

This gives the proportion of variance explained by each principal component.

If:

```math
\lambda_1,\lambda_2,\ldots,\lambda_p
```

are the eigenvalues, then:

```math
\text{Variance Explained by PC}_i
=
\frac{\lambda_i}
{\lambda_1+\lambda_2+\cdots+\lambda_p}
```

---

# 71. 📊 Creating a PCA DataFrame

Create:

```python
pca_df = pd.DataFrame(
    X_pca,
    columns=[
        "PC1",
        "PC2",
        "PC3",
        "PC4"
    ]
)
```

Add species:

```python
pca_df["species"] = iris_df["species"]
```

View:

```python
pca_df.head()
```

---

# 72. 📈 Plotting PC1 vs PC2

```python
sns.scatterplot(
    data=pca_df,
    x="PC1",
    y="PC2",
    hue="species"
)

plt.title("PCA of Iris Dataset")

plt.show()
```

This allows us to visualize a four-dimensional dataset using two principal components.

---

# 73. 🧠 Important NumPy Functions

| Python              | Meaning                                              |
| ------------------- | ---------------------------------------------------- |
| `np.array()`        | Create array or matrix                               |
| `A.shape`           | Matrix dimensions                                    |
| `A.T`               | Transpose                                            |
| `A @ B`             | Matrix multiplication                                |
| `A * B`             | Element-wise multiplication                          |
| `np.zeros()`        | Zero matrix                                          |
| `np.eye()`          | Identity matrix                                      |
| `np.linalg.det()`   | Determinant                                          |
| `np.linalg.inv()`   | Matrix inverse                                       |
| `np.linalg.solve()` | Solve linear system                                  |
| `np.linalg.norm()`  | Vector or matrix norm                                |
| `np.linalg.eig()`   | General eigenvalue decomposition                     |
| `np.linalg.eigh()`  | Eigen decomposition for symmetric/Hermitian matrices |
| `np.cov()`          | Covariance matrix                                    |
| `np.corrcoef()`     | Correlation matrix                                   |

---

# 74. 🧠 Important pandas Functions

| Python             | Meaning                    |
| ------------------ | -------------------------- |
| `pd.DataFrame()`   | Create DataFrame           |
| `df.head()`        | First rows                 |
| `df.tail()`        | Last rows                  |
| `df.shape`         | Number of rows and columns |
| `df.info()`        | Structure and data types   |
| `df.describe()`    | Summary statistics         |
| `df["x"]`          | Select a column            |
| `df.loc[]`         | Label-based selection      |
| `df.iloc[]`        | Position-based selection   |
| `df.groupby()`     | Group observations         |
| `df.mean()`        | Calculate means            |
| `df.corr()`        | Correlation matrix         |
| `df.cov()`         | Covariance matrix          |
| `df.sort_values()` | Sort rows                  |
| `df.apply()`       | Apply a function           |

---

# 75. 🆚 R vs Python – Quick Translation

| Task                        | R              | Python                      |
| --------------------------- | -------------- | --------------------------- |
| Create matrix               | `matrix()`     | `np.array()`                |
| Dimensions                  | `dim(A)`       | `A.shape`                   |
| Transpose                   | `t(A)`         | `A.T`                       |
| Identity matrix             | `diag(n)`      | `np.eye(n)`                 |
| Matrix multiplication       | `%*%`          | `@`                         |
| Element-wise multiplication | `*`            | `*`                         |
| Determinant                 | `det(A)`       | `np.linalg.det(A)`          |
| Inverse                     | `solve(A)`     | `np.linalg.inv(A)`          |
| Solve $Ax=b$                | `solve(A,b)`   | `np.linalg.solve(A,b)`      |
| Eigen decomposition         | `eigen(A)`     | `np.linalg.eig(A)`          |
| Data frame                  | `data.frame()` | `pd.DataFrame()`            |
| Structure                   | `str(df)`      | `df.info()`                 |
| Summary                     | `summary(df)`  | `df.describe()`             |
| Filter                      | `filter()`     | Boolean indexing / `.loc[]` |
| Group                       | `group_by()`   | `groupby()`                 |
| Apply function              | `lapply()`     | `.apply()`                  |
| Random normal               | `rnorm()`      | `rng.normal()`              |
| Random uniform              | `runif()`      | `rng.uniform()`             |
| Scatter plot                | `plot()`       | `plt.scatter()`             |
| Scatterplot matrix          | `pairs()`      | `sns.pairplot()`            |

---

# 76. 🎯 Matrix Operations – Quick Summary

```text
Create matrix
      ↓
np.array()

Check dimensions
      ↓
A.shape

Extract element
      ↓
A[row, column]

Transpose
      ↓
A.T

Symmetry
      ↓
np.allclose(A, A.T)

Determinant
      ↓
np.linalg.det(A)

Inverse
      ↓
np.linalg.inv(A)

Matrix multiplication
      ↓
A @ B

Eigenvalues / eigenvectors
      ↓
np.linalg.eig(A)
```

---

# 77. 🧠 DataFrame Operations – Quick Summary

```text
Create
  ↓
pd.DataFrame()

Inspect
  ↓
df.info()

Preview
  ↓
df.head()

Summarize
  ↓
df.describe()

Filter
  ↓
df.loc[]
or Boolean indexing

Group
  ↓
df.groupby()

Apply function
  ↓
df.apply()
```

---

# 78. 🚀 From Matrices to Multivariate Statistics

The concepts connect directly to advanced methods.

```text
NumPy Arrays
      ↓
Matrix Operations
      ↓
Eigenvalues + Eigenvectors
      ↓
Covariance / Correlation Matrix
      ↓
PCA
      ↓
Dimensionality Reduction
      ↓
Advanced Multivariate Statistics
```

At the same time:

```text
pandas DataFrames
       ↓
Data Cleaning
       ↓
Data Transformation
       ↓
Exploratory Analysis
       ↓
Visualization
       ↓
Statistical / Machine-Learning Models
```

---

# 79. 🧬 Why This Matters in Biological Data Analysis

Biological datasets often contain many variables for every sample.

For example:

```text
Patient / Sample
       ↓
┌───────────────────────────┐
│ Gene Expression           │
│ Protein Concentration     │
│ Metabolites               │
│ Age                       │
│ Weight                    │
│ Biomarkers                │
│ Treatment Response        │
└───────────────────────────┘
```

This naturally produces **multivariate data**.

NumPy provides the mathematical structure for matrix computations, while pandas provides a practical tabular structure for managing datasets.

---

# 80. 🔑 Key Takeaways

| Concept                   | 💡 Key Point                                                      |
| ------------------------- | ----------------------------------------------------------------- |
| 🐍 **Python**             | Powerful environment for statistics and data science              |
| 🔢 **NumPy array**        | Main structure for numerical and matrix calculations              |
| 📋 **pandas DataFrame**   | Main tabular data structure                                       |
| `@`                       | Matrix multiplication                                             |
| `*`                       | Element-wise multiplication                                       |
| 🔄 **Transpose**          | Exchanges rows and columns                                        |
| 🪞 **Symmetric matrix**   | $A=A^T$                                                           |
| 🧮 **Determinant**        | Helps determine matrix invertibility                              |
| 🔁 **Inverse**            | Satisfies $AA^{-1}=I$                                             |
| ⭐ **Eigenvector**         | Direction preserved under matrix transformation                   |
| 🔢 **Eigenvalue**         | Scaling factor associated with an eigenvector                     |
| 🎲 **Random simulation**  | Useful for learning and statistical modeling                      |
| 🌱 **Random seed**        | Makes simulations reproducible                                    |
| 📈 **Visualization**      | Reveals patterns before modeling                                  |
| 🔗 **Covariance matrix**  | Describes joint variation                                         |
| 🔗 **Correlation matrix** | Describes standardized linear relationships                       |
| 📊 **PCA**                | Uses eigenvectors/eigenvalues or equivalent matrix decomposition  |
| 🤖 **scikit-learn**       | Provides PCA, clustering, classification, preprocessing, and more |

---

# 81. 🎯 Final Summary

The foundations of multivariate statistics in Python can be summarized as:

```text
                MULTIVARIATE STATISTICS
                          │
         ┌────────────────┼────────────────┐
         │                │                │
         ▼                ▼                ▼
       NUMPY           PANDAS        VISUALIZATION
         │                │                │
         ▼                ▼                ▼
Matrix Operations     DataFrames      Explore Data
         │
         ▼
Eigenvalues + Eigenvectors
         │
         ▼
Covariance / Correlation
         │
         ▼
        PCA
         │
         ▼
Dimensionality Reduction
         │
         ▼
Advanced Multivariate Analysis
```

### 🌟 Most Important Ideas

* 🔢 **NumPy provides the mathematical foundation for matrix-based analysis in Python.**
* ⭐ **Eigenvalues and eigenvectors are fundamental concepts behind PCA and many multivariate methods.**
* 📋 **pandas DataFrames are central to practical data analysis.**
* 🎲 **NumPy's random-number generators allow reproducible statistical simulations.**
* 📈 **Visualization should be an important early step before complex modeling.**
* 🔗 **Covariance and correlation matrices describe relationships among multiple variables.**
* 📊 **PCA transforms correlated variables into a smaller set of principal components.**
* 🧬 Together, these tools provide a foundation for analyzing biological and high-dimensional datasets.

> 🚀 **Final takeaway:**
> Learn how to **represent data → manipulate matrices → work with DataFrames → visualize relationships → understand eigenvectors → calculate covariance and correlation → perform PCA → move into advanced multivariate statistics and machine learning.**
