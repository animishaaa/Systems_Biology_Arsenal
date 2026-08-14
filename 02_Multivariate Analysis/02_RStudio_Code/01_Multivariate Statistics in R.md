# 📊 Multivariate Statistics in R  
## Complete Notes: Matrices, Eigenvectors, Data Frames & Plotting

This introduces the basic **R programming and linear algebra tools** needed for multivariate statistics.

Before studying advanced techniques such as **Principal Component Analysis (PCA)**, clustering, classification, and other multivariate methods, it is important to understand:

1. 🔢 Matrices and matrix operations
2. ⭐ Eigenvectors and eigenvalues
3. 📋 Data frames in R
4. 🎲 Generating random data
5. 📈 Graphical visualization of multivariate data

> 💡 **Important:** The examples are designed for learning and demonstration. They should not be interpreted as real biological conclusions.

---

# 1. 📚 About This 

Multivariate statistics often involves datasets with many variables measured for each observation.

For example, biological data may contain:

- 🧬 Gene expression
- ⚖️ Weight
- 📏 Height
- 🌡️ Temperature
- 🩸 Blood pressure
- 🧪 Biomarker concentrations

To analyze such data effectively in R, we first need a solid understanding of basic **matrix operations, data structures, and visualization**.

---

# 2. 📦 Installing and Loading Packages in R

R contains many built-in functions, but additional functionality is provided through **packages**.

## 📥 Installing a Package

A package normally needs to be installed only once.

```r
install.packages("PACKAGE_NAME")
```

For example:

```r
install.packages("dplyr")
```

---

## 📚 Loading a Package

Once installed, load the package into the current R session using:

```r
library(PACKAGE_NAME)
```

Example:

```r
library(dplyr)
```

> 📌 You normally install a package once, but you need to load it again when starting a new R session.

---

## ⚠️ Common Package Messages

If R displays:

```text
there is no package called 'dplyr'
```

install the package first:

```r
install.packages("dplyr")
```

Then load it:

```r
library(dplyr)
```

A warning that a package was built under a slightly different R version is often harmless if the package still loads and works correctly.

---

# 3. 🧹 Introduction to `dplyr`

`dplyr` is an R package commonly used for:

- 🧹 Cleaning data
- 🔄 Transforming data
- 📊 Summarizing data
- 🔍 Filtering observations
- 📋 Selecting variables

The most important functions to remember are:

| Function | Meaning | 🧠 Think |
|---|---|---|
| `filter()` | Choose rows | 🔍 Which observations? |
| `select()` | Choose columns | 📋 Which variables? |
| `mutate()` | Create or modify columns | ➕ Make a variable |
| `arrange()` | Sort rows | ↕️ Order the data |
| `summarise()` | Calculate summaries | 🧮 Mean, median, etc. |
| `group_by()` | Divide observations into groups | 👥 Analyze groups separately |

### 📌 Example

```r
library(dplyr)

filter(iris, Species == "setosa")
```

This selects only observations belonging to *Iris setosa*.

---

# 4. 🔢 Matrices and Matrix Operations

## What Is a Matrix?

A **matrix** is a rectangular arrangement of numbers organized into:

- ➡️ Rows
- ⬇️ Columns

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

---

# 5. 💻 Creating a Matrix in R

A matrix is created using:

```r
matrix()
```

Example:

```r
A = matrix(c(3,5,1,3,0,8), nrow=2, ncol=3)
```

A shorter version is:

```r
A = matrix(c(3,5,1,3,0,8), 2, 3)
```

R fills matrices **column-wise by default**.

Therefore:

```r
A = matrix(c(3,5,1,3,0,8), 2, 3)
```

produces:

```math
A =
\begin{bmatrix}
3 & 1 & 0 \\
5 & 3 & 8
\end{bmatrix}
```

> 📌 **Important:** R fills matrix elements down each column unless `byrow=TRUE` is specified.

---

## ↔️ Filling a Matrix by Rows

Use:

```r
byrow=TRUE
```

Example:

```r
A = matrix(c(3,1,0,2,4,3), 3, 2, byrow=TRUE)
```

This gives:

```math
A =
\begin{bmatrix}
3 & 1 \\
0 & 2 \\
4 & 3
\end{bmatrix}
```

---

# 6. 🔍 Extracting Elements from a Matrix

Consider:

```r
A = matrix(
  c(67,77,89,170,173,179,120,123,130),
  3,
  3
)
```

Because R fills column-wise:

```math
A =
\begin{bmatrix}
67 & 170 & 120 \\
77 & 173 & 123 \\
89 & 179 & 130
\end{bmatrix}
```

Matrix indexing follows:

```text
A[row, column]
```

---

## 🔹 Extract a Single Element

```r
A[1,3]
```

means:

```text
Row 1, Column 3
```

Result:

```text
120
```

Similarly:

```r
A[3,2]
```

returns:

```text
179
```

---

## ➡️ Extract an Entire Row

```r
A[1,]
```

returns the first row.

---

## ⬇️ Extract an Entire Column

```r
A[,2]
```

returns the second column.

---

## 🔢 Extract Several Columns

```r
A[1,1:3]
```

returns columns 1 through 3 from row 1.

To select only specific columns:

```r
A[1,c(1,3)]
```

This returns columns 1 and 3 from row 1.

---

## 🧩 Extracting a Sub-Matrix

```r
G = A[,2:3]
```

This extracts columns 2 and 3.

Therefore:

```math
G =
\begin{bmatrix}
170 & 120 \\
173 & 123 \\
179 & 130
\end{bmatrix}
```

---

# 7. 🏹 Vectors in R

Vectors may be represented as column or row matrices.

## ⬇️ Column Vector

```r
v = matrix(c(2,3,5,1), 4, 1)
```

This produces:

```math
v =
\begin{bmatrix}
2 \\
3 \\
5 \\
1
\end{bmatrix}
```

---

## ➡️ Row Vector

```r
v = matrix(c(2,3,5,1), 1, 4)
```

This produces:

```math
v =
\begin{bmatrix}
2 & 3 & 5 & 1
\end{bmatrix}
```

---

# 8. 0️⃣ Zero Matrix and Identity Matrix

## Zero Matrix

A **zero matrix** contains only zeros.

```r
A = matrix(0, 3, 3)
```

This gives:

```math
A =
\begin{bmatrix}
0 & 0 & 0 \\
0 & 0 & 0 \\
0 & 0 & 0
\end{bmatrix}
```

---

## 🔳 Identity Matrix

An **identity matrix** has ones along the main diagonal and zeros elsewhere.

In R:

```r
diag(3)
```

produces:

```math
I =
\begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
```

The identity matrix behaves like the number **1** in ordinary multiplication.

```math
AI = IA = A
```

---

# 9. 🔄 Transpose of a Matrix

The **transpose** exchanges the rows and columns of a matrix.

Suppose:

```r
A = matrix(c(1,2,3,4,5,6), 2, 3)
```

Then:

```math
A =
\begin{bmatrix}
1 & 3 & 5 \\
2 & 4 & 6
\end{bmatrix}
```

Calculate the transpose:

```r
t(A)
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

Thus:

```math
A_{m\times n}
\quad\longrightarrow\quad
A^T_{n\times m}
```

---

# 10. 🪞 Symmetric Matrices

A matrix is **symmetric** if:

```math
A=A^T
```

For example:

```math
A =
\begin{bmatrix}
2 & 1 \\
1 & 3
\end{bmatrix}
```

is symmetric because:

```math
A^T =
\begin{bmatrix}
2 & 1 \\
1 & 3
\end{bmatrix}
=A
```

---

## 🔍 Checking Symmetry in R

You can compare manually:

```r
A == t(A)
```

Or use:

```r
isSymmetric(A)
```

> 💡 Symmetric matrices are extremely important in multivariate statistics because **covariance and correlation matrices are symmetric**.

---

# 11. ➕ Matrix Addition and Subtraction

Suppose:

```r
A = matrix(c(1,3,2,4), 2, 2)
B = matrix(2, 2, 2)
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

```r
A + B
```

gives:

```math
A+B =
\begin{bmatrix}
3 & 4 \\
5 & 6
\end{bmatrix}
```

Subtraction:

```r
A - B
```

gives:

```math
A-B =
\begin{bmatrix}
-1 & 0 \\
1 & 2
\end{bmatrix}
```

> 📌 Matrices must have compatible dimensions for element-wise addition and subtraction.

---

# 12. ✖️ Matrix Multiplication

## 🔢 Scalar Multiplication

Multiply every element of the matrix by a scalar:

```r
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

## 🏹 Matrix × Vector

Suppose:

```r
A = matrix(c(1,3,2,4), 2, 2)
v = matrix(c(3,4), 2, 1)
```

Therefore:

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

```r
A %*% v
```

The calculation is:

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

which gives:

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

## ⚠️ `%*%` vs `*`

For matrix multiplication use:

```r
A %*% v
```

Do **not** confuse this with:

```r
A * v
```

because `*` performs **element-wise multiplication**, while `%*%` performs **matrix multiplication**.

---

# 13. 🔁 Order Matters in Matrix Multiplication

In general:

```math
AB \neq BA
```

In R:

```r
A %*% B
B %*% A
```

may produce different results.

> 🧠 Matrix multiplication is generally **not commutative**.

---

## 🔳 Identity Matrix Property

Suppose:

```r
I = diag(2)
```

Then:

```r
I %*% v
```

returns $v$.

Mathematically:

```math
Iv=v
```

---

# 14. 📐 Matrix Dimension Compatibility

Suppose:

```math
A_{m\times n}
```

and:

```math
B_{n\times p}
```

Then multiplication is possible:

```math
AB
```

and the result has dimensions:

```math
AB_{m\times p}
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
2\times4
```

---

# 15. 📝 Exercise 1.1 – Matrices

Important skills to practice include:

- 🔍 Column extraction
- 🧩 Sub-matrix extraction
- 🔄 Identity matrix transpose
- 🪞 Symmetry checking
- ➖ Matrix subtraction
- ✖️ Matrix-vector multiplication
- 📐 Dimension compatibility

---

# 16. 🔢 Matrices and Matrix Operations

## 🧮 Determinant

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

### R Example

```r
A = matrix(c(3,2,2,4), 2, 2)
det(A)
```

Because R fills column-wise:

```math
A =
\begin{bmatrix}
3 & 2 \\
2 & 4
\end{bmatrix}
```

Therefore:

```math
\det(A)
=
(3)(4)-(2)(2)
=
12-4
=
8
```

---

## 🔢 3 × 3 Determinant

```r
A = matrix(c(1,4,3,2,5,2,3,5,3), 3, 3)

det(A)
```

R calculates the determinant automatically.

---

# 17. 🔁 Inverse of a Matrix

For a matrix $A$, its inverse is written:

```math
A^{-1}
```

The inverse satisfies:

```math
AA^{-1}=I
```

and:

```math
A^{-1}A=I
```

In R:

```r
A = matrix(c(3,4,1,2), 2, 2)

solve(A)
```

---

## ❌ Singular Matrix

Consider:

```r
B = matrix(c(3,3,2,2), 2, 2)
```

This gives:

```math
B =
\begin{bmatrix}
3 & 2 \\
3 & 2
\end{bmatrix}
```

Its rows are linearly dependent, and:

```math
\det(B)=0
```

Therefore, $B$ is **singular** and has no inverse.

Trying:

```r
solve(B)
```

will produce an error.

> 📌 A square matrix is invertible only when its determinant is non-zero.

---

## ✅ Identity Check

To check an inverse:

```r
A %*% solve(A)
```

The result should be approximately:

```math
I =
\begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
```

Small numerical rounding errors may sometimes appear in computer calculations.

---

# 18. 🧩 Solving Linear Equations

Consider the system:

```math
3a+b=4
```

```math
4a+2b=6
```

This can be expressed as:

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

In R:

```r
A = matrix(c(3,4,1,2), 2, 2)
B = matrix(c(4,6), 2, 1)

solve(A, B)
```

The solution is:

```math
\begin{bmatrix}
a \\
b
\end{bmatrix}
=
\begin{bmatrix}
1 \\
1
\end{bmatrix}
```

because:

```math
3(1)+1=4
```

and:

```math
4(1)+2(1)=6
```

---

# 19. ⭐ Eigenvectors and Eigenvalues

The fundamental eigenvector equation is:

```math
Av=\lambda v
```

where:

- $A$ = matrix
- $v$ = eigenvector
- $\lambda$ = eigenvalue

An eigenvector is a special vector whose **direction remains on the same line** after transformation by $A$.

The eigenvalue describes how much the eigenvector is scaled.

---

# 20. 🏹 Drawing a Vector in R

Define:

```r
v = c(3,3)
origin = c(0,0)
```

Create an empty plot:

```r
plot(
  NULL,
  NULL,
  xlim=c(0,5),
  ylim=c(0,5)
)
```

Add a grid:

```r
grid()
```

Draw the vector:

```r
arrows(
  origin[1],
  origin[2],
  v[1],
  v[2],
  length=0.15
)
```

This draws an arrow from:

```math
(0,0)
```

to:

```math
(3,3)
```

---

# 21. 📏 Calculating Vector Length

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

In R:

```r
sqrt(sum(v^2))
```

For:

```r
v = c(3,3)
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

# 22. 🔍 Checking an Eigenvector Visually

Consider:

```r
A = matrix(c(1,1,2,0), 2, 2)
v = c(2,1)
```

Because R fills matrices column-wise:

```math
A =
\begin{bmatrix}
1 & 2 \\
1 & 0
\end{bmatrix}
```

and:

```math
v =
\begin{bmatrix}
2 \\
1
\end{bmatrix}
```

Calculate:

```r
Av = A %*% v
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

Notice:

```math
Av
=
2
\begin{bmatrix}
2 \\
1
\end{bmatrix}
=
2v
```

Therefore:

```math
\lambda=2
```

and $v$ is an eigenvector.

✅ The transformed vector stays on the same line.

---

# 23. 🔢 Calculating the Eigenvalue from Vector Lengths

If $Av$ and $v$ point in the same direction and the scaling is positive, their lengths can be compared:

```r
sqrt(sum(Av^2)) / sqrt(sum(v^2))
```

For this example:

```math
\frac{\|Av\|}{\|v\|}
=
2
```

Therefore:

```math
\lambda=2
```

> ⚠️ The ratio of lengths gives the **magnitude** $|\lambda|$. If the eigenvalue is negative, the transformed vector points in the opposite orientation, so the sign must be determined separately.

---

# 24. 📏 Normalizing an Eigenvector

To normalize a vector:

```r
v / sqrt(sum(v^2))
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

Normalization is especially important in **PCA**.

---

# 25. 💻 Eigenvalues and Eigenvectors in R

R can calculate eigenvalues and eigenvectors automatically using:

```r
eigen(A)
```

For example:

```r
A = matrix(c(1,1,2,0), 2, 2)

eigen(A)
```

The returned object contains:

```text
$values
$vectors
```

To store the result:

```r
Eig = eigen(A)
```

Access eigenvalues:

```r
Eig$values
```

Access eigenvectors:

```r
Eig$vectors
```

> 📌 Eigenvectors are stored as **columns** of `Eig$vectors`.

Therefore:

```r
Eig$vectors[,1]
```

is the first eigenvector.

---

# 26. 📈 Plotting Eigenvectors

Calculate:

```r
Eig = eigen(A)
```

Create a plotting area:

```r
plot(
  NULL,
  NULL,
  xlim=c(-1,1),
  ylim=c(-1,1),
  xlab="x",
  ylab="y"
)

grid()
```

Plot the first eigenvector:

```r
arrows(
  0,
  0,
  Eig$vectors[1,1],
  Eig$vectors[2,1],
  length=0.15
)
```

Plot the second eigenvector:

```r
arrows(
  0,
  0,
  Eig$vectors[1,2],
  Eig$vectors[2,2],
  length=0.15
)
```

This allows us to visualize the **special directions** associated with the matrix.

---

# 27. 📋 Working with Data Frames

A **data frame** is one of the most important data structures in R.

Each:

- ➡️ Row usually represents an observation
- ⬇️ Column usually represents a variable

Create some variables:

```r
Gender = factor(c("M","F","F","F","M","M","F"))

Weight = c(80,58,65,70,90,100,50)

Height = c(190,171,175,169,182,183,165)

Temp = c(37.5,38.3,37.0,37.9,38.6,40.1,36.7)
```

Combine them:

```r
df = data.frame(
  Gender,
  Weight,
  Height,
  Temp
)
```

The resulting structure is conceptually:

| Gender | Weight | Height | Temp |
|---|---:|---:|---:|
| M | 80 | 190 | 37.5 |
| F | 58 | 171 | 38.3 |
| F | 65 | 175 | 37.0 |
| F | 70 | 169 | 37.9 |
| M | 90 | 182 | 38.6 |
| M | 100 | 183 | 40.1 |
| F | 50 | 165 | 36.7 |

---

# 28. 🔍 Examining Data Frame Structure

Use:

```r
str(df)
```

This displays information such as:

- Number of observations
- Number of variables
- Variable names
- Variable types

For example:

```text
Gender → factor
Weight → numeric
Height → numeric
Temp   → numeric
```

---

# 29. 📋 Converting to a Tibble

A **tibble** is a modern version of an R data frame.

Load:

```r
library(tibble)
```

Convert:

```r
as_tibble(df)
```

Tibbles are commonly used with the **tidyverse**.

---

# 30. 📊 Summarizing a Data Frame

Use:

```r
summary(df)
```

For numeric variables, R provides information such as:

- Minimum
- First quartile
- Median
- Mean
- Third quartile
- Maximum

For categorical variables, it provides category counts.

---

# 31. 🔍 Subsetting Data

Suppose we want only female observations.

Using base R:

```r
subset(df, Gender=="F")
```

Using `dplyr`:

```r
library(dplyr)

filter(df, Gender=="F")
```

Both select rows where:

```text
Gender = F
```

---

# 32. 🔁 Applying Functions to Data

## `lapply()`

Calculate the mean of numeric columns:

```r
lapply(df[,2:4], mean)
```

This applies:

```r
mean()
```

to:

```text
Weight
Height
Temp
```

---

## 👥 `tapply()`

Calculate mean weight separately by gender:

```r
tapply(df$Weight, df$Gender, mean)
```

Conceptually:

```text
Gender
  ↓
 ┌───────┬───────┐
 F       M
 ↓       ↓
Mean    Mean
Weight  Weight
```

---

## 📊 `aggregate()`

Calculate group means:

```r
aggregate(. ~ Gender, df, FUN=mean)
```

This calculates the mean of each numeric variable separately for each gender.

---

# 33. 🛠️ Creating Custom Functions

You can create your own function in R.

Example: calculate the area of a circle.

```r
CircleArea = function(r){
  area = r^2 * pi
  return(area)
}
```

Use:

```r
CircleArea(5)
```

The mathematical formula is:

```math
A=\pi r^2
```

---

# 34. 📏 Creating a Normalization Function

Define:

```r
normalize = function(x){
  x / max(x)
}
```

This divides every observation by the maximum value.

Apply it to numeric columns:

```r
data.frame(
  lapply(df[,2:4], normalize)
)
```

For a value $x_i$:

```math
x_i^{*}
=
\frac{x_i}{\max(x)}
```

> 📌 This is **max normalization**. It is different from z-score standardization.

---

# 35. 🎲 Generating Random Data

R can generate random values from statistical distributions.

## 🔔 Normal Distribution

```r
rnorm(4, 0, 1)
```

means:

```text
Generate 4 random observations
Mean = 0
Standard deviation = 1
```

General syntax:

```r
rnorm(n, mean, sd)
```

---

# 36. 🌱 Setting a Random Seed

Random simulations normally produce different values every time.

Use:

```r
set.seed(12)
```

to make the generated values reproducible.

Example:

```r
set.seed(12)

rnorm(4,0,1)
```

Running the same code with the same seed produces the same pseudo-random sequence.

> 💡 Reproducibility is extremely important in scientific data analysis.

---

# 37. 👥 Simulating Population Data

Suppose we want to simulate 40 heights with:

```text
Mean = 175
Standard deviation = 7
```

Use:

```r
set.seed(12)

sim_data = rnorm(40, 175, 7)
```

Plot the distribution:

```r
hist(sim_data)
```

Calculate the sample mean:

```r
mean(sim_data)
```

Conceptually:

```math
X \sim N(175,7^2)
```

---

# 38. 🎲 Uniform Distribution

Use:

```r
runif(100000)
```

By default, this generates observations from:

```math
U(0,1)
```

General syntax:

```r
runif(n, min, max)
```

For example:

```r
runif(100, 5, 10)
```

generates 100 random numbers between 5 and 10.

---

# 39. 📚 Built-In Data Sets

R contains several useful datasets for learning statistical methods.

---

## 🌸 Iris Dataset

View the first observations:

```r
head(iris)
```

The variables include:

- Sepal length
- Sepal width
- Petal length
- Petal width
- Species

Calculate species-specific means:

```r
aggregate(. ~ Species, iris, mean)
```

This gives the mean of every numerical measurement for each species.

---

# 40. 🦀 Crab Data

The `crabs` dataset is available through the `MASS` package.

Load:

```r
library(MASS)
```

View:

```r
head(crabs)
```

The dataset contains morphological measurements from crabs and provides another example of **multivariate biological data**.

---

# 41. 📈 Graphical Illustration of Multivariate Data

Visualization should normally be an early step in statistical analysis.

Plots can reveal:

- 🔗 Relationships
- 👥 Groups
- 📈 Trends
- ⚠️ Outliers
- 🧩 Clusters
- 📊 Differences between variables

---

# 42. 🔵 Scatter Plot

Using the Iris dataset:

```r
plot(
  iris$Petal.Width,
  iris$Petal.Length
)
```

A clearer version is:

```r
plot(
  iris$Petal.Width,
  iris$Petal.Length,
  xlab="Petal Width",
  ylab="Petal Length"
)
```

Each point represents one flower.

The plot helps examine the relationship between:

```text
Petal Width ↔ Petal Length
```

---

# 43. 🎨 Colored Scatter Plot

Color observations by species:

```r
plot(
  iris$Petal.Width,
  iris$Petal.Length,
  col=iris$Species,
  xlab="Petal Width",
  ylab="Petal Length"
)
```

This can reveal **species-specific clustering**.

For example:

- 🌷 Setosa forms a clear cluster
- 🌺 Versicolor forms another cluster
- 🌸 Virginica forms another cluster

---

# 44. 🖼️ Multiple Plots

Use:

```r
par(mfrow=c(1,2))
```

This divides the plotting window into:

```text
1 row
2 columns
```

Conceptually:

```text
┌──────────────┬──────────────┐
│    Plot 1    │    Plot 2    │
└──────────────┴──────────────┘
```

Reset later using:

```r
par(mfrow=c(1,1))
```

---

# 45. 📦 Boxplots + Jittered Points

Create a boxplot:

```r
boxplot(
  Petal.Length ~ Species,
  data=iris
)
```

Add individual observations:

```r
points(
  jitter(as.numeric(iris$Species)),
  iris$Petal.Length
)
```

The boxplot summarizes the distributions, while jittered points show the individual observations.

---

# 46. 📍 Stripcharts

A stripchart displays individual observations directly.

```r
stripchart(
  Petal.Length ~ Species,
  data=iris,
  vertical=TRUE,
  method="jitter"
)
```

The `jitter` option slightly separates overlapping observations.

This helps us see:

- Sample density
- Variation
- Outliers
- Differences between groups

---

# 47. 📉 Profile Plot

The `GGally` package can be used to create parallel-coordinate/profile plots.

Load:

```r
library(GGally)
```

Then:

```r
ggparcoord(
  iris,
  columns=1:4,
  groupColumn=5,
  scale="globalminmax"
)
```

This visualizes several variables simultaneously.

Each line corresponds to an observation.

The axes correspond to:

```text
Sepal.Length
Sepal.Width
Petal.Length
Petal.Width
```

The plot can reveal multivariate patterns across species.

---

# 48. 🔢 Scatter Plot Matrix

A scatterplot matrix allows us to examine pairwise relationships between several variables simultaneously.

```r
pairs(
  iris[,1:4],
  col=iris$Species,
  upper.panel=NULL
)
```

This compares:

```text
Sepal Length
Sepal Width
Petal Length
Petal Width
```

with one another.

It can reveal:

- 🔗 Correlations
- 🌸 Species separation
- 🧩 Clusters
- ⚠️ Outliers
- 📈 Linear relationships

> 💡 A scatterplot matrix is one of the most useful exploratory tools for multivariate data.

---

# 49. 🧠 Important R Operators to Remember

| Operator / Function | Meaning |
|---|---|
| `*` | Element-wise multiplication |
| `%*%` | Matrix multiplication |
| `t(A)` | Matrix transpose |
| `det(A)` | Determinant |
| `solve(A)` | Matrix inverse |
| `solve(A,b)` | Solve linear system |
| `diag(n)` | Identity matrix |
| `eigen(A)` | Eigenvalues and eigenvectors |
| `A[i,j]` | Matrix element |
| `A[i,]` | Entire row |
| `A[,j]` | Entire column |

---

# 50. 🎯 Matrix Operations – Quick Summary

```text
Create matrix
     ↓
matrix()

Extract element
     ↓
A[row, column]

Transpose
     ↓
t(A)

Symmetry
     ↓
isSymmetric(A)

Determinant
     ↓
det(A)

Inverse
     ↓
solve(A)

Matrix multiplication
     ↓
A %*% B

Eigenvalues / eigenvectors
     ↓
eigen(A)
```

---

# 51. 🧠 Data Frame Operations – Quick Summary

```text
Create
  ↓
data.frame()

Inspect
  ↓
str()

Summarize
  ↓
summary()

Filter
  ↓
subset()
or
filter()

Group summaries
  ↓
tapply()
aggregate()

Apply a function
  ↓
lapply()
```

---

# 52. 🚀 From Matrices to Multivariate Statistics

The concepts in this tutorial connect directly to more advanced methods.

```text
Matrices
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
Multivariate Analysis
```

At the same time:

```text
Data Frames
    ↓
Data Cleaning
    ↓
Exploration
    ↓
Visualization
    ↓
Statistical Modeling
```

---

# 53. 🧬 Why This Matters in Biological Data Analysis

Biological datasets often contain many measurements for every sample.

For example:

```text
Patient
   ↓
┌──────────────────────────┐
│ Gene Expression          │
│ Protein Concentration    │
│ Age                      │
│ Weight                   │
│ Biomarkers               │
│ Treatment Response       │
└──────────────────────────┘
```

This naturally produces **multivariate data**.

Matrices provide the mathematical representation of such datasets, while data frames provide a convenient R structure for working with them.

---

# 54. 🔑 Key Takeaways

| Concept | 💡 Key Point |
|---|---|
| 🔢 **Matrix** | Rectangular arrangement of numbers |
| ➡️ **Rows** | Usually observations |
| ⬇️ **Columns** | Usually variables |
| `%*%` | Matrix multiplication |
| `*` | Element-wise multiplication |
| 🔄 **Transpose** | Exchanges rows and columns |
| 🪞 **Symmetric matrix** | $A=A^T$ |
| 🧮 **Determinant** | Helps determine whether a matrix is invertible |
| 🔁 **Inverse** | Satisfies $AA^{-1}=I$ |
| ⭐ **Eigenvector** | Direction preserved by matrix transformation |
| 🔢 **Eigenvalue** | Scaling associated with an eigenvector |
| 📋 **Data frame** | Major R structure for datasets |
| 🎲 **Random data** | Useful for simulation and learning |
| 🌱 **Seed** | Makes simulation reproducible |
| 📈 **Visualization** | Helps explore patterns before modeling |
| 📊 **PCA** | Uses matrix algebra, eigenvalues, and eigenvectors |

---

# 55. 🎯 Final Summary

The foundations of multivariate statistics in R can be summarized as:

```text
                 MULTIVARIATE STATISTICS
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
       MATRICES        DATA FRAMES      VISUALIZATION
          │                │                │
          ▼                ▼                ▼
   Matrix Operations   Data Handling    Explore Patterns
          │
          ▼
 Eigenvalues + Eigenvectors
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

- 🔢 **Matrices are the mathematical foundation of multivariate statistics.**
- ⭐ **Eigenvalues and eigenvectors are fundamental to PCA and many other multivariate techniques.**
- 📋 **Data frames are central to practical data analysis in R.**
- 🎲 **Random-number generation allows us to simulate and understand statistical behavior.**
- 📈 **Visualization should be an important early step before fitting complex statistical models.**
- 🧬 Together, these concepts provide the foundation for analyzing complex biological and high-dimensional datasets.

> 🚀 **Final takeaway:**  
> Learn how to **represent data → manipulate matrices → explore data frames → visualize relationships → understand eigenvectors → move into PCA and advanced multivariate statistics.**
