# 📊 Principal Component Analysis (PCA)

### From Basic Intuition → Mathematics → Interpretation → Post-Analysis

> 🎯 **Goal:** Understand not only *how* PCA works, but **why every step exists** and how to interpret the final result.

---

## 📚 Table of Contents

1. [What is PCA?](#1--what-is-pca)
2. [Why do we need PCA?](#2--why-do-we-need-pca)
3. [Why standardization matters](#3--why-standardization-matters)
4. [Complete PCA workflow](#4--complete-pca-workflow)
5. [Covariance and correlation](#5--covariance-and-correlation)
6. [Eigenvalues and eigenvectors](#6--eigenvalues-and-eigenvectors)
7. [Principal components](#7--principal-components)
8. [Component matrix](#8--component-matrix)
9. [PCA scores](#9--pca-scores)
10. [Explained variance](#10--explained-variance)
11. [Choosing the number of PCs](#11--choosing-the-number-of-pcs)
12. [Standardized PC scores](#12--standardized-pc-scores)
13. [Eigenvectors vs loadings](#13--eigenvectors-vs-loadings)
14. [Interpreting PCs](#14--interpreting-pcs)
15. [Rotation and Varimax](#15--rotation-and-varimax)
16. [Rotated components](#16--rotated-components)
17. [Rotated scores](#17--rotated-scores)
18. [Post-PCA analysis](#18--post-pca-analysis)
19. [Common mistakes](#19--common-mistakes)
20. [Complete PCA story](#20--complete-pca-story)
21. [Quick cheat sheet](#21--quick-cheat-sheet)
22. [Applications](#22--applications)
23. [Recommended video](#23--recommended-video)

---

# 1. 🧠 What Is PCA?

**PCA = Principal Component Analysis**

PCA is an **unsupervised dimensionality-reduction technique**.

It transforms a dataset containing many potentially correlated variables into a smaller set of new variables called:

> **Principal Components (PCs)**

The PCs are constructed so that they:

* 📈 Capture as much variance as possible
* 🔗 Are mutually uncorrelated
* 🥇 Are ordered from most informative to least informative
* 📉 Can reduce the dimensionality of the original dataset

In simple terms:

> **PCA tries to summarize many related variables using a smaller number of informative dimensions.**

---

# 2. ❓ Why Do We Need PCA?

## The problem

Real datasets often contain many variables.

For example:

| Person | DBP | SBP | Weight | Height |
| ------ | --: | --: | -----: | -----: |
| A      |  78 | 128 |     65 |    165 |
| B      |  82 | 132 |     75 |    175 |
| C      |  80 | 130 |     70 |    170 |

These variables may not be independent.

For example:

* 🩺 DBP may correlate with SBP
* ⚖️ Weight may correlate with height
* 📏 Height and weight may describe a common concept such as **body size**

Therefore, four measured variables may contain fewer than four truly independent dimensions of information.

---

## 💡 PCA's idea

Imagine a cloud of points:

```text
             •
          •
       •
    •
 •
```

The original coordinate axes might not align with the direction in which the data varies most.

PCA effectively finds new axes:

```text
             •
          •
       •        ↗ PC1
    •        ↗
 •        ↗
```

### PC1

The first principal component points in the direction containing the:

> 🥇 **maximum possible variance**

### PC2

The second principal component captures the:

> 🥈 **next largest amount of variance**

while remaining orthogonal to PC1.

And so on.

---

# 3. ⚖️ Why Standardization Matters

Before PCA, variables measured on very different scales commonly need to be standardized.

Consider:

| Variable | Typical scale |
| -------- | ------------: |
| Weight   |         70 kg |
| Height   |        170 cm |
| Height   |        1.70 m |

Height measured in centimeters and height measured in meters represent the same physical quantity.

But their numerical variances are dramatically different.

Example:

```text
Variance(weight)       ≈ 37.7
Variance(height in cm) ≈ 33
Variance(height in m)  ≈ 0.003
```

⚠️ PCA is driven by **variance**.

Therefore, if raw variables have incomparable scales, variables with numerically large variance can dominate the PCA.

---

## 🔧 Standardization

A common transformation is the **Z-score**:

[
z = \frac{x-\mu}{\sigma}
]

where:

* (x) = original observation
* (\mu) = variable mean
* (\sigma) = standard deviation
* (z) = standardized observation

After standardization:

```text
Mean ≈ 0
Variance ≈ 1
SD ≈ 1
```

Example:

| Variable |  Mean |  SD |
| -------- | ----: | --: |
| DBP      |  80.2 | 2.6 |
| SBP      | 130.0 | 2.5 |
| Weight   |  69.6 | 6.6 |
| Height   | 169.7 | 6.4 |

Each observation is transformed into its corresponding Z-score.

---

### 🧠 Important nuance

Standardization is strongly recommended when variables have:

* Different units
* Different numerical scales
* Very different variances

However, it is **not mathematically mandatory in every PCA problem**.

PCA can be performed on a covariance matrix without standardization when the original scale itself is scientifically meaningful.

> 📌 **Practical rule:** If variables use different units or scales, standardize unless you have a specific reason not to.

---

# 4. 🗺️ Complete PCA Workflow

The complete PCA pipeline can be remembered as:

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

Or:

1. 🧹 Prepare the data
2. ⚖️ Standardize variables when appropriate
3. 🔗 Calculate covariance/correlation matrix
4. 🧮 Calculate eigenvalues
5. 🧭 Calculate eigenvectors
6. 🧩 Construct principal components
7. 📍 Calculate scores
8. 📊 Calculate explained variance
9. ✂️ Decide how many PCs to retain
10. 🔎 Interpret components
11. 🔄 Optionally rotate retained components
12. 🚀 Use PCs in downstream analysis

---

# 5. 🔗 Covariance and Correlation

PCA needs information about how variables vary together.

## Covariance

For two variables (X) and (Y):

[
Cov(X,Y)
========

\frac{\sum (x_i-\bar{x})(y_i-\bar{y})}{n-1}
]

Interpretation:

```text
Positive covariance
X ↑ → Y tends to ↑

Negative covariance
X ↑ → Y tends to ↓

Covariance near zero
No strong linear co-movement
```

---

## 📦 Covariance matrix

For four variables:

```text
          DBP   SBP   Weight   Height
DBP        •     •      •        •
SBP        •     •      •        •
Weight     •     •      •        •
Height     •     •      •        •
```

The diagonal contains the variance of each variable.

The off-diagonal values describe covariance between pairs of variables.

When all variables are standardized, PCA based on the standardized variables is equivalent to PCA using the **correlation matrix**.

---

# 6. 🧮 Eigenvalues and Eigenvectors

This is the mathematical heart of PCA.

Suppose the covariance/correlation matrix is:

[
C
]

PCA solves:

[
C\mathbf{v}=\lambda\mathbf{v}
]

where:

* (C) = covariance/correlation matrix
* (\mathbf{v}) = eigenvector
* (\lambda) = eigenvalue

---

## 🧭 Eigenvector

An eigenvector tells us:

> **Which direction should the new PCA axis point?**

Each eigenvector defines one principal component.

---

## 📊 Eigenvalue

An eigenvalue tells us:

> **How much variance exists along that principal-component direction?**

Therefore:

```text
Eigenvector → direction
Eigenvalue  → variance captured
```

### Memory trick 🧠

> 🧭 **Vector = direction**
> 📊 **Value = importance**

---

# 7. 🧩 Principal Components

A principal component is a **linear combination** of the original standardized variables.

For example:

[
PC_1 =
w_1Z_{DBP}
+w_2Z_{SBP}
+w_3Z_{Weight}
+w_4Z_{Height}
]

Suppose:

[
PC_1 =
-0.53Z_{DBP}
-0.50Z_{SBP}
+0.48Z_{Weight}
+0.49Z_{Height}
]

The coefficients come from the eigenvector associated with PC1.

---

## 🔍 Reading the coefficients

```text
Large |coefficient|
        ↓
Strong contribution to that direction

Small |coefficient|
        ↓
Weak contribution
```

The sign indicates direction.

For this PC:

```text
DBP      −
SBP      −

Weight   +
Height   +
```

So increasing the PC1 score corresponds broadly to:

```text
↑ Body size
↓ Blood-pressure variables
```

This suggests a **contrast between body size and blood pressure** in this dataset.

---

# 8. 🧱 Component Matrix

Example eigenvector/component matrix:

| Variable |   PC1 |   PC2 |   PC3 |   PC4 |
| -------- | ----: | ----: | ----: | ----: |
| DBP      | -0.53 | -0.46 |  0.14 | -0.70 |
| SBP      | -0.50 | -0.52 | -0.16 |  0.68 |
| Weight   |  0.48 | -0.52 |  0.69 |  0.12 |
| Height   |  0.49 | -0.50 | -0.69 | -0.18 |

Each **column** is an eigenvector:

```text
Column 1 → PC1 direction
Column 2 → PC2 direction
Column 3 → PC3 direction
Column 4 → PC4 direction
```

For normalized eigenvectors:

[
\sum_j v_j^2 = 1
]

---

# 9. 📍 PCA Scores

This distinction is extremely important.

### Eigenvectors/components describe variables.

### Scores describe observations.

Suppose a person has standardized measurements:

```text
DBP     = z₁
SBP     = z₂
Weight  = z₃
Height  = z₄
```

Then:

[
Score_{PC1}
===========

-0.53z_1
-0.50z_2
+0.48z_3
+0.49z_4
]

In matrix notation:

[
T = ZV
]

where:

* (Z) = standardized data matrix
* (V) = eigenvector/component matrix
* (T) = score matrix

So:

```text
Standardized observations
          ×
Component directions
          ↓
       PC Scores
```

---

## 🧠 Intuition

A score answers:

> **Where is this observation located along this principal-component axis?**

For example:

```text
Person A → PC1 = -2.1
Person B → PC1 =  0.3
Person C → PC1 =  2.4
```

These people occupy different positions along PC1.

---

# 10. 📊 Explained Variance

Example:

| PC  | Eigenvalue / Variance | % Variance | Cumulative % |
| --- | --------------------: | ---------: | -----------: |
| PC1 |                  2.41 |      60.2% |        60.2% |
| PC2 |                  1.45 |      36.2% |    **96.4%** |
| PC3 |                  0.10 |       2.5% |        98.9% |
| PC4 |                  0.04 |       1.1% |         100% |

The explained variance ratio is:

[
\text{Explained Variance Ratio}_k
=================================

\frac{\lambda_k}{\sum_j\lambda_j}
]

For standardized PCA with four variables:

[
\sum_j\lambda_j = 4
]

approximately, subject to rounding.

---

## 💡 Main result

```text
PC1 = 60.2%
PC2 = 36.2%
────────────
Total = 96.4%
```

🔥 Two dimensions retain approximately **96.4% of the total variance** originally represented by four standardized variables.

That is dimensionality reduction:

```text
4 variables
    ↓ PCA
2 components
    ↓
≈96.4% variance retained
```

---

# 11. ✂️ Choosing the Number of PCs

There is no single universal rule. Several criteria are commonly considered together.

---

## Rule 1️⃣: Cumulative explained variance

Choose enough PCs to retain an acceptable percentage of variance.

Common heuristic:

```text
80% ─┐
90%  ├─ often considered
95% ─┘
```

Here:

[
PC1+PC2=96.4%
]

✅ PC1 and PC2 would be sufficient under this criterion.

---

## Rule 2️⃣: Kaiser criterion

For PCA based on a correlation matrix:

> Retain components with eigenvalue (>1).

Why 1?

After standardization, each original variable contributes approximately one unit of variance.

So a PC with:

[
\lambda > 1
]

explains more variance than one average standardized original variable.

Here:

```text
PC1 = 2.41 ✅
PC2 = 1.45 ✅
PC3 = 0.10 ❌
PC4 = 0.04 ❌
```

Therefore:

> **Retain PC1 and PC2**

⚠️ The Kaiser criterion is a heuristic, not a universal law.

---

## Rule 3️⃣: Scree plot

Plot:

```text
Eigenvalue
    │
2.5 │ ●
    │
2.0 │
    │
1.5 │     ●
    │
1.0 │
    │
0.5 │
    │           ●    ●
0.0 └────────────────────
       PC1  PC2  PC3  PC4
```

Look for the:

> 🦵 **Elbow**

Here, the major drop occurs after PC2.

Therefore:

> Keep PC1 + PC2.

---

## 🔬 More advanced approaches

For serious analysis, also consider:

* Parallel analysis
* Cross-validation
* Reconstruction error
* Domain knowledge
* Downstream predictive performance

---

# 12. 📐 Standardized PC Scores

Raw component scores can themselves have different variances.

A PC score may be standardized using:

[
Z_{PC_k}
========

\frac{PC_k-\overline{PC_k}}{SD(PC_k)}
]

This produces scores with approximately:

```text
Mean = 0
SD   = 1
```

This can be useful when downstream analysis requires PCs to be placed on comparable scales.

⚠️ Standardizing PC scores is **not an obligatory step of PCA itself**.

---

# 13. 🧲 Eigenvectors vs Loadings

This is one of the most commonly confused PCA concepts.

## 🧭 Eigenvectors

Eigenvectors define the component directions.

For a normalized eigenvector:

[
\sum_j v_{jk}^{2}=1
]

Example PC1 eigenvector:

```text
DBP      -0.53
SBP      -0.50
Weight    0.48
Height    0.49
```

---

## 🧲 Loadings

Under a common PCA convention for standardized variables:

[
Loading_{jk}
============

v_{jk}\sqrt{\lambda_k}
]

These loadings correspond to correlations between the original standardized variables and component scores.

Example:

| Variable | PC1 Loading |
| -------- | ----------: |
| DBP      |       -0.82 |
| SBP      |       -0.77 |
| Weight   |        0.75 |
| Height   |        0.77 |

Interpretation:

```text
|Loading| close to 1 → strong relationship
|Loading| close to 0 → weak relationship
```

---

### 🧠 Remember

```text
Eigenvalue  → How much variance?
Eigenvector → Which direction?
Score       → Where is each observation?
Loading     → How strongly is each variable associated with a PC?
```

---

# 14. 🔎 Interpreting Principal Components

## PC1

Example loadings:

```text
DBP      -0.82
SBP      -0.77
Weight   +0.75
Height   +0.77
```

Possible interpretation:

> 🩺 ↔️ ⚖️ **Blood pressure vs body size contrast**

Higher PC1 values correspond to relatively:

```text
Higher Weight / Height
Lower DBP / SBP
```

and lower PC1 values imply the opposite pattern.

---

## PC2

If all variables have substantial loadings in the same direction, PC2 may represent a more general **overall magnitude/common variation** pattern, depending on the actual loadings and dataset.

⚠️ Component names are interpretations, not mathematically generated labels.

Domain knowledge matters.

---

## ➕➖ A crucial fact about signs

The sign of an eigenvector is arbitrary.

If:

[
v
]

is an eigenvector, then:

[
-v
]

is equally valid.

Therefore:

```text
PC1 = [-0.53, -0.50, +0.48, +0.49]
```

and:

```text
PC1 = [+0.53, +0.50, -0.48, -0.49]
```

describe the **same PCA axis**, just pointing in opposite directions.

🔥 Do not attach intrinsic meaning to the absolute choice of positive versus negative orientation.

Interpret **relationships and contrasts**.

---

# 15. 🔄 Rotation and Varimax

Sometimes retained PCs are statistically valid but difficult to interpret.

Example:

| Variable |   PC1 |   PC2 |
| -------- | ----: | ----: |
| DBP      | -0.53 | -0.46 |
| SBP      | -0.50 | -0.52 |
| Weight   |  0.48 | -0.52 |
| Height   |  0.49 | -0.50 |

Several variables contribute substantially to both components.

This creates **cross-loading** and makes interpretation less clean.

---

## 🔄 Varimax rotation

Varimax is an **orthogonal rotation**.

Its goal is to produce a simpler loading structure by encouraging variables to have:

```text
High loading on one component
        +
Low loading on others
```

while keeping rotated axes orthogonal.

Conceptually:

```text
Original PC axes
       ↘
        \   ↗ PC2
         \ /
----------●---------- PC1
         /


Rotate retained axes
             │ RC1
             │
             │
─────────────●──────────── RC2
```

The coordinate system changes, but the retained subspace remains the same.

---

# 16. 🎯 Rotated Components

Example after Varimax rotation:

| Variable |       RC1 |       RC2 |
| -------- | --------: | --------: |
| DBP      | **-0.97** |      0.18 |
| SBP      | **-0.98** |      0.10 |
| Weight   |      0.09 | **-0.97** |
| Height   |      0.12 | **-0.97** |

Now interpretation becomes much cleaner.

### RC1 🩺

Strong contribution from:

```text
DBP
SBP
```

Therefore:

> **RC1 ≈ Blood Pressure Component**

### RC2 📏⚖️

Strong contribution from:

```text
Weight
Height
```

Therefore:

> **RC2 ≈ Body Size Component**

This is much easier to communicate.

---

# 17. 🔃 Rotated Scores

If (T) contains retained PCA scores and (R) is the rotation matrix, under the relevant rotation convention:

[
T_{rotated}=TR
]

So:

```text
Original retained scores
          ×
Rotation matrix
          ↓
Rotated scores
```

Example redistributed variances:

| Component | Variance |
| --------- | -------: |
| RC1       |     1.94 |
| RC2       |     1.92 |
| **Total** | **3.86** |

Before rotation:

[
2.41+1.45=3.86
]

After rotation:

[
1.94+1.92=3.86
]

Therefore:

> 🔒 **The total variance represented by the retained orthogonal subspace is preserved.**

But the variance can be redistributed between the rotated components.

---

## ⚠️ Important distinction

Rotation does **not** make PCA capture additional variance.

It primarily changes the orientation of the retained axes to make interpretation easier.

```text
Before rotation:
PC1 = 2.41
PC2 = 1.45

After rotation:
RC1 = 1.94
RC2 = 1.92

Total before = Total after = 3.86
```

---

# 18. 🚀 Post-PCA Analysis

PCA is often not the final analysis.

The resulting scores can be used for further analysis.

---

## 📊 1. Score Plot

Plot:

```text
PC2
 ↑
 │     ● ●
 │  ●
 │              ● ●
 │
 │ ●
 └──────────────────→ PC1
```

Useful for identifying:

* Clusters
* Outliers
* Trends
* Group separation
* Similar observations

---

## 🧲 2. Loading Plot

Shows how variables relate to components.

Useful for answering:

> Which original variables are driving PC1 and PC2?

---

## 🎯 3. Biplot

A biplot combines:

```text
Observation scores
        +
Variable directions/loadings
```

into one visualization.

It helps answer both:

> Where are the samples?

and:

> Which variables explain their positions?

---

## 🤖 4. Machine Learning

Instead of:

```text
X1, X2, X3, ... X100
```

we may use:

```text
PC1, PC2, ... PC10
```

as features.

Potential benefits include:

* Lower dimensionality
* Reduced multicollinearity
* Faster model training
* Noise reduction
* Easier visualization

⚠️ PCA does not automatically improve prediction. Important low-variance information can sometimes matter for the target variable.

---

## 🧩 5. Clustering

PCA scores can be used before:

* K-means
* Hierarchical clustering
* Gaussian mixture models

Example:

```text
Original:
100 correlated variables

        ↓ PCA

10 PCs

        ↓ clustering

Groups / patterns
```

---

# 19. ⚠️ Common PCA Mistakes

## ❌ Mistake 1: Ignoring scale

Running covariance-based PCA on variables with drastically different units can cause high-variance variables to dominate.

### ✅ Fix

Standardize when appropriate.

---

## ❌ Mistake 2: Thinking PC1 is always the "most important variable"

PC1 is not an original variable.

It is:

> A **linear combination** of variables that captures maximum variance.

---

## ❌ Mistake 3: Confusing loadings and scores

```text
Loadings → Variables
Scores   → Observations
```

---

## ❌ Mistake 4: Treating eigenvector signs as absolute

The entire eigenvector can be multiplied by (-1) without changing the PCA solution.

---

## ❌ Mistake 5: Assuming high variance means high predictive value

PCA does not know the prediction target (y).

It only examines variation in (X).

Therefore:

> High variance ≠ automatically useful for prediction.

---

## ❌ Mistake 6: Assuming PCA discovers causality

PCA finds variance/correlation structure.

It does **not** establish:

```text
X causes Y
```

---

## ❌ Mistake 7: Blindly applying the 80–90% rule

Explained variance is useful, but component selection should also consider:

* Research goals
* Interpretability
* Scree plot
* Parallel analysis
* Validation
* Downstream performance

---

## ❌ Mistake 8: Thinking rotation increases information

Rotation can improve interpretation.

It does not create new information.

---

# 20. 🧠 Complete PCA Story

Suppose we begin with:

```text
DBP
SBP
Weight
Height
```

### Step 1️⃣ — Standardize

```text
Raw variables
     ↓
Z-scores
```

Why?

> Put differently scaled variables onto comparable scales.

---

### Step 2️⃣ — Measure relationships

Calculate:

```text
Covariance matrix
      or
Correlation matrix
```

Why?

> Understand how variables vary together.

---

### Step 3️⃣ — Eigendecomposition

Solve:

[
C\mathbf{v}=\lambda\mathbf{v}
]

This gives:

```text
Eigenvectors → directions
Eigenvalues  → variance along those directions
```

---

### Step 4️⃣ — Construct PCs

```text
PC1 = weighted combination of variables
PC2 = another weighted combination
...
```

---

### Step 5️⃣ — Project observations

[
T=ZV
]

Now each person receives:

```text
PC1 score
PC2 score
PC3 score
...
```

---

### Step 6️⃣ — Rank PCs

Example:

```text
PC1 → 60.2%
PC2 → 36.2%
PC3 →  2.5%
PC4 →  1.1%
```

---

### Step 7️⃣ — Reduce dimensions

```text
PC1 + PC2 = 96.4%
```

So:

```text
4D
 ↓
2D
```

while retaining approximately 96.4% of total standardized variance.

---

### Step 8️⃣ — Interpret

Inspect:

```text
Eigenvectors
Loadings
Score plots
Biplots
```

---

### Step 9️⃣ — Optional rotation

If interpretation is unclear:

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

### Step 🔟 — Downstream analysis

Use scores for:

```text
📊 Visualization
🧩 Clustering
🤖 Machine learning
🔎 Outlier detection
🧬 Omics exploration
📉 Dimensionality reduction
```

---

# 21. 📝 Quick Cheat Sheet

| Concept                | Meaning                                                                        |
| ---------------------- | ------------------------------------------------------------------------------ |
| 📊 PCA                 | Dimensionality-reduction technique                                             |
| ⚖️ Standardization     | Places variables on comparable scales                                          |
| 🔗 Covariance          | How two variables vary together                                                |
| 🧭 Eigenvector         | Direction of a PC                                                              |
| 📈 Eigenvalue          | Variance captured by a PC                                                      |
| 🧩 Principal Component | Weighted linear combination of variables                                       |
| 📍 Score               | Position of an observation along a PC                                          |
| 🧲 Loading             | Association/correlation between variable and PC under standard PCA conventions |
| 📉 Explained Variance  | Percentage of total variance captured                                          |
| 🦵 Scree Plot          | Helps choose number of PCs                                                     |
| 1️⃣ Kaiser Criterion   | Often retain eigenvalues > 1 for correlation PCA                               |
| 🔄 Varimax             | Orthogonal rotation for simpler interpretation                                 |
| 🎯 Biplot              | Displays observations and variables together                                   |

---

# 22. 🌍 Applications of PCA

PCA is foundational in multivariate data analysis.

### 🧬 Biology / Omics

```text
Thousands of genes
       ↓ PCA
Few major expression patterns
```

Used in:

* Gene expression
* Proteomics
* Metabolomics
* Population genetics

---

### 🏭 Engineering

Useful for:

* Sensor-data analysis
* Process monitoring
* Fault detection
* Quality control
* Multivariate condition monitoring

---

### 🤖 Machine Learning

Useful for:

* Feature reduction
* Multicollinearity reduction
* Data visualization
* Preprocessing
* Compression

---

### 🖼️ Images

An image can contain thousands or millions of correlated pixel values.

PCA can represent much of the variation using fewer dimensions.

---

### 💰 Finance

Can help identify common variation across:

* Assets
* Interest rates
* Yield curves
* Economic indicators

---

# 23. 🎥 Recommended Video

## StatQuest — Principal Component Analysis (PCA), Step-by-Step

▶️ **YouTube:**
https://www.youtube.com/watch?v=FgakZw6K1QQ

StatQuest provides a particularly accessible visual explanation of:

* PCA intuition
* Variance
* Principal-component directions
* Eigenvectors
* Eigenvalues
* Dimensionality reduction

---

# 🧠 The One-Minute PCA Story

If you remember nothing else, remember this:

```text
Many correlated variables
          ↓
    Standardize
          ↓
Find directions of maximum variance
          ↓
    Eigenvectors
          ↓
Measure variance in each direction
          ↓
     Eigenvalues
          ↓
Project observations onto those directions
          ↓
       Scores
          ↓
Keep the important PCs
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

Order those axes by variance captured.

### 📍 Project

Place every observation onto the new axes.

### ✂️ Reduce

Discard directions containing relatively little variance.

### 🔎 Interpret

Use loadings, scores, plots, and domain knowledge to understand the structure.

---

## ⭐ Final Formula Map

```text
STANDARDIZATION

            x - μ
     z = ─────────
              σ


EIGENVALUE PROBLEM

     C v = λ v


PRINCIPAL COMPONENT

     PCₖ = Z vₖ


ALL PCA SCORES

     T = Z V


EXPLAINED VARIANCE

                  λₖ
     EVRₖ = ─────────────
              Σ λⱼ


LOADINGS
(common standardized-PCA convention)

     Lₖ = vₖ √λₖ


ORTHOGONAL ROTATION

     T_rotated = T R
```

---

> 💡 **PCA does not simply delete variables. It changes the coordinate system so that the most important variance in the data can be represented using fewer dimensions.**

**PCA in one sentence:** 📊
**Find the directions where the data varies most, project the data onto those directions, and keep only the directions carrying useful information.**
