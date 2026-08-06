# 🔢 NumPy Arrays

> **Scientific Computing with Python**

NumPy (**Numerical Python**) is the fundamental library for numerical computing in Python.

It provides the **NumPy array**, which is the equivalent of an **R vector**, but with greater speed and efficiency for numerical operations.

Almost every scientific library in Python depends on NumPy.

---

# 📚 Table of Contents

1. What is NumPy?
2. Why Use NumPy?
3. Installing NumPy
4. Importing NumPy
5. Creating Arrays
6. Array Properties
7. Indexing
8. Slicing
9. Mathematical Operations
10. Statistical Functions
11. Random Numbers
12. Array Reshaping
13. Comparison with R Vectors
14. Biological Examples
15. Key Takeaways

---

# 📖 What is NumPy?

NumPy is a Python library designed for:

- 🔢 Numerical computing
- 📊 Statistical analysis
- 📈 Matrix operations
- 🧮 Linear algebra
- 🎲 Random number generation

The core object in NumPy is the **ndarray (N-dimensional array)**.

---

# 🚀 Why Use NumPy?

Compared with Python lists, NumPy arrays are:

- ⚡ Faster
- 💾 More memory efficient
- ➕ Support vectorized mathematics
- 📊 Ideal for statistics
- 🤖 Used by almost every scientific package

---

# 📦 Installing NumPy

```bash
pip install numpy
```

Most Anaconda installations already include NumPy.

---

# 📥 Importing NumPy

```python
import numpy as np
```

Using the alias `np` is the standard convention.

---

# 🔢 Creating Arrays

Create an array from a list.

```python
import numpy as np

bp = np.array([142, 145, 139, 141])
```

Display the array.

```python
print(bp)
```

Output

```text
[142 145 139 141]
```

---

# 📏 Array Properties

## Number of Elements

```python
len(bp)
```

Output

```text
4
```

---

## Shape

```python
bp.shape
```

Output

```text
(4,)
```

---

## Data Type

```python
bp.dtype
```

Output

```text
dtype('int64')
```

(Data type may differ depending on the operating system.)

---

# 🔍 Indexing

NumPy uses **zero-based indexing**.

| Index | Value |
|-------|------|
| 0 | 142 |
| 1 | 145 |
| 2 | 139 |
| 3 | 141 |

First value

```python
bp[0]
```

Output

```text
142
```

---

Last value

```python
bp[-1]
```

Output

```text
141
```

---

# ✂️ Slicing

First three values

```python
bp[0:3]
```

Output

```text
[142 145 139]
```

---

Last two values

```python
bp[2:]
```

Output

```text
[139 141]
```

---

# ➕ Mathematical Operations

Addition

```python
bp + 10
```

Output

```text
[152 155 149 151]
```

---

Multiplication

```python
bp * 2
```

Output

```text
[284 290 278 282]
```

---

Division

```python
bp / 2
```

Output

```text
[71.0 72.5 69.5 70.5]
```

---

Power

```python
bp ** 2
```

---

# 📊 Statistical Functions

Mean

```python
np.mean(bp)
```

Equivalent in R

```r
mean(bp)
```

---

Median

```python
np.median(bp)
```

Equivalent in R

```r
median(bp)
```

---

Maximum

```python
np.max(bp)
```

Equivalent in R

```r
max(bp)
```

---

Minimum

```python
np.min(bp)
```

Equivalent in R

```r
min(bp)
```

---

Sum

```python
np.sum(bp)
```

Equivalent in R

```r
sum(bp)
```

---

Standard Deviation

```python
np.std(bp, ddof=1)
```

Equivalent in R

```r
sd(bp)
```

> **Note:** `ddof=1` calculates the **sample standard deviation**, matching R's `sd()` function.

---

Variance

```python
np.var(bp, ddof=1)
```

Equivalent in R

```r
var(bp)
```

---

# 🎲 Random Numbers

Random integers

```python
np.random.randint(
    0,
    100,
    size=10
)
```

---

Random decimal numbers

```python
np.random.rand(5)
```

---

Normally distributed numbers

```python
np.random.normal(
    loc=100,
    scale=15,
    size=20
)
```

Where:

- `loc` = mean
- `scale` = standard deviation
- `size` = sample size

---

# 📐 Array Reshaping

Create a matrix.

```python
matrix = np.array([
    [1, 2],
    [3, 4]
])
```

Shape

```python
matrix.shape
```

Output

```text
(2, 2)
```

---

Reshape

```python
bp.reshape(2, 2)
```

Output

```text
[[142 145]
 [139 141]]
```

---

# ⚖️ NumPy vs R Vectors

| Feature | NumPy | R |
|----------|--------|----|
| Vector | `np.array()` | `c()` |
| Mean | `np.mean()` | `mean()` |
| Median | `np.median()` | `median()` |
| SD | `np.std(ddof=1)` | `sd()` |
| Variance | `np.var(ddof=1)` | `var()` |
| Maximum | `np.max()` | `max()` |
| Minimum | `np.min()` | `min()` |

---

# 🧬 Biological Example

Blood pressure measurements

```python
bp = np.array([
    142,
    144,
    140,
    138,
    145,
    141
])

np.mean(bp)
np.std(bp, ddof=1)
```

---

Gene expression values

```python
expression = np.array([
    3.2,
    4.1,
    2.8,
    5.0,
    4.3
])

np.mean(expression)
np.max(expression)
```

---

Protein concentrations

```python
protein = np.array([
    1.8,
    2.4,
    2.1,
    2.7,
    2.3
])

np.median(protein)
```

---

# 💡 Tips

- ⚡ NumPy arrays are significantly faster than Python lists.
- 📊 NumPy is the standard library for scientific computing.
- 📈 Statistical functions are available through `numpy`.
- 🔢 Arrays support vectorized operations without loops.
- 🧮 Most statistical packages accept NumPy arrays directly.

---

# 🎯 Key Takeaways

- 🔢 NumPy is the foundation of scientific computing in Python.
- 📦 The NumPy array is the closest equivalent to an R vector.
- ⚡ Arrays provide efficient mathematical and statistical operations.
- 📊 Built-in functions calculate means, medians, variances, and standard deviations.
- 🎲 NumPy includes powerful random number generators for simulations.
- 📐 Arrays can be reshaped into matrices for more advanced analyses.
- 🤖 Nearly all Python statistics and machine learning libraries rely on NumPy arrays.

