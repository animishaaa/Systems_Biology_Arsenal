# 📊 Multivariate Statistics in R

## Correlation Matrix & Principal Component Analysis (PCA)

> 🎯 **Goal:** Learn how to explore relationships between multiple variables using covariance and correlation matrices, then use PCA to reduce dimensionality while preserving as much information as possible.

---

## 📚 Table of Contents

1. [What This Tutorial Covers](#1--what-this-tutorial-covers)
2. [Iris Dataset](#2--iris-dataset)
3. [Correlation Matrix](#3--correlation-matrix)
4. [Spearman Correlation](#4--spearman-correlation)
5. [Correlation Plot](#5--correlation-plot)
6. [Extracting Strong Correlations](#6--extracting-strong-correlations)
7. [Significance Testing of Correlations](#7--significance-testing-of-correlations)
8. [Covariance Matrix](#8--covariance-matrix)
9. [Why PCA Is Needed](#9--why-pca-is-needed)
10. [Variable Reduction Intuition](#10--variable-reduction-intuition)
11. [PCA Finds the Best Linear Combination](#11--pca-finds-the-best-linear-combination)
12. [PCA Using Eigenvectors Manually](#12--pca-using-eigenvectors-manually)
13. [Computing Principal Component Scores](#13--computing-principal-component-scores)
14. [PCA Using `prcomp`](#14--pca-using-prcomp)
15. [PCA Visualization with ggplot2](#15--pca-visualization-with-ggplot2)
16. [When PCA Does Not Work Well](#16--when-pca-does-not-work-well)
17. [PCA with Standardization](#17--pca-with-standardization)
18. [Choosing the Number of Components](#18--choosing-the-number-of-components)
19. [Loadings and Varimax Rotation](#19--loadings-and-varimax-rotation)
20. [PCA with the psych Package](#20--pca-with-the-psych-package)
21. [Complete Workflow](#21--complete-workflow)
22. [Key Concepts](#22--key-concepts)
23. [Quick R Cheat Sheet](#23--quick-r-cheat-sheet)
24. [Key Takeaways](#24--key-takeaways)

---

# 1. 🎯 What This Tutorial Covers

This tutorial introduces two fundamental topics in **multivariate statistics**:

1. 🔗 **Covariance and correlation matrices**
2. 📉 **Principal Component Analysis (PCA)**

These concepts are commonly used before or during:

* 🧩 Clustering
* 🤖 Classification
* 📉 Dimensionality reduction
* 📊 Multivariate modeling
* 🧬 Omics analysis
* 🔎 Exploratory data analysis

The basic workflow is:

```text
Multiple Variables
       ↓
Covariance / Correlation
       ↓
Understand Relationships
       ↓
PCA
       ↓
Reduce Dimensions
       ↓
Interpret / Visualize / Model
```

---

# 2. 🌸 Iris Dataset

The tutorial uses the built-in R dataset:

```r
iris
```

The Iris dataset contains measurements from three flower species.

---

## 🔍 Load and Inspect the Data

```r
head(iris)
```

Example output:

```text
  Sepal.Length Sepal.Width Petal.Length Petal.Width Species
1          5.1         3.5          1.4         0.2  setosa
2          4.9         3.0          1.4         0.2  setosa
3          4.7         3.2          1.3         0.2  setosa
...
```

---

## 📋 Dataset Structure

The variables are:

| Variable       | Type        |
| -------------- | ----------- |
| `Sepal.Length` | Numeric     |
| `Sepal.Width`  | Numeric     |
| `Petal.Length` | Numeric     |
| `Petal.Width`  | Numeric     |
| `Species`      | Categorical |

The first four columns contain numerical measurements.

The final column contains the flower species:

```text
setosa
versicolor
virginica
```

---

## ⚠️ Important

Correlation, covariance, and standard PCA calculations require numerical variables.

Therefore we often select:

```r
iris[, 1:4]
```

This means:

```text
Rows    → all rows

Columns → 1 through 4
```

---

# 3. 🔗 Correlation Matrix

## What Is Correlation?

Correlation measures the **strength and direction of a linear relationship** between two variables.

The correlation coefficient $r$ ranges from:

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
Little or no linear relationship


r = -1
↓
Perfect negative linear relationship
```

---

## Pearson Correlation

Pearson correlation is the default correlation method in R.

For variables $X$ and $Y$:

$$
r_{XY} = \frac{Cov(X,Y)}{\sigma_X\sigma_Y}
$$

---

## 🧮 Calculate the Correlation Matrix

```r
cor(iris[, 1:4], method = "pearson")
```

Example output:

```text
             Sepal.Length Sepal.Width Petal.Length Petal.Width
Sepal.Length    1.0000000  -0.1175698    0.8717538   0.8179411
Sepal.Width    -0.1175698   1.0000000   -0.4284401  -0.3661259
Petal.Length    0.8717538  -0.4284401    1.0000000   0.9628654
Petal.Width     0.8179411  -0.3661259    0.9628654   1.0000000
```

---

## 🔎 Interpretation

### Strongest correlation

```text
Petal.Length ↔ Petal.Width
r ≈ 0.96
```

This represents a **very strong positive relationship**.

As petal length increases, petal width also tends to increase.

---

### Another strong correlation

```text
Sepal.Length ↔ Petal.Length
r ≈ 0.87
```

This is also a strong positive relationship.

---

### Weak correlation

```text
Sepal.Length ↔ Sepal.Width
r ≈ -0.12
```

This represents a weak linear relationship.

---

## 🧠 Why Are Diagonal Values Equal to 1?

Every variable is perfectly correlated with itself.

Therefore:

$$
r_{XX}=1
$$

That is why the diagonal contains:

```text
1
1
1
1
```

---

# Correlation Within One Group

Sometimes we do not want correlations across the entire dataset.

For example, we may want correlations only within:

> 🌸 **versicolor**

Use:

```r
cor(
  iris[iris$Species == "versicolor", 1:4],
  method = "pearson"
)
```

The expression:

```r
iris$Species == "versicolor"
```

selects only observations belonging to that species.

Conceptually:

```text
Full Iris Dataset
        ↓
Select versicolor
        ↓
Keep Numeric Variables
        ↓
Calculate Correlations
```

---

# 4. 🏆 Spearman Correlation

Pearson correlation is based on the numerical values themselves.

It is primarily designed to measure:

> **Linear relationships**

Pearson correlation can also be affected by extreme observations.

---

## Why Use Spearman Correlation?

Spearman correlation works with the **ranks** of observations instead of their raw values.

Use:

```r
cor(
  iris[iris$Species == "versicolor", 1:4],
  method = "spearman"
)
```

---

## Spearman Characteristics

Spearman correlation:

* 🏆 Uses ranks
* 📈 Detects monotonic relationships
* 🛡️ Is generally less sensitive to extreme values
* ❌ Does not require a strictly linear relationship

---

## Pearson vs Spearman

| Pearson                                       | Spearman                                   |
| --------------------------------------------- | ------------------------------------------ |
| Uses raw values                               | Uses ranks                                 |
| Measures linear association                   | Measures monotonic association             |
| More sensitive to outliers                    | More robust to outliers                    |
| Common for approximately linear relationships | Useful for ranked/nonlinear monotonic data |

---

# 5. 🎨 Correlation Plot

Large correlation matrices can become difficult to inspect.

Instead of reading many numbers, we can visualize the relationships.

---

## Install / Load `corrplot`

```r
library(corrplot)
```

Calculate the correlation matrix:

```r
cor_mat <- cor(iris[, 1:4], method = "pearson")
```

Plot it:

```r
corrplot(cor_mat, type = "lower")
```

---

## 🔎 Interpretation

A typical `corrplot` visualization uses:

```text
Blue
 ↓
Positive correlation


Red
 ↓
Negative correlation


Large circle
 ↓
Strong correlation


Small circle
 ↓
Weak correlation
```

The diagonal represents:

```text
Variable vs itself
r = 1
```

and usually does not provide useful information for interpretation.

---

# 6. 🔥 Extracting Strong Correlations

Sometimes we want to automatically identify only the strongest relationships.

For example:

$$
|r| > 0.80
$$

---

## Step 1️⃣ — Remove the Diagonal

The diagonal always contains 1.

Remove it:

```r
diag(cor_mat) <- NA
```

---

## Step 2️⃣ — Remove Duplicate Correlations

The correlation matrix is symmetric.

For example:

```text
Correlation(A,B)
=
Correlation(B,A)
```

So we only need one triangle.

```r
cor_mat[upper.tri(cor_mat)] <- NA
```

Inspect:

```r
cor_mat
```

---

## Step 3️⃣ — Reshape the Matrix

Load:

```r
library(reshape)
```

Convert the matrix into long format:

```r
cor_melt <- melt(cor_mat)
```

Remove missing values:

```r
na.omit(cor_melt)
```

The structure becomes approximately:

```text
Variable 1     Variable 2      Correlation
------------------------------------------------
Petal.Width    Petal.Length       0.963
Petal.Length   Sepal.Length       0.872
...
```

---

## Step 4️⃣ — Extract Strong Correlations

For:

$$
|r| > 0.80
$$

use:

```r
index <- which(
  cor_melt$value > 0.80 |
  cor_melt$value < -0.80
)
```

Extract them:

```r
most_cor <- cor_melt[index, ]
```

Sort:

```r
most_cor[
  order(most_cor$value, decreasing = TRUE),
]
```

Example result:

```text
Petal.Width   Petal.Length   0.9628654
Petal.Length  Sepal.Length   0.8717538
Petal.Width   Sepal.Length   0.8179411
```

---

## 🧠 Simpler Mathematical Meaning

The condition:

```r
value > 0.80 | value < -0.80
```

is equivalent to:

$$
|r| > 0.80
$$

So we are selecting:

```text
Strong positive correlations

OR

Strong negative correlations
```

---

# 7. 🧪 Significance Testing of Correlations

A correlation coefficient tells us the **strength of an observed relationship**.

But we may also ask:

> Could this observed correlation plausibly have arisen by chance if the population correlation were zero?

---

## Testing One Pair

Example:

```r
cor.test(
  iris$Sepal.Length,
  iris$Sepal.Width
)
```

Important output includes:

* Correlation estimate
* p-value
* Confidence interval

Example:

```text
p-value ≈ 0.1519
```

The confidence interval includes zero.

Therefore:

> ❌ The correlation is not statistically significant at the conventional 0.05 level.

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

## P-Values for All Variable Pairs

Load:

```r
library(Hmisc)
```

Then:

```r
rcorr(
  as.matrix(iris[, 1:4]),
  type = "pearson"
)
```

`rcorr()` provides:

* 📊 Correlation matrix
* 🧪 P-value matrix
* 🔢 Number of observations

---

# Multiple Testing Problem

With several variables, many pairwise tests are performed.

For four variables, the number of unique comparisons is:

$$
\frac{4(4-1)}{2}=6
$$

So there are:

```text
6 unique pairwise correlation tests
```

---

## Bonferroni Correction

One simple multiple-testing correction is:

$$
p_{adjusted}=p\times m
$$

where:

* $p$ = original p-value
* $m$ = number of comparisons

Here:

```text
m = 6
```

In R:

```r
rcorr(
  as.matrix(iris[, 1:4]),
  type = "pearson"
)$P * 6
```

Rounded:

```r
round(
  rcorr(
    as.matrix(iris[, 1:4]),
    type = "pearson"
  )$P * 6,
  3
)
```

---

## 📌 Interpretation

After Bonferroni correction:

> Most of the stronger Iris correlations remain significant, while the weak Sepal.Length vs Sepal.Width relationship does not.

---

# 8. 📦 Covariance Matrix

## What Is Covariance?

Covariance describes how two variables change together.

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
One tends to increase while the other decreases


Covariance near zero
↓
Little linear co-movement
```

---

## Calculate the Covariance Matrix

```r
cov(iris[, 1:4])
```

Example:

```text
             Sepal.Length Sepal.Width Petal.Length Petal.Width
Sepal.Length    0.6856935 -0.0424340    1.2743154   0.5162707
...
```

---

## Diagonal Elements

The diagonal of the covariance matrix contains:

> **Variances**

For example:

```r
var(iris$Sepal.Length)
```

corresponds to the Sepal.Length diagonal entry.

Therefore:

$$
Cov(X,X)=Var(X)
$$

---

# Covariance of Standardized Variables

Standardize the variables:

```r
scale_iris <- scale(iris[, 1:4])
```

Calculate covariance:

```r
cov(scale_iris)
```

The resulting covariance matrix is the same as the Pearson correlation matrix, apart from possible tiny numerical rounding differences.

Therefore:

> ⭐ **Covariance matrix of standardized variables = correlation matrix**

This is a fundamental connection between standardization and PCA.

---

# 9. 📉 Why PCA Is Needed

Suppose a dataset contains:

* Many variables
* Strong correlations
* Redundant information

Then interpretation becomes difficult.

---

## The Problem

```text
Variable 1 ─┐
Variable 2 ─┤
Variable 3 ─┤
Variable 4 ─┤
Variable 5 ─┤
...         │
Variable p ─┘
```

Many variables may describe overlapping underlying patterns.

---

## PCA Solution

PCA:

* 🧩 Combines variables
* 📉 Reduces dimensions
* 📊 Preserves as much variance as possible
* 🔗 Creates mutually uncorrelated principal components

Conceptually:

```text
Many Correlated Variables
          ↓
         PCA
          ↓
Few Uncorrelated Components
          ↓
Most Variance Preserved
```

---

# 10. 🩺 Variable Reduction Intuition

Consider two blood-pressure measurements:

```r
DBP <- c(78, 80, 81, 82, 84, 86)

SBP <- c(126, 128, 127, 130, 130, 132)
```

Plot:

```r
plot(
  DBP,
  SBP,
  xlab = "Diastolic BP (mmHg)",
  ylab = "Systolic BP (mmHg)"
)
```

If DBP and SBP are strongly positively correlated, they contain overlapping information.

---

## 💡 Can We Combine Them?

A simple approach:

```r
BP_mean <- (DBP + SBP) / 2
```

or:

```r
BP_sum <- DBP + SBP
```

Both reduce two variables into one.

But these combinations were chosen manually.

---

## General Linear Combination

A general combination is:

$$
PC = \alpha_1X_1 + \alpha_2X_2
$$

For blood pressure:

$$
PC = \alpha_1DBP + \alpha_2SBP
$$

The question becomes:

> **Which values of $\alpha_1$ and $\alpha_2$ give the most informative combination?**

That is where PCA enters.

---

# 11. 🎯 PCA Finds the Best Linear Combination

PCA finds the coefficients that maximize the variance of the new component.

For two variables:

$$
PC_1 = \alpha_1X_1 + \alpha_2X_2
$$

PCA chooses the weights so that:

> **Variance of PC1 is maximized**

subject to the normalization constraint:

$$
\alpha_1^2+\alpha_2^2=1
$$

This prevents us from artificially increasing variance simply by making the coefficients arbitrarily large.

---

## Trying Different Weights

Example 1:

```r
BP <- 0.8 * DBP + 0.6 * SBP

var(BP)
```

Example 2:

```r
BP <- 0.6 * DBP + 0.8 * SBP

var(BP)
```

Different weights produce different variances.

PCA mathematically finds the direction producing the:

> 🥇 **Maximum variance**

---

# 12. 🧮 PCA Using Eigenvectors Manually

Create a data matrix:

```r
data <- cbind(DBP, SBP)
```

Calculate its covariance matrix:

```r
COV <- cov(data)
```

Calculate the eigenvalues and eigenvectors:

```r
eig <- eigen(COV)

eig
```

---

## Eigen Decomposition Output

The output contains:

```text
$values
↓
Eigenvalues


$vectors
↓
Eigenvectors
```

---

## 📊 Eigenvalues

Eigenvalues tell us:

> **How much variance each principal component explains**

The largest eigenvalue corresponds to PC1.

---

## 🧭 Eigenvectors

Eigenvectors provide:

> **The weights used to construct each principal component**

---

## First Principal Component Weights

```r
alfa1 <- eig$vectors[1, 1]

alfa2 <- eig$vectors[2, 1]
```

Then:

```r
BP <- alfa1 * DBP + alfa2 * SBP
```

Check its variance:

```r
var(BP)
```

This variance corresponds to the largest eigenvalue, subject to the same centering convention used in constructing the component.

---

## 🧠 Core PCA Relationship

```text
Covariance Matrix
       ↓
Eigen Decomposition
       ↓
┌──────────────────────┐
│ Eigenvalues          │ → Variance
│ Eigenvectors         │ → Directions / Weights
└──────────────────────┘
```

---

# 13. 📍 Computing Principal Component Scores

PCA usually operates on centered data.

For DBP:

$$
DBP_{centered}=DBP-\overline{DBP}
$$

For SBP:

$$
SBP_{centered}=SBP-\overline{SBP}
$$

---

## Calculate PC1 Scores

```r
PC1 <-
  eig$vectors[1, 1] * (DBP - mean(DBP)) +
  eig$vectors[2, 1] * (SBP - mean(SBP))
```

---

## Calculate PC2 Scores

```r
PC2 <-
  eig$vectors[1, 2] * (DBP - mean(DBP)) +
  eig$vectors[2, 2] * (SBP - mean(SBP))
```

---

## Plot the Scores

```r
plot(
  PC1,
  PC2,
  xlim = c(-6, 6),
  ylim = c(-6, 6)
)
```

Typically:

```text
PC1
↓
Large spread


PC2
↓
Small spread
```

Therefore:

> **PC1 explains more variance than PC2.**

---

## 🧠 What Are PCA Scores?

Scores tell us:

> **Where each observation lies along each principal-component axis.**

Remember:

```text
Eigenvector
    ↓
Direction / weights


Score
    ↓
Position of observation
```

---

# 14. 💻 PCA Using `prcomp`

Although PCA can be calculated manually, R provides a convenient implementation:

```r
pca <- prcomp(data)
```

Inspect:

```r
pca
```

---

## Important `prcomp` Components

### Standard deviations

```r
pca$sdev
```

These are the standard deviations of the principal-component scores.

---

### Component weights

```r
pca$rotation
```

These are the principal-component directions/loadings in the `prcomp` convention.

---

### Scores

```r
pca$x
```

These are the coordinates of each observation in PCA space.

---

## 📊 Variance Explained

Variance of each PC:

```r
pca$sdev^2
```

Total variance:

```r
sum(pca$sdev^2)
```

Proportion explained by PC1:

```r
pca$sdev[1]^2 / sum(pca$sdev^2)
```

For the blood-pressure example:

> **PC1 explains approximately 97% of the variance.**

Therefore, two correlated variables can be represented reasonably well by one principal component.

---

# 15. 🎨 PCA Visualization with ggplot2

Load packages:

```r
library(ggplot2)
library(scales)
```

Calculate proportions of explained variance:

```r
prop.pca <- pca$sdev^2 / sum(pca$sdev^2)
```

Convert PC scores to a data frame:

```r
dataset <- data.frame(pca$x)
```

Plot:

```r
ggplot(dataset) +
  geom_point(
    aes(PC1, PC2),
    size = 3.5
  ) +
  geom_text(
    aes(
      PC1,
      PC2,
      label = 1:length(PC1)
    ),
    size = 2.2,
    col = "white"
  ) +
  labs(
    x = paste(
      "PC1 (",
      percent(prop.pca[1]),
      ")",
      sep = ""
    ),
    y = paste(
      "PC2 (",
      percent(prop.pca[2]),
      ")",
      sep = ""
    )
  )
```

---

## Why Include Explained Variance in Axis Labels?

Instead of:

```text
PC1
PC2
```

the plot can show:

```text
PC1 (97%)
PC2 (3%)
```

This immediately tells us how much information each axis represents.

---

# 16. ⚠️ When PCA Does Not Work Well

PCA reduces dimensionality most effectively when variables contain shared or correlated structure.

Consider:

```r
x1 <- c(
  14.2, 7.7, 11.9, 9.2, 13.4,
  12.4, 10.9, 9.0, 11.4, 7.2
)

x2 <- c(
  5.6, 10.4, 9.3, 7.2, 11.4,
  5.9, 11.3, 8.0, 6.9, 5.2
)
```

Create the matrix:

```r
data <- cbind(x1, x2)
```

Perform PCA:

```r
pca <- prcomp(data)
```

Calculate PC1 variance proportion:

```r
pca$sdev[1]^2 / sum(pca$sdev^2)
```

Result:

```text
≈ 52%
```

---

## 🧠 Interpretation

If PC1 explains only about 52%, then PC2 still contains almost half of the total variance.

Therefore:

```text
2 original variables
        ↓
Keep only PC1
        ↓
Lose ~48% variance
```

That is not effective dimensionality reduction.

---

## Key Principle

> ⭐ **PCA is particularly useful when variables contain substantial correlated/redundant structure.**

If variables contain independent information, multiple components may be required.

---

# 17. ⚖️ PCA with Standardization

Now consider four variables:

```text
DBP
SBP
Weight
Height
```

Create:

```r
data <- data.frame(
  DBP,
  SBP,
  Weight,
  Height
)
```

Standardize:

```r
sdata <- scale(data)
```

Run PCA:

```r
pca <- prcomp(sdata)
```

Summary:

```r
summary(pca)
```

Example explained variance:

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

So:

```text
4 Original Variables
        ↓
       PCA
        ↓
2 Principal Components
        ↓
≈ 96% Variance Preserved
```

---

## Alternative R Syntax

`prcomp()` can also standardize directly:

```r
pca <- prcomp(
  data,
  center = TRUE,
  scale. = TRUE
)
```

This is often cleaner than manually calling `scale()` first.

---

# 18. ✂️ Choosing the Number of Components

Three commonly used approaches are:

1. 📊 Cumulative explained variance
2. 1️⃣ Kaiser criterion
3. 🦵 Scree plot

---

## 1️⃣ Explained Variance Rule

Retain enough PCs to explain approximately:

```text
80%
90%
or another scientifically useful threshold
```

Here:

$$
PC1 + PC2 \approx 96%
$$

Therefore:

> ✅ Keep PC1 and PC2.

---

## 2️⃣ Kaiser Criterion

For standardized PCA:

> Retain components with eigenvalues greater than 1.

Conceptually:

```text
Eigenvalue > 1
      ↓
Component explains more variance
than one standardized variable
```

---

## 3️⃣ Scree Plot

R provides:

```r
plot(pca, type = "l")
```

The scree plot displays approximately:

```text
Variance
   │
   │ ●
   │
   │      ●
   │
   │             ●
   │                 ●
   └────────────────────→
      PC1 PC2 PC3 PC4
```

Look for the:

> 🦵 **Elbow point**

If the curve flattens strongly after PC2:

> ✅ Keep PC1 and PC2.

---

# 19. 🔄 Loadings and Varimax Rotation

## Why Rotate?

Unrotated principal components may contain substantial contributions from several variables.

That can make interpretation difficult.

Rotation aims to produce a simpler loading structure.

---

## Varimax Rotation

Varimax is an **orthogonal rotation**.

Use:

```r
varmax <- varimax(
  pca$rotation[, 1:2]
)
```

Inspect:

```r
print(
  loadings(varmax),
  cutoff = 0
)
```

A possible interpretation is:

```text
DBP
SBP
 ↓
Rotated Component 1


Weight
Height
 ↓
Rotated Component 2
```

Therefore:

```text
RC1 ≈ Blood Pressure

RC2 ≈ Body Size
```

---

## 🧠 Why Rotation Helps

Before rotation:

```text
Variable A → PC1 + PC2
Variable B → PC1 + PC2
Variable C → PC1 + PC2
```

After rotation:

```text
Variable A → Mainly RC1
Variable B → Mainly RC1

Variable C → Mainly RC2
Variable D → Mainly RC2
```

This produces a cleaner interpretation.

---

## Important Point

> Rotation does **not create additional information**.

For an orthogonal rotation, the retained component subspace stays the same.

Rotation mainly changes:

> **Interpretability**

---

# 20. 🧠 PCA with the `psych` Package

The `psych` package provides another way of performing component analysis.

Load:

```r
library(psych)
```

Run:

```r
pr <- principal(
  data,
  nfactors = 2,
  rotate = "none"
)
```

Inspect:

```r
pr
```

---

## Loadings

In this framework, component loadings can be interpreted as relationships between original variables and components.

For standardized component solutions, these are commonly interpreted similarly to variable-component correlations.

---

## Example Check

```r
cor(
  pr$scores[, 1],
  DBP
)
```

This examines the correlation between:

```text
PC1 scores
    ↕
DBP
```

---

# Varimax Using `psych`

```r
pr_varmax <- principal(
  data,
  nfactors = 2,
  rotate = "varimax"
)
```

Inspect scores:

```r
round(
  pr_varmax$scores,
  2
)
```

Possible interpretation:

```text
RC1 → Blood Pressure

RC2 → Body Size
```

---

# 21. 🗺️ Complete Workflow

The entire tutorial can be summarized as:

```text
Raw Multivariate Data
        ↓
Select Numeric Variables
        ↓
Correlation Matrix
        ↓
Inspect Strong Relationships
        ↓
Test Correlation Significance
        ↓
Covariance Matrix
        ↓
Standardize Variables
        ↓
PCA
        ↓
Eigenvalues + Eigenvectors
        ↓
PC Scores
        ↓
Explained Variance
        ↓
Choose Number of PCs
        ↓
Interpret Loadings
        ↓
Optional Varimax Rotation
        ↓
Visualization / Clustering / Modeling
```

---

# 22. 🧠 Key Concepts

## 🔗 Correlation

Answers:

> **How strongly are two variables linearly related?**

$$
-1 \le r \le 1
$$

---

## 📦 Covariance

Answers:

> **Do two variables tend to vary together?**

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

Tells us:

> **Direction / component weights**

---

## 📊 Eigenvalue

Tells us:

> **Variance captured by a component**

---

## 🧩 Principal Component

A weighted linear combination:

$$
PC_1 = \alpha_1X_1 + \alpha_2X_2 + \cdots + \alpha_pX_p
$$

---

## 📍 Score

Tells us:

> **Where an observation lies along a PC**

---

## 🧲 Loading

Tells us:

> **How strongly a variable is associated with a component**

---

## 🔄 Rotation

Helps:

> **Make component interpretation clearer**

---

# 23. 💻 Quick R Cheat Sheet

## Inspect Iris

```r
head(iris)
```

---

## Pearson Correlation

```r
cor(
  iris[, 1:4],
  method = "pearson"
)
```

---

## Spearman Correlation

```r
cor(
  iris[, 1:4],
  method = "spearman"
)
```

---

## Correlation Matrix

```r
cor_mat <- cor(
  iris[, 1:4],
  method = "pearson"
)
```

---

## Correlation Plot

```r
library(corrplot)

corrplot(
  cor_mat,
  type = "lower"
)
```

---

## Covariance Matrix

```r
cov(iris[, 1:4])
```

---

## Standardize Data

```r
scale_iris <- scale(
  iris[, 1:4]
)
```

---

## Correlation Significance

```r
cor.test(
  iris$Sepal.Length,
  iris$Sepal.Width
)
```

---

## All Correlation P-Values

```r
library(Hmisc)

rcorr(
  as.matrix(iris[, 1:4]),
  type = "pearson"
)
```

---

## PCA

```r
pca <- prcomp(
  iris[, 1:4],
  center = TRUE,
  scale. = TRUE
)
```

---

## PCA Summary

```r
summary(pca)
```

---

## PC Standard Deviations

```r
pca$sdev
```

---

## PC Variances

```r
pca$sdev^2
```

---

## PCA Weights

```r
pca$rotation
```

---

## PCA Scores

```r
pca$x
```

---

## Explained Variance Proportion

```r
pca$sdev^2 / sum(pca$sdev^2)
```

---

## Scree Plot

```r
plot(
  pca,
  type = "l"
)
```

---

## Varimax

```r
varmax <- varimax(
  pca$rotation[, 1:2]
)
```

---

# 24. ✅ Key Takeaways

### 🔗 Correlation Matrix

Shows pairwise relationships between variables.

```text
+1 → Strong positive
 0 → Weak/no linear relationship
-1 → Strong negative
```

---

### 🏆 Spearman vs Pearson

```text
Pearson
↓
Linear relationships


Spearman
↓
Rank-based monotonic relationships
```

---

### 📦 Covariance

Shows whether variables change together.

Standardized covariance becomes correlation.

---

### 📉 PCA

PCA reduces dimensionality by replacing correlated variables with fewer principal components.

---

### 🧭 Eigenvectors

> **Directions / weights**

---

### 📊 Eigenvalues

> **Variance explained**

---

### 📍 Scores

> **Positions of observations in PCA space**

---

### 🧲 Loadings

> **Relationships between variables and components**

---

### ⚖️ Standardization

Especially important when variables have different units or scales.

---

### 🔄 Rotation

Improves component interpretation but does not create additional information.

---

# 🧠 Final Mental Model

Remember the tutorial as:

> **Relate → Standardize → Rotate → Reduce → Interpret**

```text
RELATE
  ↓
Correlation / Covariance


STANDARDIZE
  ↓
Put variables on comparable scales


ROTATE
  ↓
Find principal directions


REDUCE
  ↓
Keep important PCs


INTERPRET
  ↓
Scores + Loadings + Plots
```

---

# ⭐ One-Line Summary

> **Correlation tells us which variables move together; PCA uses those relationships to replace correlated variables with fewer uncorrelated components that preserve most of the variation in the data.**
