# 📊 Principal Component Analysis (PCA)

### From Basic Intuition → Mathematics → Interpretation → Post-Analysis

> 🎯 **Goal:** Understand what PCA does, why each step exists, how the mathematics works, and how to interpret the results.

---

## 📚 Table of Contents

1. [What Is PCA?](#1--what-is-pca)
2. [Why Do We Need PCA?](#2--why-do-we-need-pca)
3. [Why Standardization Matters](#3--why-standardization-matters)
4. [Complete PCA Workflow](#4--complete-pca-workflow)
5. [Covariance and Correlation](#5--covariance-and-correlation)
6. [Eigenvalues and Eigenvectors](#6--eigenvalues-and-eigenvectors)
7. [Principal Components](#7--principal-components)
8. [Component Matrix](#8--component-matrix)
9. [PCA Scores](#9--pca-scores)
10. [Explained Variance](#10--explained-variance)
11. [How Many Components Should We Keep?](#11--how-many-components-should-we-keep)
12. [Standardized PC Scores](#12--standardized-pc-scores)
13. [Eigenvectors vs Loadings](#13--eigenvectors-vs-loadings)
14. [Interpreting Principal Components](#14--interpreting-principal-components)
15. [Why Rotation Is Used](#15--why-rotation-is-used)
16. [Varimax Rotation](#16--varimax-rotation)
17. [Rotated Scores](#17--rotated-scores)
18. [Post-PCA Analysis](#18--post-pca-analysis)
19. [Common PCA Mistakes](#19--common-pca-mistakes)
20. [Complete PCA Story](#20--complete-pca-story)
21. [PCA Formula Sheet](#21--pca-formula-sheet)
22. [Quick Cheat Sheet](#22--quick-cheat-sheet)
23. [Applications](#23--applications)
24. [Final Mental Model](#24--final-mental-model)
25. [Recommended Video](#25--recommended-video)

---

# 1. 🧠 What Is PCA?

**PCA = Principal Component Analysis**

PCA is an **unsupervised dimensionality-reduction technique**.

It transforms many potentially correlated variables into a smaller number of new variables called:

> **Principal Components (PCs)**

These principal components:

* 📈 Capture as much variance as possible
* 🔗 Are mutually uncorrelated
* 🥇 Are ordered from most informative to least informative
* 📉 Can reduce dimensionality
* 🧩 Are linear combinations of the original variables

In simple words:

> **PCA summarizes many related variables using fewer informative dimensions.**

---

# 2. ❓ Why Do We Need PCA?

Real datasets often contain many variables.

Example:

| Person | DBP | SBP | Weight | Height |
| ------ | --: | --: | -----: | -----: |
| A      |  78 | 128 |     65 |    165 |
| B      |  82 | 132 |     75 |    175 |
| C      |  80 | 130 |     70 |    170 |

These variables may be correlated.

For example:

* 🩺 DBP may correlate with SBP
* ⚖️ Weight may correlate with height
* 📏 Weight and height may represent body size

This means four measured variables may contain fewer than four truly independent dimensions.

---

## 💡 PCA Intuition

Imagine the data forms a diagonal cloud:

```text
Y
↑

|                  •
|              •
|          •
|      •
|  •
|
+----------------------------→ X
```

The largest variation is not aligned with the original X or Y axis.

PCA finds better axes:

```text
                     ↗ PC1
                  •
              •
          •
      •
  •

            ↖ PC2
```

### 🥇 PC1

PC1 captures the:

> **Maximum possible variance**

### 🥈 PC2

PC2 captures the:

> **Maximum remaining variance while being orthogonal to PC1**

The process continues for PC3, PC4, etc.

---

# 3. ⚖️ Why Standardization Matters

PCA is driven by variance.

Suppose we measure:

| Variable |  Scale |
| -------- | -----: |
| Weight   |  70 kg |
| Height   | 170 cm |
| Height   | 1.70 m |

Height in centimeters and height in meters represent the same biological property, but their numerical variance is very different.

Example:

```text
Variance(weight)       ≈ 37.7
Variance(height in cm) ≈ 33
Variance(height in m)  ≈ 0.003
```

If PCA is performed directly on variables with very different scales:

> ⚠️ Variables with large numerical variance may dominate PCA.

---

## 🔧 Z-Score Standardization

A common solution is standardization.

$$
z = \frac{x-\mu}{\sigma}
$$

where:

* $x$ = original observation
* $\mu$ = variable mean
* $\sigma$ = standard deviation
* $z$ = standardized value

After standardization:

```text
Mean     ≈ 0
Variance ≈ 1
SD       ≈ 1
```

---

## 📋 Example

Suppose:

| Variable |  Mean |  SD |
| -------- | ----: | --: |
| DBP      |  80.2 | 2.6 |
| SBP      | 130.0 | 2.5 |
| Weight   |  69.6 | 6.6 |
| Height   | 169.7 | 6.4 |

If DBP is 78:

$$
z_{\text{DBP}} = \frac{78-80.2}{2.6}
$$

---

## 🧠 Important Note

Standardization is especially useful when variables have:

* Different units
* Different scales
* Very different variances

However:

> Standardization is not mathematically mandatory in every PCA problem.

If the original scale itself is scientifically meaningful, covariance-based PCA without standardization may be appropriate.

### 📌 Practical Rule

> If variables have different units or very different scales, standardize unless you have a scientific reason not to.

---

# 4. 🗺️ Complete PCA Workflow

```text
Raw Data
   ↓
Data Cleaning
   ↓
Standardization
   ↓
Covariance / Correlation Matrix
   ↓
Eigenvalue Decomposition
   ↓
Eigenvalues + Eigenvectors
   ↓
Principal Components
   ↓
PC Scores
   ↓
Explained Variance
   ↓
Select Important PCs
   ↓
Interpret Loadings
   ↓
Score Plot / Loading Plot / Biplot
   ↓
Optional Rotation
   ↓
Downstream Analysis
```

Step-by-step:

1. 🧹 Prepare the data
2. ⚖️ Standardize when appropriate
3. 🔗 Calculate covariance or correlation matrix
4. 🧮 Calculate eigenvalues
5. 🧭 Calculate eigenvectors
6. 🧩 Construct principal components
7. 📍 Calculate scores
8. 📊 Calculate explained variance
9. ✂️ Select important PCs
10. 🔎 Interpret loadings
11. 📉 Visualize the results
12. 🔄 Optionally rotate retained components
13. 🚀 Perform downstream analysis

---

# 5. 🔗 Covariance and Correlation

PCA needs information about how variables vary together.

---

## Covariance

For variables $X$ and $Y$:

$$
\mathrm{Cov}(X,Y)
=
\frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}{n-1}
$$

where:

* $x_i$ = observation $i$ for $X$
* $y_i$ = observation $i$ for $Y$
* $\bar{x}$ = mean of $X$
* $\bar{y}$ = mean of $Y$
* $n$ = number of observations

---

## 🧠 Covariance Interpretation

```text
Positive covariance

X ↑
Y ↑

Variables tend to increase together.
```

```text
Negative covariance

X ↑
Y ↓

One tends to increase while the other decreases.
```

```text
Covariance ≈ 0

No strong linear co-movement.
```

---

## 📦 Covariance Matrix

For two variables:

$$
\mathbf{C}
=
\begin{bmatrix}
\mathrm{Var}(X_1) & \mathrm{Cov}(X_1,X_2) \\
\mathrm{Cov}(X_2,X_1) & \mathrm{Var}(X_2)
\end{bmatrix}
$$

For four variables:

```text
          DBP   SBP   Weight   Height
DBP        •     •      •        •
SBP        •     •      •        •
Weight     •     •      •        •
Height     •     •      •        •
```

The diagonal contains:

> **Variances**

The off-diagonal elements contain:

> **Covariances**

---

## 🔗 Correlation

Correlation standardizes covariance.

$$
r_{XY}
=
\frac{\mathrm{Cov}(X,Y)}
{\sigma_X\sigma_Y}
$$

The correlation coefficient satisfies:

$$
-1 \le r \le 1
$$

Interpretation:

```text
r ≈ +1 → Strong positive relationship
r ≈  0 → Weak/no linear relationship
r ≈ -1 → Strong negative relationship
```

When all variables are standardized:

> PCA on standardized variables is equivalent to PCA using the correlation matrix.

---

# 6. 🧮 Eigenvalues and Eigenvectors

This is the mathematical heart of PCA.

Let the covariance or correlation matrix be:

$$
\mathbf{C}
$$

PCA solves:

$$
\mathbf{C}\mathbf{v} = \lambda\mathbf{v}
$$

where:

* $\mathbf{C}$ = covariance/correlation matrix
* $\mathbf{v}$ = eigenvector
* $\lambda$ = eigenvalue

---

## 🧭 Eigenvector

An eigenvector tells us:

> **The direction of a principal component**

Each eigenvector creates a new PCA axis.

---

## 📊 Eigenvalue

An eigenvalue tells us:

> **How much variance exists along that direction**

Remember:

```text
Eigenvector → Direction
Eigenvalue  → Variance captured
```

### 🧠 Memory Trick

> 🧭 Vector = direction
> 📊 Value = variance

---

## 📈 Ordering Eigenvalues

PCA orders components from largest eigenvalue to smallest:

$$
\lambda_1 \ge \lambda_2 \ge \lambda_3 \ge \cdots \ge \lambda_p
$$

Therefore:

```text
Largest eigenvalue
       ↓
      PC1

Second largest
       ↓
      PC2

Third largest
       ↓
      PC3
```

---

# 7. 🧩 Principal Components

A principal component is a linear combination of the original variables.

For standardized variables:

$$
PC_1 = w_1Z_{\text{DBP}} + w_2Z_{\text{SBP}} + w_3Z_{\text{Weight}} + w_4Z_{\text{Height}}
$$

The coefficients:

$$
w_1,;w_2,;w_3,;w_4
$$

come from the eigenvector associated with PC1.

---

## 📋 Example PC1

Suppose:

$$
PC_1 = -0.53Z_{\text{DBP}} - 0.50Z_{\text{SBP}} + 0.48Z_{\text{Weight}} + 0.49Z_{\text{Height}}
$$

Then:

| Variable | PC1 Weight |
| -------- | ---------: |
| DBP      |      -0.53 |
| SBP      |      -0.50 |
| Weight   |      +0.48 |
| Height   |      +0.49 |

---

## 🔍 Meaning of the Coefficients

```text
Large absolute coefficient
        ↓
Strong contribution

Small absolute coefficient
        ↓
Weak contribution
```

For PC1:

```text
DBP      −
SBP      −

Weight   +
Height   +
```

Therefore, increasing PC1 roughly corresponds to:

```text
↑ Weight
↑ Height

↓ DBP
↓ SBP
```

Possible interpretation:

> 🩺 **Blood Pressure vs Body Size**

---

# 8. 🧱 Component Matrix

Example:

| Variable |   PC1 |   PC2 |   PC3 |   PC4 |
| -------- | ----: | ----: | ----: | ----: |
| DBP      | -0.53 | -0.46 |  0.14 | -0.70 |
| SBP      | -0.50 | -0.52 | -0.16 |  0.68 |
| Weight   |  0.48 | -0.52 |  0.69 |  0.12 |
| Height   |  0.49 | -0.50 | -0.69 | -0.18 |

Each column is an eigenvector.

```text
Column PC1 → Eigenvector 1
Column PC2 → Eigenvector 2
Column PC3 → Eigenvector 3
Column PC4 → Eigenvector 4
```

---

## Normalized Eigenvectors

Eigenvectors are usually normalized:

$$
\sum_{j=1}^{p}v_{jk}^{2} = 1
$$

For PC1:

$$
(-0.53)^2 + (-0.50)^2 + (0.48)^2 + (0.49)^2 \approx 1
$$

The small difference is caused by rounding.

---

# 9. 📍 PCA Scores

A critical distinction:

> **Eigenvectors describe component directions.**

> **Scores describe observations.**

Suppose an observation has standardized values:

```text
DBP     = z₁
SBP     = z₂
Weight  = z₃
Height  = z₄
```

Then:

$$
\mathrm{Score}_{PC1}
=
-0.53z_1
-0.50z_2
+0.48z_3
+0.49z_4
$$

---

## 🧮 Matrix Form

Let:

* $\mathbf{Z}$ = standardized data matrix
* $\mathbf{V}$ = eigenvector matrix

Then:

$$
\mathbf{T} = \mathbf{Z}\mathbf{V}
$$

where:

* $\mathbf{T}$ = score matrix

Conceptually:

```text
Standardized Data
        ×
Eigenvectors
        ↓
     Scores
```

---

## 🧠 What Does a Score Mean?

A score tells us:

> **Where an observation lies along a particular principal component.**

Example:

```text
Person A → PC1 = -2.1
Person B → PC1 =  0.3
Person C → PC1 =  2.4
```

Person A and Person C are far apart along PC1.

Therefore, they differ strongly according to the pattern represented by PC1.

---

# 10. 📊 Explained Variance

Suppose PCA produces:

| PC  | Eigenvalue | % Variance | Cumulative % |
| --- | ---------: | ---------: | -----------: |
| PC1 |       2.41 |      60.2% |        60.2% |
| PC2 |       1.45 |      36.2% |    **96.4%** |
| PC3 |       0.10 |       2.5% |        98.9% |
| PC4 |       0.04 |       1.1% |         100% |

---

## Explained Variance Ratio

For component $k$:

$$
EVR_k = \frac{\lambda_k}{\sum_{j=1}^{p}\lambda_j}
$$

For four standardized variables:

$$
\sum_{j=1}^{4}\lambda_j \approx 4
$$

because each standardized variable contributes approximately one unit of variance.

---

## PC1

$$
\frac{2.41}{4} \approx 0.6025
$$

Therefore:

$$
PC1 \approx 60.2%
$$

---

## PC2

$$
\frac{1.45}{4} \approx 0.3625
$$

Therefore:

$$
PC2 \approx 36.2%
$$

---

## 🔥 PC1 + PC2

$$
60.2% + 36.2% = 96.4%
$$

Therefore:

> **PC1 and PC2 preserve approximately 96.4% of the variance.**

```text
4 Variables
    ↓
   PCA
    ↓
2 Principal Components
    ↓
≈ 96.4% Variance Retained
```

---

# 11. ✂️ How Many Components Should We Keep?

Several criteria can be used.

---

## 1️⃣ Cumulative Explained Variance

Typical heuristic thresholds:

```text
80%
90%
95%
```

Here:

$$
PC1 + PC2 = 96.4%
$$

Therefore:

> ✅ PC1 and PC2 are sufficient using this criterion.

---

## 2️⃣ Kaiser Criterion

For standardized PCA or PCA based on a correlation matrix:

> Retain components with eigenvalues greater than 1.

Because:

$$
\mathrm{Var}(Z)=1
$$

a component with:

$$
\lambda > 1
$$

explains more variance than one average standardized original variable.

Example:

```text
PC1 = 2.41 ✅
PC2 = 1.45 ✅
PC3 = 0.10 ❌
PC4 = 0.04 ❌
```

Therefore:

> ✅ Retain PC1 and PC2.

⚠️ The Kaiser criterion is a heuristic, not a universal law.

---

## 3️⃣ Scree Plot

```text
Eigenvalue
    │
2.5 │ ●
    │
2.0 │
    │
1.5 │       ●
    │
1.0 │
    │
0.5 │
    │                ●    ●
0.0 └────────────────────────
       PC1   PC2   PC3   PC4
```

Look for the:

> 🦵 **Elbow**

Here the large drop occurs after PC2.

Therefore:

> ✅ Retain PC1 and PC2.

---

## 4️⃣ Parallel Analysis

Parallel analysis compares observed eigenvalues against eigenvalues from random data.

Keep a component when:

```text
Observed eigenvalue
        >
Random-data eigenvalue
```

This is generally more rigorous than relying only on the Kaiser rule.

---

## 5️⃣ Scientific Context

Also consider:

* Biological importance
* Interpretability
* Downstream performance
* Cross-validation
* Reconstruction error

---

# 12. 📐 Standardized PC Scores

PC scores can themselves be standardized:

$$
Z_{PC_k} = \frac{PC_k-\overline{PC_k}}{SD(PC_k)}
$$

After standardization:

```text
Mean ≈ 0
SD   ≈ 1
```

This can help when components need to be compared on the same scale.

> ⚠️ Standardizing PC scores is not a mandatory step of PCA.

---

# 13. 🧲 Eigenvectors vs Loadings

These concepts are related but not identical.

---

## 🧭 Eigenvectors

Eigenvectors define the component directions.

Example PC1 eigenvector:

```text
DBP      -0.53
SBP      -0.50
Weight   +0.48
Height   +0.49
```

Normalized eigenvectors satisfy:

$$
\sum_j v_{jk}^{2}=1
$$

---

## 🧲 Loadings

Under a common standardized-PCA convention:

$$
l_{jk} = v_{jk}\sqrt{\lambda_k}
$$

where:

* $l_{jk}$ = loading
* $v_{jk}$ = eigenvector coefficient
* $\lambda_k$ = eigenvalue

For standardized variables, loadings can be interpreted as correlations between original variables and PC scores.

Example:

| Variable | PC1 Loading |
| -------- | ----------: |
| DBP      |       -0.82 |
| SBP      |       -0.77 |
| Weight   |       +0.75 |
| Height   |       +0.77 |

---

## 🧠 Interpretation

```text
|Loading| close to 1
        ↓
Strong relationship

|Loading| close to 0
        ↓
Weak relationship
```

---

## 🧠 Remember

```text
Eigenvalue
    ↓
How much variance?

Eigenvector
    ↓
Which direction?

Score
    ↓
Where is each observation?

Loading
    ↓
Which variables define the component?
```

---

# 14. 🔎 Interpreting Principal Components

Suppose PC1 loadings are:

```text
DBP      -0.82
SBP      -0.77
Weight   +0.75
Height   +0.77
```

We can identify two sides:

```text
Negative:
DBP
SBP

Positive:
Weight
Height
```

Therefore PC1 may represent:

> 🩺 **Blood Pressure vs Body Size**

---

## High PC1 Score

A high PC1 score may indicate:

```text
Higher Weight
Higher Height
Lower DBP
Lower SBP
```

---

## Low PC1 Score

A low PC1 score may indicate:

```text
Lower Weight
Lower Height
Higher DBP
Higher SBP
```

---

## ➕➖ Eigenvector Signs Are Arbitrary

Suppose:

$$
\mathbf{v} =
\begin{bmatrix}
-0.53 \
-0.50 \
0.48 \
0.49
\end{bmatrix}
$$

Then:

$$
-\mathbf{v} =
\begin{bmatrix}
0.53 \
0.50 \
-0.48 \
-0.49
\end{bmatrix}
$$

is equally valid.

Both represent the same PCA axis.

Therefore:

> ⚠️ Do not attach biological meaning to the absolute sign of a component.

Interpret the **relative relationships among variables**.

---

# 15. 🔄 Why Rotation Is Used

Sometimes PCA components are mathematically useful but difficult to interpret.

Example:

| Variable |   PC1 |   PC2 |
| -------- | ----: | ----: |
| DBP      | -0.53 | -0.46 |
| SBP      | -0.50 | -0.52 |
| Weight   |  0.48 | -0.52 |
| Height   |  0.49 | -0.50 |

Several variables contribute substantially to both PCs.

This is called:

> **Cross-loading**

---

## 🎯 Goal of Rotation

Rotation tries to produce:

```text
Variable A
   ↓
High loading on Component 1
Low loading on Component 2
```

and:

```text
Variable B
   ↓
Low loading on Component 1
High loading on Component 2
```

This makes interpretation easier.

---

# 16. 🔄 Varimax Rotation

Varimax is an **orthogonal rotation**.

Its goal is to:

* Increase large loadings
* Reduce intermediate loadings
* Simplify the component structure
* Keep rotated components orthogonal

---

## Before Rotation

| Variable |   PC1 |   PC2 |
| -------- | ----: | ----: |
| DBP      | -0.53 | -0.46 |
| SBP      | -0.50 | -0.52 |
| Weight   |  0.48 | -0.52 |
| Height   |  0.49 | -0.50 |

---

## After Varimax Rotation

| Variable |       RC1 |       RC2 |
| -------- | --------: | --------: |
| DBP      | **-0.97** |      0.18 |
| SBP      | **-0.98** |      0.10 |
| Weight   |      0.09 | **-0.97** |
| Height   |      0.12 | **-0.97** |

Now interpretation becomes clearer.

---

## 🩺 RC1

Strong loadings:

```text
DBP
SBP
```

Therefore:

> **RC1 ≈ Blood Pressure Component**

---

## ⚖️ RC2

Strong loadings:

```text
Weight
Height
```

Therefore:

> **RC2 ≈ Body Size Component**

---

## 🧠 Important Point

Rotation does not create new information.

It changes the orientation of the retained axes.

```text
PC1 + PC2
    ↓
Same retained subspace
    ↓
RC1 + RC2
```

---

# 17. 🔃 Rotated Scores

Let:

* $\mathbf{T}$ = retained PCA score matrix
* $\mathbf{R}$ = rotation matrix

Then:

$$
\mathbf{T}_{\text{rotated}} = \mathbf{T}\mathbf{R}
$$

---

## Variance Before Rotation

$$
2.41 + 1.45 = 3.86
$$

---

## Variance After Rotation

Suppose:

$$
1.94 + 1.92 = 3.86
$$

Therefore:

> 🔒 **Total variance in the retained orthogonal subspace is preserved.**

However, variance can be redistributed among rotated components.

---

# 18. 🚀 Post-PCA Analysis

PCA is often followed by additional analyses.

---

## 📊 1. Score Plot

Plot:

```text
PC2
 ↑

 │       ● ●
 │   ●
 │                ●
 │
 │ ●
 └────────────────────→ PC1
```

Useful for finding:

* Clusters
* Outliers
* Group separation
* Trends
* Batch effects

---

## 🧲 2. Loading Plot

A loading plot shows:

> Which variables contribute strongly to PC1, PC2, etc.?

---

## 🎯 3. Biplot

A biplot combines:

```text
Observation Scores
        +
Variable Loadings
```

This allows us to see:

* Sample positions
* Variable directions
* Relationships between samples and variables

---

## 📐 Interpreting Biplot Angles

```text
Small angle
    ↓
Positive correlation
```

```text
≈ 90°
    ↓
Weak linear correlation
```

```text
≈ 180°
    ↓
Negative correlation
```

---

## 🤖 4. PCA Before Machine Learning

Instead of:

```text
X1
X2
X3
...
X100
```

we may use:

```text
PC1
PC2
...
PC10
```

Potential benefits:

* Lower dimensionality
* Less multicollinearity
* Faster computation
* Noise reduction
* Easier visualization

---

## ⚠️ Important Warning

PCA does not use the target variable $y$.

It only analyzes variation in $\mathbf{X}$.

Therefore:

> High variance does not automatically mean high predictive importance.

---

## 🧩 5. PCA Before Clustering

```text
100 correlated variables
          ↓
         PCA
          ↓
10 Principal Components
          ↓
      Clustering
          ↓
       Groups
```

PCA can reduce redundant dimensions before clustering.

---

# 19. ⚠️ Common PCA Mistakes

## ❌ Mistake 1: Ignoring Scale

Different measurement units can distort PCA.

### ✅ Fix

Standardize when appropriate.

---

## ❌ Mistake 2: Thinking PC1 Is an Original Variable

PC1 is:

> A weighted combination of original variables.

---

## ❌ Mistake 3: Confusing Scores and Loadings

```text
Scores   → Observations
Loadings → Variables
```

---

## ❌ Mistake 4: Confusing Eigenvalues and Eigenvectors

```text
Eigenvalue  → Variance
Eigenvector → Direction
```

---

## ❌ Mistake 5: Treating Signs as Absolute

Eigenvector signs can be reversed without changing the PCA solution.

---

## ❌ Mistake 6: Assuming High Variance Means High Predictive Value

PCA is unsupervised.

---

## ❌ Mistake 7: Assuming PCA Finds Causality

PCA identifies correlation and variance structure.

It does not prove:

```text
X causes Y
```

---

## ❌ Mistake 8: Blindly Using 80–90%

Also consider:

* Scree plot
* Parallel analysis
* Domain knowledge
* Validation
* Interpretability

---

## ❌ Mistake 9: Thinking Rotation Adds Information

Rotation improves interpretability.

It does not create information.

---

# 20. 🧠 Complete PCA Story

Start with:

```text
DBP
SBP
Weight
Height
```

---

## Step 1️⃣ Standardize

$$
z = \frac{x-\mu}{\sigma}
$$

---

## Step 2️⃣ Build Covariance or Correlation Matrix

$$
\mathbf{C}
$$

---

## Step 3️⃣ Solve Eigenvalue Problem

$$
\mathbf{C}\mathbf{v} = \lambda\mathbf{v}
$$

---

## Step 4️⃣ Interpret Outputs

```text
Eigenvector → Direction
Eigenvalue  → Variance
```

---

## Step 5️⃣ Construct PCs

$$
PC_1 = -0.53Z_{\text{DBP}} - 0.50Z_{\text{SBP}} + 0.48Z_{\text{Weight}} + 0.49Z_{\text{Height}}
$$

---

## Step 6️⃣ Calculate Scores

$$
\mathbf{T} = \mathbf{Z}\mathbf{V}
$$

---

## Step 7️⃣ Calculate Explained Variance

```text
PC1 → 60.2%
PC2 → 36.2%
PC3 →  2.5%
PC4 →  1.1%
```

---

## Step 8️⃣ Reduce Dimensions

$$
PC1 + PC2 = 96.4%
$$

```text
4 dimensions
      ↓
2 dimensions
```

---

## Step 9️⃣ Interpret

Use:

* Eigenvectors
* Loadings
* Scores
* Scree plot
* Score plot
* Loading plot
* Biplot

---

## Step 🔟 Optional Rotation

```text
PC1 + PC2
    ↓
 Varimax
    ↓
RC1 + RC2
```

Possible interpretation:

```text
RC1 → Blood Pressure
RC2 → Body Size
```

---

# 21. 🧮 PCA Formula Sheet

## Standardization

$$
z = \frac{x-\mu}{\sigma}
$$

---

## Covariance

$$
\mathrm{Cov}(X,Y) = \frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}{n-1}
$$

---

## Correlation

$$
r_{XY} = \frac{\mathrm{Cov}(X,Y)}{\sigma_X\sigma_Y}
$$

---

## Eigenvalue Equation

$$
\mathbf{C}\mathbf{v} = \lambda\mathbf{v}
$$

---

## Principal Component

$$
PC_k = \mathbf{Z}\mathbf{v}_k
$$

---

## PCA Score Matrix

$$
\mathbf{T} = \mathbf{Z}\mathbf{V}
$$

---

## Explained Variance Ratio

$$
EVR_k = \frac{\lambda_k}{\sum_j\lambda_j}
$$

---

## Cumulative Explained Variance

$$
CEV_m = \frac{\sum_{k=1}^{m}\lambda_k}{\sum_{j=1}^{p}\lambda_j}
$$

---

## Loading

$$
l_{jk} = v_{jk}\sqrt{\lambda_k}
$$

---

## Standardized PC Score

$$
Z_{PC_k} = \frac{PC_k-\overline{PC_k}}{SD(PC_k)}
$$

---

## Rotated Scores

$$
\mathbf{T}_{\text{rotated}} = \mathbf{T}\mathbf{R}
$$

---

# 22. 📝 Quick Cheat Sheet

| Concept                | Meaning                            |
| ---------------------- | ---------------------------------- |
| 📊 PCA                 | Dimensionality reduction           |
| ⚖️ Standardization     | Makes scales comparable            |
| 🔗 Covariance          | How variables vary together        |
| 🔗 Correlation         | Standardized relationship          |
| 🧭 Eigenvector         | Direction of a PC                  |
| 📈 Eigenvalue          | Variance captured                  |
| 🧩 Principal Component | Linear combination of variables    |
| 📍 Score               | Observation position along PC      |
| 🧲 Loading             | Variable-PC relationship           |
| 📉 Explained Variance  | Variance captured by a PC          |
| 🦵 Scree Plot          | Helps select PCs                   |
| 1️⃣ Kaiser Criterion   | Often retain $\lambda > 1$         |
| 🔄 Varimax             | Rotation for easier interpretation |
| 🎯 Biplot              | Scores + loadings                  |

---

# 23. 🌍 Applications

## 🧬 Biology and Omics

PCA is widely used in:

* RNA-seq
* Gene-expression analysis
* Proteomics
* Metabolomics
* Population genetics
* Microbiome studies
* Single-cell analysis

Example:

```text
20,000 Genes
     ↓
    PCA
     ↓
PC1 + PC2
     ↓
Major Biological Patterns
```

---

## 🧫 Batch-Effect Detection

PCA can reveal whether samples separate according to:

```text
Biological Condition
        or
Technical Batch
```

---

## 🏭 Engineering

Uses include:

* Sensor analysis
* Fault detection
* Process monitoring
* Quality control
* Condition monitoring

---

## 🤖 Machine Learning

Uses include:

* Feature reduction
* Noise reduction
* Visualization
* Preprocessing
* Compression

---

## 🖼️ Image Processing

```text
Thousands of Pixels
        ↓
       PCA
        ↓
Few Important Components
```

---

## 💰 Finance

PCA can identify common factors among:

* Stocks
* Bond yields
* Interest rates
* Economic indicators

---

# 24. 🏁 Final Mental Model

Think of PCA as:

> 🔄 **Rotate → Rank → Project → Reduce → Interpret**

### 🔄 Rotate

Find directions that better describe the data.

### 📊 Rank

Order directions by variance captured.

### 📍 Project

Place observations onto the new axes.

### ✂️ Reduce

Discard low-information directions.

### 🔎 Interpret

Use scores, loadings, plots, and domain knowledge.

---

# 🧠 PCA in One Minute

```text
Many Correlated Variables
          ↓
     Standardize
          ↓
Covariance / Correlation Matrix
          ↓
 Eigenvalue Decomposition
          ↓
Eigenvectors + Eigenvalues
          ↓
Principal Components
          ↓
       Scores
          ↓
Explained Variance
          ↓
Keep Important PCs
          ↓
Reduce Dimensions
          ↓
Interpret + Visualize
```

---

# ⭐ Most Important Relationships

```text
Eigenvector
    ↓
Direction of PC

Eigenvalue
    ↓
Variance captured

Score
    ↓
Position of observation

Loading
    ↓
Relationship between variable and PC
```

---

# ✅ Final Takeaway

> **PCA transforms correlated variables into orthogonal principal components ordered by the amount of variance they explain.**

In one line:

```text
Original Variables
       ↓
      PCA
       ↓
Orthogonal Components
       ↓
Rank by Variance
       ↓
Keep Important PCs
       ↓
Simpler Representation
```

---

# 25. 🎥 Recommended Video

## StatQuest: Principal Component Analysis (PCA), Step-by-Step

▶️ YouTube:

https://www.youtube.com/watch?v=FgakZw6K1QQ

Recommended learning order:

```text
Variance
   ↓
Covariance
   ↓
Standardization
   ↓
Eigenvectors
   ↓
Eigenvalues
   ↓
PC Scores
   ↓
Explained Variance
   ↓
Loadings
   ↓
Biplots
   ↓
Rotation
```

> 🎯 Once these ideas connect, PCA becomes much easier to understand.
