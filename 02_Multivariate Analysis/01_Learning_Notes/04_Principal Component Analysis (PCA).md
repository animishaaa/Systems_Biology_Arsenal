# 📊 Principal Component Analysis (PCA)

### From Basic Intuition → Mathematics → Interpretation → Post-Analysis

> 🎯 **Goal:** Understand not only *how* PCA works, but **why every step exists**, what the mathematics means, and how to interpret the final results.

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
11. [Choosing the Number of PCs](#11--choosing-the-number-of-pcs)
12. [Standardized PC Scores](#12--standardized-pc-scores)
13. [Eigenvectors vs Loadings](#13--eigenvectors-vs-loadings)
14. [Interpreting Principal Components](#14--interpreting-principal-components)
15. [Rotation and Varimax](#15--rotation-and-varimax)
16. [Rotated Components](#16--rotated-components)
17. [Rotated Scores](#17--rotated-scores)
18. [Post-PCA Analysis](#18--post-pca-analysis)
19. [Common PCA Mistakes](#19--common-pca-mistakes)
20. [The Complete PCA Story](#20--the-complete-pca-story)
21. [Quick Cheat Sheet](#21--quick-cheat-sheet)
22. [Applications of PCA](#22--applications-of-pca)
23. [Recommended Video](#23--recommended-video)

---

# 1. 🧠 What Is PCA?

**PCA = Principal Component Analysis**

PCA is an **unsupervised dimensionality-reduction technique**.

It converts a dataset containing many potentially correlated variables into a smaller set of new variables called:

> **Principal Components (PCs)**

The principal components:

* 📈 Capture as much variance as possible
* 🔗 Are mutually uncorrelated
* 🥇 Are ordered from most informative to least informative
* 📉 Can be used to reduce dimensionality

In simple words:

> **PCA summarizes many related variables using a smaller number of informative dimensions.**

---

# 2. ❓ Why Do We Need PCA?

Real-world datasets often contain many variables.

For example:

| Person | DBP | SBP | Weight | Height |
| ------ | --: | --: | -----: | -----: |
| A      |  78 | 128 |     65 |    165 |
| B      |  82 | 132 |     75 |    175 |
| C      |  80 | 130 |     70 |    170 |

These variables may be correlated.

For example:

* 🩺 DBP may correlate with SBP
* ⚖️ Weight may correlate with height
* 📏 Weight and height may both represent a broader concept such as **body size**

Therefore, four measured variables may contain fewer than four truly independent dimensions of information.

---

## 💡 PCA Intuition

Imagine a cloud of points:

```text
             •
          •
       •
    •
 •
```

The original coordinate axes may not align with the direction where the data varies most.

PCA finds new axes.

```text
             •
          •
       •        ↗ PC1
    •        ↗
 •        ↗
```

### 🥇 PC1

The first principal component points in the direction containing the:

> **Maximum possible variance**

### 🥈 PC2

The second principal component captures the:

> **Next largest amount of variance**

while remaining orthogonal to PC1.

The same idea continues for PC3, PC4, and so on.

---

# 3. ⚖️ Why Standardization Matters

PCA is based on **variance**.

Variables measured using very different scales can therefore cause problems.

Consider:

| Variable | Example Scale |
| -------- | ------------: |
| Weight   |         70 kg |
| Height   |        170 cm |
| Height   |        1.70 m |

Height measured in centimeters and height measured in meters represent the same physical quantity.

However, their numerical variances are very different.

```text
Variance(weight)       ≈ 37.7
Variance(height in cm) ≈ 33
Variance(height in m)  ≈ 0.003
```

If PCA is applied directly to variables with incomparable scales:

> ⚠️ Variables with large numerical variances can dominate the principal components.

---

## 🔧 Z-Score Standardization

A common solution is to standardize each variable.

The Z-score formula is:

$$
z = \frac{x-\mu}{\sigma}
$$

where:

* $x$ = original observation
* $\mu$ = mean of the variable
* $\sigma$ = standard deviation
* $z$ = standardized observation

After standardization:

```text
Mean     ≈ 0
Variance ≈ 1
SD       ≈ 1
```

Example:

| Variable |  Mean |  SD |
| -------- | ----: | --: |
| DBP      |  80.2 | 2.6 |
| SBP      | 130.0 | 2.5 |
| Weight   |  69.6 | 6.6 |
| Height   | 169.7 | 6.4 |

Each observation is converted into a Z-score.

---

### 🧠 Important Note

Standardization is especially useful when variables have:

* Different units
* Different numerical scales
* Very different variances

However, standardization is **not mathematically mandatory for every PCA problem**.

PCA can also be performed directly on a covariance matrix when the original scale is scientifically meaningful.

> 📌 **Practical rule:** If the variables are measured in different units or have very different scales, standardize them before PCA unless there is a specific reason not to.

---

# 4. 🗺️ Complete PCA Workflow

The complete PCA pipeline is:

```text
Raw Data
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
Visualize / Analyze
   ↓
Optional Rotation
```

Step-by-step:

1. 🧹 Prepare the data
2. ⚖️ Standardize variables when appropriate
3. 🔗 Calculate covariance or correlation matrix
4. 🧮 Calculate eigenvalues
5. 🧭 Calculate eigenvectors
6. 🧩 Construct principal components
7. 📍 Calculate PCA scores
8. 📊 Calculate explained variance
9. ✂️ Decide how many PCs to retain
10. 🔎 Interpret components
11. 🔄 Optionally rotate retained components
12. 🚀 Use the PCs in downstream analysis

---

# 5. 🔗 Covariance and Correlation

PCA needs information about how variables vary together.

## Covariance

For two variables $X$ and $Y$:

$$
\operatorname{Cov}(X,Y)
=======================

\frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}{n-1}
$$

### Interpretation

```text
Positive covariance
X ↑ → Y tends to ↑

Negative covariance
X ↑ → Y tends to ↓

Covariance ≈ 0
No strong linear co-movement
```

---

## 📦 Covariance Matrix

For four variables:

```text
          DBP   SBP   Weight   Height
DBP        •     •      •        •
SBP        •     •      •        •
Weight     •     •      •        •
Height     •     •      •        •
```

The diagonal contains the variance of each variable.

The off-diagonal values contain covariance between pairs of variables.

For example:

$$
\mathbf{C}
==========

\begin{bmatrix}
\operatorname{Var}(X_1) & \operatorname{Cov}(X_1,X_2) \
\operatorname{Cov}(X_2,X_1) & \operatorname{Var}(X_2)
\end{bmatrix}
$$

When all variables are standardized, PCA on standardized variables is equivalent to PCA using the **correlation matrix**.

---

# 6. 🧮 Eigenvalues and Eigenvectors

This is the mathematical heart of PCA.

Suppose the covariance or correlation matrix is:

$$
\mathbf{C}
$$

PCA solves the eigenvalue equation:

$$
\mathbf{C}\mathbf{v}
====================

\lambda\mathbf{v}
$$

where:

* $\mathbf{C}$ = covariance/correlation matrix
* $\mathbf{v}$ = eigenvector
* $\lambda$ = eigenvalue

---

## 🧭 Eigenvector

An eigenvector tells us:

> **Which direction should the new PCA axis point?**

Each eigenvector defines the direction of one principal component.

---

## 📊 Eigenvalue

An eigenvalue tells us:

> **How much variance exists along that eigenvector direction?**

Therefore:

```text
Eigenvector → Direction
Eigenvalue  → Variance captured
```

### 🧠 Memory Trick

> 🧭 **Vector = direction**
> 📊 **Value = importance**

---

# 7. 🧩 Principal Components

A principal component is a **linear combination of the original standardized variables**.

For example:

$$
PC_1
====

w_1Z_{\text{DBP}}
+
w_2Z_{\text{SBP}}
+
w_3Z_{\text{Weight}}
+
w_4Z_{\text{Height}}
$$

Suppose PC1 is:

$$
PC_1
====

-0.53Z_{\text{DBP}}
-0.50Z_{\text{SBP}}
+0.48Z_{\text{Weight}}
+0.49Z_{\text{Height}}
$$

The coefficients come from the eigenvector corresponding to PC1.

---

## 🔍 Meaning of the Coefficients

```text
Large |coefficient|
        ↓
Strong contribution

Small |coefficient|
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

Therefore, increasing PC1 approximately corresponds to:

```text
↑ Body size
↓ Blood-pressure variables
```

So PC1 represents a contrast between:

> 🩺 **Blood pressure** ↔ ⚖️ **Body size**

---

# 8. 🧱 Component Matrix

Example eigenvector matrix:

| Variable |   PC1 |   PC2 |   PC3 |   PC4 |
| -------- | ----: | ----: | ----: | ----: |
| DBP      | -0.53 | -0.46 |  0.14 | -0.70 |
| SBP      | -0.50 | -0.52 | -0.16 |  0.68 |
| Weight   |  0.48 | -0.52 |  0.69 |  0.12 |
| Height   |  0.49 | -0.50 | -0.69 | -0.18 |

Each column is an eigenvector.

```text
Column 1 → PC1 direction
Column 2 → PC2 direction
Column 3 → PC3 direction
Column 4 → PC4 direction
```

For a normalized eigenvector:

$$
\sum_{j=1}^{p}v_{jk}^{2}=1
$$

---

# 9. 📍 PCA Scores

This distinction is extremely important:

> **Eigenvectors describe directions in variable space.**

> **Scores describe the observations projected onto those directions.**

Suppose one person has standardized measurements:

```text
DBP     = z₁
SBP     = z₂
Weight  = z₃
Height  = z₄
```

Then the PC1 score is:

$$
\operatorname{Score}_{PC1}
==========================

-0.53z_1
-0.50z_2
+0.48z_3
+0.49z_4
$$

In matrix notation:

$$
\mathbf{T}
==========

\mathbf{Z}\mathbf{V}
$$

where:

* $\mathbf{Z}$ = standardized data matrix
* $\mathbf{V}$ = eigenvector matrix
* $\mathbf{T}$ = PCA score matrix

Conceptually:

```text
Standardized Data
       ×
Eigenvectors
       ↓
PCA Scores
```

---

## 🧠 What Does a Score Mean?

A score tells us:

> **Where an observation lies along a principal-component axis.**

Example:

```text
Person A → PC1 = -2.1
Person B → PC1 =  0.3
Person C → PC1 =  2.4
```

These people occupy different positions along PC1.

---

# 10. 📊 Explained Variance

Suppose PCA produces:

| PC  | Eigenvalue | % Variance | Cumulative % |
| --- | ---------: | ---------: | -----------: |
| PC1 |       2.41 |      60.2% |        60.2% |
| PC2 |       1.45 |      36.2% |    **96.4%** |
| PC3 |       0.10 |       2.5% |        98.9% |
| PC4 |       0.04 |       1.1% |         100% |

The explained variance ratio for component $k$ is:

$$
\text{Explained Variance Ratio}_k
=================================

\frac{\lambda_k}
{\sum_{j=1}^{p}\lambda_j}
$$

For standardized PCA with four variables:

$$
\sum_{j=1}^{4}\lambda_j \approx 4
$$

subject to rounding.

---

## 💡 Main Result

```text
PC1 = 60.2%
PC2 = 36.2%
────────────
Total = 96.4%
```

Therefore:

> 🔥 **PC1 + PC2 retain approximately 96.4% of the total standardized variance.**

So PCA reduces:

```text
4 variables
     ↓
    PCA
     ↓
2 principal components
     ↓
≈ 96.4% variance retained
```

---

# 11. ✂️ Choosing the Number of PCs

Several methods can be used.

---

## 1️⃣ Cumulative Explained Variance

A common heuristic is to retain enough components to explain approximately:

```text
80%
90%
95%
```

of the variance.

Here:

$$
60.2% + 36.2% = 96.4%
$$

Therefore:

> ✅ PC1 and PC2 are sufficient using this criterion.

---

## 2️⃣ Kaiser Criterion

For PCA based on standardized variables or a correlation matrix:

> Retain components with eigenvalues greater than 1.

Why?

Each standardized original variable contributes approximately one unit of variance.

Therefore, a component with:

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

So:

> **Retain PC1 and PC2**

⚠️ The Kaiser rule is a heuristic, not a universal law.

---

## 3️⃣ Scree Plot

A scree plot displays eigenvalue against component number.

```text
Eigenvalue
    │
2.5 │ ●
    │
2.0 │
    │
1.5 │      ●
    │
1.0 │
    │
0.5 │
    │             ●    ●
0.0 └─────────────────────
       PC1  PC2  PC3  PC4
```

Look for the:

> 🦵 **Elbow**

Here, the sharp drop occurs after PC2.

Therefore:

> ✅ Retain PC1 and PC2.

---

## 🔬 More Advanced Methods

More rigorous approaches include:

* Parallel analysis
* Cross-validation
* Reconstruction error
* Downstream predictive performance
* Domain knowledge

---

# 12. 📐 Standardized PC Scores

Principal-component scores can also be standardized.

For component $k$:

$$
Z_{PC_k}
========

\frac{PC_k-\overline{PC_k}}
{SD(PC_k)}
$$

This gives approximately:

```text
Mean = 0
SD   = 1
```

This may be useful when PC scores are later used in analyses requiring comparable scales.

> ⚠️ Standardizing PC scores is **not a mandatory step of PCA itself**.

---

# 13. 🧲 Eigenvectors vs Loadings

This is one of the most commonly confused parts of PCA.

---

## 🧭 Eigenvectors

Eigenvectors define the component directions.

For normalized eigenvectors:

$$
\sum_j v_{jk}^{2}=1
$$

Example:

```text
PC1 eigenvector

DBP      -0.53
SBP      -0.50
Weight    0.48
Height    0.49
```

---

## 🧲 Loadings

Under a common standardized-PCA convention:

$$
l_{jk}
======

v_{jk}\sqrt{\lambda_k}
$$

where:

* $l_{jk}$ = loading of variable $j$ on component $k$
* $v_{jk}$ = eigenvector coefficient
* $\lambda_k$ = eigenvalue of component $k$

For standardized variables, these loadings can be interpreted as correlations between the original variables and PC scores.

Example:

| Variable | PC1 Loading |
| -------- | ----------: |
| DBP      |       -0.82 |
| SBP      |       -0.77 |
| Weight   |        0.75 |
| Height   |        0.77 |

Interpretation:

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
Eigenvalue  → How much variance?
Eigenvector → Which direction?
Score       → Where is each observation?
Loading     → Which variables strongly define a PC?
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

Then PC1 represents a contrast between:

```text
Blood pressure  ←→  Body size
```

A person with a high PC1 score may have relatively:

```text
Higher Weight / Height
Lower DBP / SBP
```

while a low PC1 score indicates the opposite pattern.

---

## ➕➖ Important: Eigenvector Signs Are Arbitrary

Suppose:

$$
\mathbf{v}
==========

\begin{bmatrix}
-0.53 \
-0.50 \
0.48 \
0.49
\end{bmatrix}
$$

Then:

$$
-\mathbf{v}
===========

\begin{bmatrix}
0.53 \
0.50 \
-0.48 \
-0.49
\end{bmatrix}
$$

is an equally valid eigenvector.

Therefore:

> ⚠️ The absolute positive/negative orientation of a PC has no intrinsic meaning.

What matters is the **relative relationship among variables**.

---

# 15. 🔄 Rotation and Varimax

Sometimes retained principal components are mathematically correct but difficult to interpret.

Example:

| Variable |   PC1 |   PC2 |
| -------- | ----: | ----: |
| DBP      | -0.53 | -0.46 |
| SBP      | -0.50 | -0.52 |
| Weight   |  0.48 | -0.52 |
| Height   |  0.49 | -0.50 |

Many variables contribute substantially to more than one component.

This is called **cross-loading**.

---

## 🔄 Varimax Rotation

Varimax is an **orthogonal rotation**.

Its goal is to create a simpler structure where variables tend to have:

```text
Large loading on one component
        +
Small loading on other components
```

while keeping the rotated components orthogonal.

Conceptually:

```text
Original retained PCA axes
           ↓
        Rotate
           ↓
Simpler interpretable axes
```

---

# 16. 🎯 Rotated Components

Example after Varimax rotation:

| Variable |       RC1 |       RC2 |
| -------- | --------: | --------: |
| DBP      | **-0.97** |      0.18 |
| SBP      | **-0.98** |      0.10 |
| Weight   |      0.09 | **-0.97** |
| Height   |      0.12 | **-0.97** |

Now interpretation is much clearer.

### 🩺 RC1

Strong loadings:

```text
DBP
SBP
```

Therefore:

> **RC1 ≈ Blood Pressure Component**

### ⚖️ RC2

Strong loadings:

```text
Weight
Height
```

Therefore:

> **RC2 ≈ Body Size Component**

---

# 17. 🔃 Rotated Scores

If $\mathbf{T}$ contains the retained PCA scores and $\mathbf{R}$ is the rotation matrix:

$$
\mathbf{T}_{rotated}
====================

\mathbf{T}\mathbf{R}
$$

Conceptually:

```text
Original PCA Scores
        ×
Rotation Matrix
        ↓
Rotated Scores
```

Example:

| Component | Variance |
| --------- | -------: |
| RC1       |     1.94 |
| RC2       |     1.92 |
| **Total** | **3.86** |

Before rotation:

$$
2.41 + 1.45 = 3.86
$$

After rotation:

$$
1.94 + 1.92 = 3.86
$$

Therefore:

> 🔒 **The total variance represented by the retained orthogonal subspace is preserved.**

However, the variance is redistributed between the rotated components.

---

# 18. 🚀 Post-PCA Analysis

PCA is often only the beginning.

The resulting PCA scores can be used in further analyses.

---

## 📊 1. Score Plot

Plot PC1 against PC2:

```text
PC2
 ↑
 │        ● ●
 │   ●
 │                ● ●
 │
 │ ●
 └────────────────────→ PC1
```

Useful for identifying:

* Clusters
* Outliers
* Trends
* Group separation
* Similar observations

---

## 🧲 2. Loading Plot

A loading plot helps answer:

> Which original variables are driving PC1 and PC2?

---

## 🎯 3. Biplot

A biplot combines:

```text
Observation scores
        +
Variable loadings
```

It simultaneously shows:

* Where observations are located
* Which variables explain those locations

---

## 🤖 4. Machine Learning

Instead of using:

```text
X1, X2, X3, ..., X100
```

we may use:

```text
PC1, PC2, ..., PC10
```

Potential benefits:

* Reduced dimensionality
* Reduced multicollinearity
* Faster model training
* Noise reduction
* Easier visualization

> ⚠️ PCA does not automatically improve prediction because PCA maximizes variance in $X$, not predictive information about a target $y$.

---

## 🧩 5. Clustering

PCA is commonly used before:

* K-means
* Hierarchical clustering
* Gaussian mixture models

Example:

```text
100 correlated variables
          ↓
         PCA
          ↓
10 principal components
          ↓
      Clustering
          ↓
Groups / Patterns
```

---

# 19. ⚠️ Common PCA Mistakes

## ❌ Mistake 1: Ignoring Scale

Variables measured in very different units can dominate covariance-based PCA.

### ✅ Solution

Standardize when appropriate.

---

## ❌ Mistake 2: Thinking PC1 Is an Original Variable

PC1 is not one original feature.

It is a:

> **Linear combination of the original variables**

---

## ❌ Mistake 3: Confusing Scores and Loadings

```text
Scores   → Observations
Loadings → Variables
```

---

## ❌ Mistake 4: Treating Signs as Absolute

The signs of eigenvectors may be reversed without changing the PCA solution.

---

## ❌ Mistake 5: Assuming High Variance Means High Predictive Value

PCA does not use a target variable.

It only examines variation in the predictor matrix $\mathbf{X}$.

Therefore:

> High variance does not automatically mean high predictive importance.

---

## ❌ Mistake 6: Assuming PCA Finds Causality

PCA identifies variance and correlation structure.

It does **not** establish:

```text
X causes Y
```

---

## ❌ Mistake 7: Blindly Using the 80–90% Rule

Explained variance should be considered together with:

* Domain knowledge
* Scree plot
* Parallel analysis
* Interpretability
* Validation
* Downstream performance

---

## ❌ Mistake 8: Thinking Rotation Creates Information

Rotation can improve interpretability.

It does **not** create additional information.

---

# 20. 🧠 The Complete PCA Story

Suppose we start with:

```text
DBP
SBP
Weight
Height
```

---

## Step 1️⃣ — Standardize

$$
z = \frac{x-\mu}{\sigma}
$$

Why?

> Put variables with different units or scales onto comparable scales.

---

## Step 2️⃣ — Build the Covariance/Correlation Matrix

$$
\mathbf{C}
$$

Why?

> Measure how variables vary together.

---

## Step 3️⃣ — Eigenvalue Decomposition

Solve:

$$
\mathbf{C}\mathbf{v}
====================

\lambda\mathbf{v}
$$

This gives:

```text
Eigenvectors → Directions
Eigenvalues  → Variance along those directions
```

---

## Step 4️⃣ — Construct Principal Components

$$
PC_k
====

\mathbf{Z}\mathbf{v}_k
$$

Each PC is a weighted combination of the original standardized variables.

---

## Step 5️⃣ — Calculate Scores

For all observations:

$$
\mathbf{T}
==========

\mathbf{Z}\mathbf{V}
$$

Now every observation receives:

```text
PC1 score
PC2 score
PC3 score
...
```

---

## Step 6️⃣ — Rank Components

Example:

```text
PC1 → 60.2%
PC2 → 36.2%
PC3 →  2.5%
PC4 →  1.1%
```

---

## Step 7️⃣ — Reduce Dimensionality

$$
PC1 + PC2 = 96.4%
$$

Therefore:

```text
4 dimensions
      ↓
2 dimensions
```

while retaining approximately 96.4% of the variance.

---

## Step 8️⃣ — Interpret

Inspect:

```text
Eigenvectors
Loadings
Score plots
Loading plots
Biplots
```

---

## Step 9️⃣ — Optional Rotation

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

## Step 🔟 — Downstream Analysis

Use PCA scores for:

* 📊 Visualization
* 🧩 Clustering
* 🤖 Machine learning
* 🔎 Outlier detection
* 🧬 Omics analysis
* 📉 Dimensionality reduction

---

# 21. 📝 Quick Cheat Sheet

| Concept                    | Meaning                                              |
| -------------------------- | ---------------------------------------------------- |
| 📊 **PCA**                 | Dimensionality-reduction technique                   |
| ⚖️ **Standardization**     | Places variables on comparable scales                |
| 🔗 **Covariance**          | How two variables vary together                      |
| 🧭 **Eigenvector**         | Direction of a PC                                    |
| 📈 **Eigenvalue**          | Variance captured by a PC                            |
| 🧩 **Principal Component** | Weighted linear combination of variables             |
| 📍 **Score**               | Position of an observation along a PC                |
| 🧲 **Loading**             | Association between an original variable and a PC    |
| 📉 **Explained Variance**  | Fraction of total variance captured                  |
| 🦵 **Scree Plot**          | Helps determine number of PCs                        |
| 1️⃣ **Kaiser Criterion**   | Retain eigenvalues greater than 1 in correlation PCA |
| 🔄 **Varimax**             | Orthogonal rotation for easier interpretation        |
| 🎯 **Biplot**              | Displays observations and variables together         |

---

# 22. 🌍 Applications of PCA

## 🧬 Biology and Omics

```text
Thousands of genes
        ↓
       PCA
        ↓
Few major expression patterns
```

Applications include:

* Gene expression
* Proteomics
* Metabolomics
* Population genetics
* Single-cell data exploration

---

## 🏭 Engineering

PCA can be used for:

* Sensor-data analysis
* Process monitoring
* Fault detection
* Quality control
* Condition monitoring

---

## 🤖 Machine Learning

PCA can help with:

* Feature reduction
* Multicollinearity reduction
* Visualization
* Noise reduction
* Data preprocessing

---

## 🖼️ Image Processing

Images may contain thousands or millions of correlated pixel values.

PCA can approximate the images using fewer dimensions.

---

## 💰 Finance

PCA can identify common variation across:

* Assets
* Interest rates
* Yield curves
* Macroeconomic indicators

---

# 23. 🎥 Recommended Video

## StatQuest — Principal Component Analysis (PCA), Step-by-Step

▶️ **YouTube**

https://www.youtube.com/watch?v=FgakZw6K1QQ

StatQuest provides an intuitive explanation of:

* PCA
* Variance
* Principal-component directions
* Eigenvectors
* Eigenvalues
* Dimensionality reduction

---

# 🧠 One-Minute PCA Story

```text
Many correlated variables
          ↓
     Standardize
          ↓
Covariance / Correlation Matrix
          ↓
Find directions of maximum variance
          ↓
      Eigenvectors
          ↓
Measure variance along those directions
          ↓
       Eigenvalues
          ↓
Project observations
          ↓
        Scores
          ↓
Keep important PCs
          ↓
Reduce dimensionality
          ↓
Interpret using loadings
          ↓
Visualize / Model / Cluster
```

---

# 🏁 Final Mental Model

Think of PCA as:

> 🔄 **Rotate → Rank → Project → Reduce → Interpret**

### 🔄 Rotate

Find better axes for describing the data.

### 📊 Rank

Order the axes according to variance captured.

### 📍 Project

Project every observation onto the new axes.

### ✂️ Reduce

Remove directions that contain relatively little variance.

### 🔎 Interpret

Use loadings, scores, visualizations, and domain knowledge to understand the resulting structure.

---

# ⭐ Formula Summary

### Standardization

$$
z
=

\frac{x-\mu}{\sigma}
$$

### Covariance

$$
\operatorname{Cov}(X,Y)
=======================

\frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}{n-1}
$$

### Eigenvalue Equation

$$
\mathbf{C}\mathbf{v}
====================

\lambda\mathbf{v}
$$

### Principal Component

$$
PC_k
====

\mathbf{Z}\mathbf{v}_k
$$

### All PCA Scores

$$
\mathbf{T}
==========

\mathbf{Z}\mathbf{V}
$$

### Explained Variance Ratio

$$
EVR_k
=====

\frac{\lambda_k}
{\sum_j \lambda_j}
$$

### PCA Loading

$$
l_{jk}
======

v_{jk}\sqrt{\lambda_k}
$$

### Orthogonal Rotation

$$
\mathbf{T}_{rotated}
====================

\mathbf{T}\mathbf{R}
$$

---

# ✅ Final Takeaway

> **PCA finds new orthogonal directions that capture the largest possible amount of variation in a dataset.**

In one line:

```text
Original correlated variables
            ↓
           PCA
            ↓
Fewer uncorrelated components
            ↓
Most important variance retained
```

> 📊 **PCA = Find the important directions → project the data → keep the useful dimensions.**
