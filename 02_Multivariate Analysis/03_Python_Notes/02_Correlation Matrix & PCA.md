# 📊 Multivariate Statistics in Python

## Correlation Matrix & Principal Component Analysis (PCA)

> 🎯 **Goal:** Learn how to explore relationships between multiple variables using covariance and correlation matrices, then use Principal Component Analysis (PCA) in Python to reduce dimensionality while preserving as much information as possible.

---

## 📚 Table of Contents

1. [What This Tutorial Covers](#1--what-this-tutorial-covers)
2. [Python Libraries](#2--python-libraries)
3. [Iris Dataset](#3--iris-dataset)
4. [Correlation Matrix](#4--correlation-matrix)
5. [Spearman Correlation](#5--spearman-correlation)
6. [Correlation Heatmap](#6--correlation-heatmap)
7. [Extracting Strong Correlations](#7--extracting-strong-correlations)
8. [Significance Testing of Correlations](#8--significance-testing-of-correlations)
9. [Covariance Matrix](#9--covariance-matrix)
10. [Why PCA Is Needed](#10--why-pca-is-needed)
11. [Variable Reduction Intuition](#11--variable-reduction-intuition)
12. [PCA Finds the Best Linear Combination](#12--pca-finds-the-best-linear-combination)
13. [PCA Using Eigenvectors Manually](#13--pca-using-eigenvectors-manually)
14. [Computing Principal Component Scores](#14--computing-principal-component-scores)
15. [PCA Using Scikit-Learn](#15--pca-using-scikit-learn)
16. [PCA Visualization](#16--pca-visualization)
17. [When PCA Does Not Reduce Dimensions Well](#17--when-pca-does-not-reduce-dimensions-well)
18. [PCA with Standardization](#18--pca-with-standardization)
19. [Choosing the Number of Components](#19--choosing-the-number-of-components)
20. [Loadings](#20--loadings)
21. [Varimax Rotation](#21--varimax-rotation)
22. [Complete PCA Workflow](#22--complete-pca-workflow)
23. [Key Concepts](#23--key-concepts)
24. [Python Cheat Sheet](#24--python-cheat-sheet)
25. [Key Takeaways](#25--key-takeaways)

---

# 1. 🎯 What This Tutorial Covers

This tutorial introduces two fundamental topics in **multivariate statistics using Python**:

1. 🔗 **Covariance and correlation matrices**
2. 📉 **Principal Component Analysis (PCA)**

These concepts are useful for:

* 🧩 Clustering
* 🤖 Classification
* 📉 Dimensionality reduction
* 📊 Multivariate modeling
* 🧬 Omics analysis
* 🔎 Exploratory data analysis
* 🏭 Process monitoring
* 🎯 Feature engineering

The overall workflow is:

```text
Multiple Variables
       ↓
Correlation / Covariance
       ↓
Understand Relationships
       ↓
Standardization
       ↓
PCA
       ↓
Reduce Dimensions
       ↓
Interpret / Visualize / Model
```

---

# 2. 🐍 Python Libraries

We will mainly use:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

from scipy import stats

from sklearn.datasets import load_iris
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
```

For correlation heatmaps:

```python
import seaborn as sns
```

---

## 📦 What Each Library Does

| Library            | Purpose                           |
| ------------------ | --------------------------------- |
| `numpy`            | Numerical and matrix calculations |
| `pandas`           | Data tables and manipulation      |
| `matplotlib`       | Plotting                          |
| `seaborn`          | Statistical visualization         |
| `scipy.stats`      | Statistical tests                 |
| `sklearn.datasets` | Example datasets                  |
| `StandardScaler`   | Standardization                   |
| `PCA`              | Principal Component Analysis      |

---

# 3. 🌸 Iris Dataset

The Iris dataset is available directly through Scikit-Learn.

---

## Load the Dataset

```python
from sklearn.datasets import load_iris

iris = load_iris()
```

Inspect the object:

```python
iris
```

---

## Convert to a Pandas DataFrame

```python
df = pd.DataFrame(
    iris.data,
    columns=iris.feature_names
)
```

Add the species:

```python
df["species"] = iris.target
```

Inspect:

```python
df.head()
```

Example:

```text
   sepal length (cm)  sepal width (cm)  petal length (cm)  petal width (cm)  species
0                5.1               3.5                1.4               0.2        0
1                4.9               3.0                1.4               0.2        0
2                4.7               3.2                1.3               0.2        0
...
```

---

## 🌸 Species Mapping

Scikit-Learn stores the species as:

```text
0 → setosa
1 → versicolor
2 → virginica
```

Check:

```python
iris.target_names
```

Output:

```text
['setosa' 'versicolor' 'virginica']
```

---

## Add Species Names

For easier interpretation:

```python
df["species_name"] = [
    iris.target_names[i]
    for i in iris.target
]
```

Now:

```python
df.head()
```

contains both numeric and categorical information.

---

## Select Only Numeric Measurement Variables

Create:

```python
X = df[iris.feature_names]
```

Now `X` contains:

```text
Sepal Length
Sepal Width
Petal Length
Petal Width
```

These are the variables used for correlation, covariance, and PCA.

---

# 4. 🔗 Correlation Matrix

## What Is Correlation?

Correlation measures the strength and direction of the **linear relationship** between two variables.

The Pearson correlation coefficient satisfies:

$$
-1 \le r \le 1
$$

Interpretation:

```text
r = +1
↓
Perfect positive linear relationship


r ≈ 0
↓
Weak / no linear relationship


r = -1
↓
Perfect negative linear relationship
```

---

## Pearson Correlation Formula

For variables $X$ and $Y$:

$$
r_{XY} = \frac{Cov(X,Y)}{\sigma_X\sigma_Y}
$$

---

## Calculate Pearson Correlations

With Pandas:

```python
cor_mat = X.corr(method="pearson")
```

Display:

```python
cor_mat
```

Approximate result:

```text
                   sepal length  sepal width  petal length  petal width
sepal length           1.0000      -0.1176        0.8718       0.8179
sepal width           -0.1176       1.0000       -0.4284      -0.3661
petal length           0.8718      -0.4284        1.0000       0.9629
petal width            0.8179      -0.3661        0.9629       1.0000
```

---

## 🔎 Interpretation

### Strongest correlation

```text
Petal Length ↔ Petal Width
r ≈ 0.96
```

This is a:

> **Very strong positive relationship**

As petal length increases, petal width tends to increase.

---

### Another strong correlation

```text
Sepal Length ↔ Petal Length
r ≈ 0.87
```

Again:

> **Strong positive correlation**

---

### Weak relationship

```text
Sepal Length ↔ Sepal Width
r ≈ -0.12
```

This indicates a weak overall linear relationship.

---

## 🧠 Why Is the Diagonal Equal to 1?

Every variable is perfectly correlated with itself.

Therefore:

$$
r_{XX}=1
$$

The diagonal of every valid correlation matrix therefore contains:

```text
1
1
1
1
```

---

# Correlation Within One Group

Sometimes correlations across the whole dataset can hide relationships within groups.

For example, calculate correlations only for **versicolor** flowers.

```python
versicolor = df[
    df["species_name"] == "versicolor"
]
```

Then:

```python
versicolor[
    iris.feature_names
].corr(method="pearson")
```

Conceptually:

```text
Full Iris Dataset
        ↓
Select Versicolor
        ↓
Select Numeric Variables
        ↓
Calculate Correlation Matrix
```

---

# 5. 🏆 Spearman Correlation

Pearson correlation measures **linear relationships**.

It can be affected by:

* Extreme observations
* Strong non-normality
* Nonlinear relationships

---

## Why Use Spearman?

Spearman correlation uses **ranks** instead of the raw observations.

Calculate:

```python
spearman_mat = X.corr(
    method="spearman"
)
```

For versicolor only:

```python
versicolor[
    iris.feature_names
].corr(method="spearman")
```

---

## Spearman Characteristics

Spearman correlation:

* 🏆 Uses ranks
* 📈 Measures monotonic association
* 🛡️ Is less sensitive to extreme values
* ❌ Does not require a strictly linear relationship

---

## Pearson vs Spearman

| Pearson                                       | Spearman                            |
| --------------------------------------------- | ----------------------------------- |
| Uses raw values                               | Uses ranks                          |
| Measures linear association                   | Measures monotonic association      |
| More sensitive to outliers                    | More robust to outliers             |
| Common for approximately linear relationships | Useful for ranked or monotonic data |

---

# 6. 🎨 Correlation Heatmap

Large correlation matrices can be difficult to read.

A heatmap provides a visual summary.

---

## Calculate Correlation Matrix

```python
cor_mat = X.corr(
    method="pearson"
)
```

---

## Plot with Seaborn

```python
plt.figure(figsize=(8, 6))

sns.heatmap(
    cor_mat,
    annot=True,
    cmap="coolwarm",
    vmin=-1,
    vmax=1
)

plt.title("Iris Correlation Matrix")
plt.show()
```

---

## 🔎 Interpretation

Conceptually:

```text
Positive values
     ↓
Positive relationship


Negative values
     ↓
Negative relationship


|r| close to 1
     ↓
Strong relationship


r close to 0
     ↓
Weak relationship
```

The diagonal contains:

```text
1.0
```

because each variable is perfectly correlated with itself.

---

# 7. 🔥 Extracting Strong Correlations

Suppose we want only correlations satisfying:

$$
|r| > 0.80
$$

---

## Step 1️⃣ — Calculate Correlation Matrix

```python
cor_mat = X.corr()
```

---

## Step 2️⃣ — Remove Duplicate Pairs

Because:

```text
Correlation(A,B)
=
Correlation(B,A)
```

we need only one triangle.

Create a mask:

```python
mask = np.triu(
    np.ones(cor_mat.shape),
    k=1
).astype(bool)
```

Extract the upper triangle:

```python
upper = cor_mat.where(mask)
```

---

## Step 3️⃣ — Convert to Long Format

```python
cor_pairs = (
    upper
    .stack()
    .reset_index()
)
```

Rename columns:

```python
cor_pairs.columns = [
    "Variable_1",
    "Variable_2",
    "Correlation"
]
```

Inspect:

```python
cor_pairs
```

---

## Step 4️⃣ — Extract Strong Correlations

```python
strong_cor = cor_pairs[
    cor_pairs["Correlation"].abs() > 0.80
]
```

Sort:

```python
strong_cor = strong_cor.sort_values(
    "Correlation",
    ascending=False
)
```

Display:

```python
strong_cor
```

Expected strong relationships include approximately:

```text
Petal Length ↔ Petal Width    0.963

Sepal Length ↔ Petal Length   0.872

Sepal Length ↔ Petal Width    0.818
```

---

## 🧠 Why Use `.abs()`?

This:

```python
cor_pairs["Correlation"].abs() > 0.80
```

means:

$$
|r| > 0.80
$$

Therefore it includes both:

```text
Strong positive correlations

AND

Strong negative correlations
```

---

# 8. 🧪 Significance Testing of Correlations

The correlation coefficient tells us the strength of an observed relationship.

We can also test whether the population correlation might plausibly be zero.

---

## Pearson Correlation Test

Using SciPy:

```python
from scipy.stats import pearsonr
```

Test:

```python
r, p_value = pearsonr(
    df["sepal length (cm)"],
    df["sepal width (cm)"]
)
```

Display:

```python
r
```

```python
p_value
```

Approximate result:

```text
r ≈ -0.118
p ≈ 0.152
```

Therefore:

> ❌ Sepal Length vs Sepal Width is not statistically significant at the conventional 0.05 level.

---

## Hypotheses

Conceptually:

```text
H0:
Population correlation = 0


H1:
Population correlation ≠ 0
```

---

# P-Values for All Correlations

We can calculate all pairwise Pearson tests manually.

```python
from itertools import combinations
from scipy.stats import pearsonr

results = []

for var1, var2 in combinations(
    iris.feature_names,
    2
):
    r, p = pearsonr(
        df[var1],
        df[var2]
    )

    results.append(
        [var1, var2, r, p]
    )
```

Convert to DataFrame:

```python
cor_tests = pd.DataFrame(
    results,
    columns=[
        "Variable_1",
        "Variable_2",
        "Correlation",
        "P_value"
    ]
)
```

Display:

```python
cor_tests
```

---

# Multiple Testing Problem

For four variables, the number of unique pairwise tests is:

$$
\frac{4(4-1)}{2}=6
$$

Therefore:

```text
6 correlation tests
```

are performed.

Testing multiple hypotheses increases the probability of false positives.

---

## Bonferroni Correction

The Bonferroni adjustment is:

$$
p_{adjusted}=p\times m
$$

where:

* $p$ = original p-value
* $m$ = number of tests

Here:

```text
m = 6
```

In Python:

```python
cor_tests["P_Bonferroni"] = (
    cor_tests["P_value"] * 6
)
```

Because a p-value cannot exceed 1:

```python
cor_tests["P_Bonferroni"] = (
    cor_tests["P_Bonferroni"]
    .clip(upper=1)
)
```

Display:

```python
cor_tests
```

---

## Alternative: `multipletests`

A more general approach:

```python
from statsmodels.stats.multitest import multipletests
```

Then:

```python
reject, p_corrected, _, _ = multipletests(
    cor_tests["P_value"],
    method="bonferroni"
)
```

Add:

```python
cor_tests["P_Bonferroni"] = p_corrected
cor_tests["Significant"] = reject
```

---

# 9. 📦 Covariance Matrix

## What Is Covariance?

Covariance measures whether two variables tend to change together.

For variables $X$ and $Y$:

$$
Cov(X,Y) = \frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}{n-1}
$$

Interpretation:

```text
Positive covariance
↓
Variables tend to increase together


Negative covariance
↓
One tends to increase while
the other decreases


Covariance ≈ 0
↓
Weak linear co-movement
```

---

## Calculate Covariance Matrix

With Pandas:

```python
cov_mat = X.cov()
```

Display:

```python
cov_mat
```

Approximate first row:

```text
Sepal Length variance     ≈ 0.686
Cov(Sepal Length, Width)  ≈ -0.042
Cov(Sepal Length, Petal Length) ≈ 1.274
...
```

---

## Diagonal Elements

The diagonal contains:

> **Variances**

For example:

```python
X["sepal length (cm)"].var()
```

corresponds to the first diagonal element.

Mathematically:

$$
Cov(X,X)=Var(X)
$$

---

# Covariance of Standardized Variables

Standardize:

```python
scaler = StandardScaler()
```

Transform:

```python
X_scaled = scaler.fit_transform(X)
```

Convert back to DataFrame:

```python
X_scaled_df = pd.DataFrame(
    X_scaled,
    columns=X.columns
)
```

Now calculate covariance.

Because Pandas uses sample covariance while `StandardScaler` uses population variance when scaling, tiny convention-related differences can appear.

For an exact sample-standardized comparison:

```python
X_standardized = (
    X - X.mean()
) / X.std(ddof=1)
```

Then:

```python
X_standardized.cov()
```

Compare with:

```python
X.corr()
```

They are equivalent up to numerical rounding.

Therefore:

> ⭐ **Covariance of sample-standardized variables = Pearson correlation matrix**

---

# 10. 📉 Why PCA Is Needed

Suppose a dataset contains:

* Many variables
* Strong correlations
* Redundant information
* Difficult-to-visualize dimensions

Then interpretation becomes challenging.

---

## The Problem

```text
X1 ─┐
X2 ─┤
X3 ─┤
X4 ─┤
X5 ─┤
... │
Xp ─┘
```

Many variables may represent overlapping information.

---

## PCA Solution

PCA:

* 🧩 Combines variables
* 📉 Reduces dimensions
* 📊 Preserves as much variance as possible
* 🔗 Creates uncorrelated components

Conceptually:

```text
Many Correlated Variables
          ↓
         PCA
          ↓
Few Principal Components
          ↓
Most Important Variance
     Is Preserved
```

---

# 11. 🩺 Variable Reduction Intuition

Consider:

```python
DBP = np.array([
    78, 80, 81, 82, 84, 86
])

SBP = np.array([
    126, 128, 127, 130, 130, 132
])
```

Plot:

```python
plt.scatter(DBP, SBP)

plt.xlabel("Diastolic BP (mmHg)")
plt.ylabel("Systolic BP (mmHg)")
plt.title("DBP vs SBP")

plt.show()
```

If the two variables are strongly correlated, they contain overlapping information.

---

## Simple Combination

Mean:

```python
BP_mean = (
    DBP + SBP
) / 2
```

Sum:

```python
BP_sum = DBP + SBP
```

Both reduce:

```text
DBP + SBP
    ↓
One new variable
```

But the combination has been chosen manually.

---

## General Linear Combination

A general linear combination is:

$$
PC = \alpha_1X_1 + \alpha_2X_2
$$

For the blood-pressure variables:

$$
PC = \alpha_1DBP + \alpha_2SBP
$$

The question is:

> **What values of $\alpha_1$ and $\alpha_2$ give us the best new variable?**

PCA answers this mathematically.

---

# 12. 🎯 PCA Finds the Best Linear Combination

PCA chooses coefficients that maximize the variance of the new component.

For two variables:

$$
PC_1 = \alpha_1X_1 + \alpha_2X_2
$$

PCA chooses the coefficients so that:

> **Variance of PC1 is maximized**

subject to:

$$
\alpha_1^2 + \alpha_2^2 = 1
$$

---

## Why Do We Need the Constraint?

Without a constraint, we could increase the component variance simply by multiplying the weights by extremely large numbers.

For example:

```text
0.5X + 0.5Y
```

could become:

```text
500X + 500Y
```

which would artificially increase variance.

Therefore PCA requires the eigenvector to have unit length.

---

## Trying Different Weights

Example:

```python
BP = (
    0.8 * DBP +
    0.6 * SBP
)
```

Variance:

```python
np.var(
    BP,
    ddof=1
)
```

Try another:

```python
BP = (
    0.6 * DBP +
    0.8 * SBP
)
```

Then:

```python
np.var(
    BP,
    ddof=1
)
```

Different coefficients produce different amounts of variance.

PCA finds the combination giving:

> 🥇 **Maximum variance**

---

# 13. 🧮 PCA Using Eigenvectors Manually

Combine the variables:

```python
data = np.column_stack(
    (DBP, SBP)
)
```

Inspect:

```python
data
```

---

## Center the Data

```python
data_centered = (
    data - data.mean(axis=0)
)
```

---

## Calculate Covariance Matrix

```python
COV = np.cov(
    data,
    rowvar=False
)
```

Display:

```python
COV
```

---

## Calculate Eigenvalues and Eigenvectors

Because the covariance matrix is symmetric, use:

```python
eigenvalues, eigenvectors = np.linalg.eigh(
    COV
)
```

`eigh()` commonly returns values in ascending order.

Sort them:

```python
indices = np.argsort(
    eigenvalues
)[::-1]
```

Then:

```python
eigenvalues = eigenvalues[indices]

eigenvectors = eigenvectors[:, indices]
```

---

## Inspect Eigenvalues

```python
eigenvalues
```

They tell us:

> **Variance captured by each principal component**

---

## Inspect Eigenvectors

```python
eigenvectors
```

They tell us:

> **Directions / weights of the principal components**

---

## 🧠 Core Relationship

```text
Covariance Matrix
       ↓
Eigen Decomposition
       ↓
┌─────────────────────────┐
│ Eigenvalues             │
│ → Variance              │
│                         │
│ Eigenvectors            │
│ → Directions / Weights  │
└─────────────────────────┘
```

---

## First Principal Component

Extract PC1 weights:

```python
alpha1 = eigenvectors[0, 0]
alpha2 = eigenvectors[1, 0]
```

Then:

```python
PC1 = (
    alpha1 * (DBP - DBP.mean()) +
    alpha2 * (SBP - SBP.mean())
)
```

Calculate:

```python
np.var(
    PC1,
    ddof=1
)
```

This should equal the largest eigenvalue, apart from floating-point rounding.

---

# 14. 📍 Computing Principal Component Scores

A principal-component score tells us where each observation lies along the component axis.

---

## Center the Variables

For DBP:

$$
DBP_{centered}=DBP-\overline{DBP}
$$

For SBP:

$$
SBP_{centered}=SBP-\overline{SBP}
$$

---

## PC1 Scores

```python
PC1 = (
    eigenvectors[0, 0] *
    (DBP - DBP.mean())
    +
    eigenvectors[1, 0] *
    (SBP - SBP.mean())
)
```

---

## PC2 Scores

```python
PC2 = (
    eigenvectors[0, 1] *
    (DBP - DBP.mean())
    +
    eigenvectors[1, 1] *
    (SBP - SBP.mean())
)
```

---

## Matrix Form

The same calculation can be done directly:

```python
scores = (
    data_centered @ eigenvectors
)
```

Then:

```python
PC1 = scores[:, 0]
PC2 = scores[:, 1]
```

Mathematically:

$$
T = ZV
$$

where:

* $Z$ = centered data
* $V$ = eigenvector matrix
* $T$ = score matrix

---

## Plot PC Scores

```python
plt.scatter(
    PC1,
    PC2
)

plt.xlabel("PC1")
plt.ylabel("PC2")
plt.axhline(0)
plt.axvline(0)

plt.show()
```

Usually:

```text
PC1
↓
Large spread


PC2
↓
Small spread
```

Therefore:

> **PC1 contains most of the variation.**

---

# 15. 🤖 PCA Using Scikit-Learn

Manual PCA is useful for understanding the mathematics.

For practical analysis, Scikit-Learn is easier.

---

## Import PCA

```python
from sklearn.decomposition import PCA
```

---

## Run PCA

For the two-variable blood-pressure example:

```python
pca = PCA()
```

Then:

```python
scores = pca.fit_transform(
    data
)
```

---

## Important PCA Attributes

### Component directions

```python
pca.components_
```

These contain the component directions/eigenvectors.

---

### Explained variance

```python
pca.explained_variance_
```

These correspond to the eigenvalues.

---

### Explained variance ratio

```python
pca.explained_variance_ratio_
```

This tells us the proportion of variance explained by each PC.

---

### PC scores

```python
scores
```

or:

```python
pca.transform(data)
```

---

## Example

```python
pca.explained_variance_ratio_
```

may produce approximately:

```text
[0.97, 0.03]
```

Meaning:

```text
PC1 ≈ 97%

PC2 ≈ 3%
```

So one principal component represents most of the information in the two variables.

---

# 16. 🎨 PCA Visualization

Suppose:

```python
scores = pca.fit_transform(
    data
)
```

Extract:

```python
PC1 = scores[:, 0]
PC2 = scores[:, 1]
```

Calculate explained variance:

```python
prop_pca = (
    pca.explained_variance_ratio_
)
```

Plot:

```python
plt.scatter(
    PC1,
    PC2
)

plt.xlabel(
    f"PC1 ({prop_pca[0]:.1%})"
)

plt.ylabel(
    f"PC2 ({prop_pca[1]:.1%})"
)

plt.title(
    "PCA Score Plot"
)

plt.show()
```

---

## Why Include Variance in Axis Labels?

Instead of:

```text
PC1
PC2
```

we see:

```text
PC1 (97%)
PC2 (3%)
```

This immediately tells us how informative each axis is.

---

## Add Observation Labels

```python
plt.scatter(
    PC1,
    PC2
)

for i in range(len(PC1)):
    plt.text(
        PC1[i],
        PC2[i],
        str(i + 1)
    )

plt.xlabel(
    f"PC1 ({prop_pca[0]:.1%})"
)

plt.ylabel(
    f"PC2 ({prop_pca[1]:.1%})"
)

plt.show()
```

---

# 17. ⚠️ When PCA Does Not Reduce Dimensions Well

Consider two variables with little shared structure:

```python
x1 = np.array([
    14.2, 7.7, 11.9, 9.2, 13.4,
    12.4, 10.9, 9.0, 11.4, 7.2
])

x2 = np.array([
    5.6, 10.4, 9.3, 7.2, 11.4,
    5.9, 11.3, 8.0, 6.9, 5.2
])
```

Combine:

```python
data_uncor = np.column_stack(
    (x1, x2)
)
```

Run PCA:

```python
pca_uncor = PCA()

pca_uncor.fit(
    data_uncor
)
```

Check:

```python
pca_uncor.explained_variance_ratio_
```

PC1 may explain only around:

```text
≈ 52%
```

---

## 🧠 Interpretation

If PC1 explains only about 52%:

```text
2 Variables
    ↓
Keep PC1 Only
    ↓
Lose ~48% Variance
```

Therefore PCA cannot efficiently reduce the data from two dimensions to one.

---

## Key Principle

> ⭐ **PCA is particularly effective when variables contain correlated or redundant structure.**

If the variables contain largely independent information, several PCs may be required.

---

# 18. ⚖️ PCA with Standardization

This becomes especially important when there are multiple variables with different scales.

---

## Example Dataset

Suppose:

```python
data = pd.DataFrame({
    "DBP": DBP,
    "SBP": SBP,
    "Weight": Weight,
    "Height": Height
})
```

---

## Standardize

```python
scaler = StandardScaler()
```

Then:

```python
sdata = scaler.fit_transform(
    data
)
```

---

## Run PCA

```python
pca = PCA()

scores = pca.fit_transform(
    sdata
)
```

---

## Explained Variance

```python
pca.explained_variance_ratio_
```

Example:

```text
PC1 ≈ 60%
PC2 ≈ 36%
PC3 ≈  3%
PC4 ≈  1%
```

Therefore:

$$
PC1 + PC2 \approx 96%
$$

Conceptually:

```text
4 Variables
     ↓
Standardization
     ↓
     PCA
     ↓
2 Principal Components
     ↓
≈ 96% Variance Preserved
```

---

# StandardScaler + PCA Pipeline

A clean machine-learning workflow is:

```python
from sklearn.pipeline import Pipeline
```

Create:

```python
pca_pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("pca", PCA())
])
```

Fit:

```python
scores = pca_pipeline.fit_transform(
    data
)
```

This ensures standardization and PCA are applied in sequence.

---

# 19. ✂️ Choosing the Number of Components

Three common approaches are:

1. 📊 Cumulative explained variance
2. 1️⃣ Kaiser criterion
3. 🦵 Scree plot

---

## 1️⃣ Explained Variance

Get:

```python
explained = (
    pca.explained_variance_ratio_
)
```

Cumulative variance:

```python
cumulative = np.cumsum(
    explained
)
```

Display:

```python
cumulative
```

Example:

```text
PC1       → 60%
PC1-PC2   → 96%
PC1-PC3   → 99%
PC1-PC4   → 100%
```

Therefore:

> ✅ PC1 and PC2 are sufficient if 90% or more variance is the chosen target.

---

## 2️⃣ Kaiser Criterion

For standardized PCA:

> Keep components with eigenvalue greater than 1.

Get eigenvalues:

```python
pca.explained_variance_
```

Then:

```python
pca.explained_variance_ > 1
```

Remember:

$$
\lambda > 1
$$

means the PC explains more variance than one average standardized variable.

---

## 3️⃣ Scree Plot

```python
eigenvalues = (
    pca.explained_variance_
)
```

Plot:

```python
plt.plot(
    range(
        1,
        len(eigenvalues) + 1
    ),
    eigenvalues,
    marker="o"
)

plt.xlabel(
    "Principal Component"
)

plt.ylabel(
    "Eigenvalue"
)

plt.title(
    "Scree Plot"
)

plt.show()
```

Look for the:

> 🦵 **Elbow**

If the graph becomes almost flat after PC2:

> ✅ Retain PC1 and PC2.

---

## Cumulative Explained Variance Plot

```python
plt.plot(
    range(
        1,
        len(cumulative) + 1
    ),
    cumulative,
    marker="o"
)

plt.xlabel(
    "Number of Components"
)

plt.ylabel(
    "Cumulative Explained Variance"
)

plt.show()
```

---

# 20. 🧲 Loadings

Loadings help us understand:

> **Which original variables define each principal component?**

---

## PCA Components

Scikit-Learn provides:

```python
pca.components_
```

Shape:

```text
n_components × n_features
```

Each row represents a PC.

---

## Component Weights

Create a table:

```python
weights = pd.DataFrame(
    pca.components_.T,
    index=data.columns,
    columns=[
        f"PC{i+1}"
        for i in range(
            pca.n_components_
        )
    ]
)
```

Display:

```python
weights
```

---

## Loadings as Variable-PC Correlations

For standardized PCA, a common loading definition is:

$$
l_{jk}=v_{jk}\sqrt{\lambda_k}
$$

In Python:

```python
loadings = (
    pca.components_.T *
    np.sqrt(
        pca.explained_variance_
    )
)
```

Convert to DataFrame:

```python
loadings_df = pd.DataFrame(
    loadings,
    index=data.columns,
    columns=[
        f"PC{i+1}"
        for i in range(
            pca.n_components_
        )
    ]
)
```

Display:

```python
loadings_df
```

---

## 🧠 Interpretation

```text
Large |loading|
      ↓
Variable strongly contributes
to / associates with PC


Small |loading|
      ↓
Weak relationship with PC
```

---

## Example Interpretation

Suppose:

```text
             PC1     PC2

DBP         -0.82   -0.55
SBP         -0.77   -0.63
Weight       0.75   -0.64
Height       0.77   -0.61
```

PC1 may approximately represent:

> **Body Size vs Blood Pressure**

while PC2 represents another orthogonal pattern.

---

# 21. 🔄 Varimax Rotation

## Why Rotate?

Unrotated PCs may be mathematically optimal for variance but difficult to interpret.

Several variables may load substantially on multiple components.

This is called:

> **Cross-loading**

---

## Goal of Rotation

Rotation tries to produce:

```text
Variable A
    ↓
High loading on RC1
Low loading on RC2
```

and:

```text
Variable B
    ↓
Low loading on RC1
High loading on RC2
```

This gives a clearer structure.

---

## Varimax

Varimax is an:

> **Orthogonal rotation**

Therefore rotated components remain orthogonal.

---

## Simple Varimax Function

Python's core Scikit-Learn PCA class does not itself provide a Varimax rotation method, but it can be implemented directly.

```python
def varimax(
    Phi,
    gamma=1.0,
    q=100,
    tol=1e-6
):
    p, k = Phi.shape

    R = np.eye(k)

    d = 0

    for i in range(q):

        d_old = d

        Lambda = Phi @ R

        u, s, vh = np.linalg.svd(
            Phi.T @ (
                Lambda ** 3
                -
                (gamma / p)
                * Lambda
                @ np.diag(
                    np.diag(
                        Lambda.T @ Lambda
                    )
                )
            )
        )

        R = u @ vh

        d = np.sum(s)

        if (
            d_old != 0
            and d / d_old < 1 + tol
        ):
            break

    return Phi @ R, R
```

---

## Rotate Two Components

Suppose we retain PC1 and PC2:

```python
first_two_loadings = (
    loadings[:, :2]
)
```

Rotate:

```python
rotated_loadings, rotation_matrix = (
    varimax(
        first_two_loadings
    )
)
```

Convert:

```python
rotated_df = pd.DataFrame(
    rotated_loadings,
    index=data.columns,
    columns=["RC1", "RC2"]
)
```

Display:

```python
rotated_df
```

Possible structure:

```text
            RC1      RC2

DBP        -0.97     0.18
SBP        -0.98     0.10
Weight      0.09    -0.97
Height      0.12    -0.97
```

---

## Interpretation

```text
RC1
 ↓
DBP + SBP
 ↓
Blood Pressure Component
```

```text
RC2
 ↓
Weight + Height
 ↓
Body Size Component
```

---

## 🧠 Important Rotation Point

Rotation does not create additional information.

```text
PC1 + PC2
    ↓
Same retained 2D subspace
    ↓
RC1 + RC2
```

Rotation changes the orientation of the retained axes to improve interpretation.

---

# Rotated Scores

If:

* $T$ = original retained scores
* $R$ = rotation matrix

then:

$$
T_R = TR
$$

In Python:

```python
rotated_scores = (
    scores[:, :2]
    @ rotation_matrix
)
```

---

# 22. 🗺️ Complete PCA Workflow

The complete Python workflow is:

```text
Raw Data
    ↓
Select Numeric Variables
    ↓
Missing-Value Check
    ↓
Correlation Matrix
    ↓
Correlation Heatmap
    ↓
Statistical Testing
    ↓
Covariance Matrix
    ↓
Standardization
    ↓
PCA
    ↓
Eigenvalues
    ↓
Eigenvectors
    ↓
PC Scores
    ↓
Explained Variance
    ↓
Choose Important PCs
    ↓
Loadings
    ↓
Score Plot / Biplot
    ↓
Optional Rotation
    ↓
Clustering / Classification / Modeling
```

---

# 23. 🧠 Key Concepts

## 🔗 Correlation

Answers:

> **How strongly are two variables linearly related?**

$$
-1 \le r \le 1
$$

---

## 📦 Covariance

Answers:

> **Do two variables tend to change together?**

$$
Cov(X,Y) = \frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}{n-1}
$$

---

## ⚖️ Standardization

Transforms:

$$
x \rightarrow z
$$

using:

$$
z = \frac{x-\mu}{\sigma}
$$

After standardization:

```text
Mean ≈ 0
SD   ≈ 1
```

---

## 🧭 Eigenvector

Represents:

> **Direction / weights of a principal component**

---

## 📊 Eigenvalue

Represents:

> **Variance captured by a component**

---

## 🧩 Principal Component

A weighted linear combination:

$$
PC_1 = \alpha_1X_1 + \alpha_2X_2 + \cdots + \alpha_pX_p
$$

---

## 📍 Score

Represents:

> **Position of an observation along a PC**

---

## 🧲 Loading

Represents:

> **Relationship between an original variable and a PC**

---

## 🔄 Rotation

Helps:

> **Make retained component structure easier to interpret**

---

# 24. 💻 Python Cheat Sheet

## Imports

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

from scipy.stats import pearsonr

from sklearn.datasets import load_iris
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
```

---

## Load Iris

```python
iris = load_iris()
```

---

## DataFrame

```python
df = pd.DataFrame(
    iris.data,
    columns=iris.feature_names
)
```

---

## Numeric Variables

```python
X = df[iris.feature_names]
```

---

## Pearson Correlation

```python
X.corr(
    method="pearson"
)
```

---

## Spearman Correlation

```python
X.corr(
    method="spearman"
)
```

---

## Correlation Heatmap

```python
sns.heatmap(
    X.corr(),
    annot=True
)

plt.show()
```

---

## One Pearson Test

```python
r, p = pearsonr(
    X.iloc[:, 0],
    X.iloc[:, 1]
)
```

---

## Covariance Matrix

```python
X.cov()
```

---

## Standardization

```python
scaler = StandardScaler()

X_scaled = scaler.fit_transform(
    X
)
```

---

## PCA

```python
pca = PCA()

scores = pca.fit_transform(
    X_scaled
)
```

---

## Eigenvalues / PC Variances

```python
pca.explained_variance_
```

---

## Explained Variance Ratios

```python
pca.explained_variance_ratio_
```

---

## Cumulative Variance

```python
np.cumsum(
    pca.explained_variance_ratio_
)
```

---

## PCA Directions

```python
pca.components_
```

---

## PCA Scores

```python
scores
```

---

## First Two PC Scores

```python
scores[:, :2]
```

---

## Component Weight Table

```python
pd.DataFrame(
    pca.components_.T,
    index=X.columns
)
```

---

## Loadings

```python
loadings = (
    pca.components_.T
    *
    np.sqrt(
        pca.explained_variance_
    )
)
```

---

## Scree Plot

```python
plt.plot(
    range(
        1,
        len(pca.explained_variance_) + 1
    ),
    pca.explained_variance_,
    marker="o"
)

plt.xlabel("Principal Component")
plt.ylabel("Eigenvalue")

plt.show()
```

---

## PCA Score Plot

```python
plt.scatter(
    scores[:, 0],
    scores[:, 1]
)

plt.xlabel("PC1")
plt.ylabel("PC2")

plt.show()
```

---

# 25. ✅ Key Takeaways

## 🔗 Correlation Matrix

Shows pairwise relationships between variables.

```text
+1 → Strong positive linear relationship

 0 → Weak/no linear relationship

-1 → Strong negative linear relationship
```

---

## 🏆 Pearson vs Spearman

```text
Pearson
   ↓
Linear association
using raw values


Spearman
   ↓
Monotonic association
using ranks
```

---

## 📦 Covariance

Shows whether variables vary together.

For standardized variables:

> **Sample covariance matrix = Pearson correlation matrix**

when the standardization and covariance calculations use consistent sample conventions.

---

## 📉 PCA

PCA transforms correlated variables into fewer principal components.

---

## 🧭 Eigenvectors

> **Directions / weights**

---

## 📊 Eigenvalues

> **Variance captured**

---

## 📍 Scores

> **Positions of observations in PCA space**

---

## 🧲 Loadings

> **Relationships between original variables and PCs**

---

## ⚖️ Standardization

Especially important when variables have:

* Different units
* Different scales
* Very different variances

---

## 🔄 Varimax Rotation

> **Improves interpretability of retained components**

It does not create additional information.

---

# 🧠 R vs Python Mapping

| R              | Python                                   |
| -------------- | ---------------------------------------- |
| `head(iris)`   | `df.head()`                              |
| `cor()`        | `DataFrame.corr()`                       |
| `cov()`        | `DataFrame.cov()`                        |
| `cor.test()`   | `scipy.stats.pearsonr()`                 |
| `scale()`      | `StandardScaler()`                       |
| `eigen()`      | `np.linalg.eigh()`                       |
| `prcomp()`     | `sklearn.decomposition.PCA()`            |
| `pca$sdev^2`   | `pca.explained_variance_`                |
| `pca$rotation` | `pca.components_.T`                      |
| `pca$x`        | `pca.fit_transform()` output             |
| `plot(pca)`    | Matplotlib scree plot                    |
| `varimax()`    | Custom / external Varimax implementation |

---

# 🧠 Final Mental Model

Remember the Python workflow as:

> **Explore → Relate → Standardize → Decompose → Project → Reduce → Interpret**

```text
EXPLORE
   ↓
Pandas DataFrame


RELATE
   ↓
Correlation + Covariance


STANDARDIZE
   ↓
StandardScaler


DECOMPOSE
   ↓
Eigenvalues + Eigenvectors


PROJECT
   ↓
PC Scores


REDUCE
   ↓
Keep Important PCs


INTERPRET
   ↓
Loadings + Plots + Rotation
```

---

# ⭐ One-Line Summary

> **Correlation tells us which variables move together; PCA uses their multivariate variance structure to transform the data into fewer uncorrelated components that preserve as much important variation as possible.**
