# 📊 Principal Component Analysis (PCA)

### From Basic Intuition → Mathematics → Interpretation → Post-Analysis

> 🎯 **Goal:** Understand what PCA does, why each step exists, how the mathematics works, and how to interpret the final results.

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
23. [Applications of PCA](#23--applications-of-pca)
24. [Final Mental Model](#24--final-mental-model)
25. [Recommended Video](#25--recommended-video)

---

# 1. 🧠 What Is PCA?

**PCA = Principal Component Analysis**

PCA is an **unsupervised dimensionality-reduction technique**.

It transforms many potentially correlated variables into a smaller number of new variables called:

> **Principal Components (PCs)**

Principal components:

* 📈 Capture as much variance as possible
* 🔗 Are mutually uncorrelated
* 🥇 Are ordered from most informative to least informative
* 📉 Can reduce dimensionality
* 🧩 Are linear combinations of the original variables

In simple words:

> **PCA summarizes many related variables using fewer informative dimensions.**

---

# 2. ❓ Why Do We Need PCA?

Real-world datasets often contain many variables.

Example:

| Person | DBP | SBP | Weight | Height |
| ------ | --: | --: | -----: | -----: |
| A      |  78 | 128 |     65 |    165 |
| B      |  82 | 132 |     75 |    175 |
| C      |  80 | 130 |     70 |    170 |

These variables may be correlated.

For example:

* 🩺 DBP may correlate with SBP
* ❤️ SBP may correlate with DBP
* ⚖️ Weight may correlate with height
* 📏 Weight and height may represent a common concept such as body size

Therefore, four measured variables may contain fewer than four truly independent dimensions of information.

---

## 💡 PCA Intuition

Imagine that observations form a diagonal cloud:

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

The greatest variation is along the diagonal rather than along the original X or Y axes.

PCA finds new axes:

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

The first principal component captures the:

> **Maximum possible variance in the data**

### 🥈 PC2

The second principal component captures the:

> **Maximum remaining variance while remaining orthogonal to PC1**

The same idea continues for PC3, PC4, and so on.

---

# 3. ⚖️ Why Standardization Matters

PCA is driven by **variance**.

Suppose we measure:

| Variable |  Scale |
| -------- | -----: |
| Weight   |  70 kg |
| Height   | 170 cm |
| Height   | 1.70 m |

Height in centimeters and height in meters represent the same biological property, but their numerical variances are completely different.

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
* $\mu$ = mean
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

If DBP = 78:

$$
z = \frac{78-80.2}{2.6}
$$

Therefore:

$$
z \approx -0.85
$$

The value is approximately **0.85 standard deviations below the mean**.

---

## 🧠 Is Standardization Always Required?

Standardization is especially important when variables have:

* Different units
* Different scales
* Very different variances

However:

> **Standardization is not mathematically mandatory for every PCA problem.**

If the original measurement scales themselves are scientifically meaningful, PCA may be performed directly on the covariance matrix.

### 📌 Practical Rule

> If variables have different units or very different scales, standardize them unless you have a specific scientific reason not to.

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
Visualize
   ↓
Optional Rotation
   ↓
Downstream Analysis
```

### Step-by-step

1. 🧹 Prepare the data
2. ⚖️ Standardize variables when appropriate
3. 🔗 Calculate the covariance or correlation matrix
4. 🧮 Calculate eigenvalues
5. 🧭 Calculate eigenvectors
6. 🧩 Construct principal components
7. 📍 Calculate PCA scores
8. 📊 Calculate explained variance
9. ✂️ Decide how many PCs to retain
10. 🔎 Interpret component loadings
11. 📉 Visualize scores and loadings
12. 🔄 Optionally rotate retained components
13. 🚀 Perform downstream analysis

---

# 5. 🔗 Covariance and Correlation

PCA needs information about how variables vary together.

---

## Covariance

For variables $X$ and $Y$:

$$
Cov(X,Y) = \frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}{n-1}
$$

where:

* $x_i$ = observation $i$ for variable X
* $y_i$ = observation $i$ for variable Y
* $\bar{x}$ = mean of X
* $\bar{y}$ = mean of Y
* $n$ = number of observations

---

## 🧠 Covariance Interpretation

### Positive covariance

```text
X ↑
Y ↑

Variables tend to increase together.
```

### Negative covariance

```text
X ↑
Y ↓

One variable tends to increase
while the other decreases.
```

### Covariance near zero

```text
Covariance ≈ 0

No strong linear co-movement.
```

---

## 📦 Covariance Matrix

For two variables, the covariance matrix conceptually contains:

|        |         X1 |         X2 |
| ------ | ---------: | ---------: |
| **X1** |    Var(X1) | Cov(X1,X2) |
| **X2** | Cov(X2,X1) |    Var(X2) |

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
r_{XY} = \frac{Cov(X,Y)}{\sigma_X\sigma_Y}
$$

The correlation coefficient satisfies:

$$
-1 \le r \le 1
$$

Interpretation:

```text
r ≈ +1  → Strong positive relationship

r ≈  0  → Weak or no linear relationship

r ≈ -1  → Strong negative relationship
```

When all variables are standardized:

> **PCA on standardized variables is equivalent to PCA based on the correlation matrix.**

---

# 6. 🧮 Eigenvalues and Eigenvectors

This is the mathematical heart of PCA.

Let the covariance or correlation matrix be $C$.

PCA solves:

$$
Cv = \lambda v
$$

where:

* $C$ = covariance or correlation matrix
* $v$ = eigenvector
* $\lambda$ = eigenvalue

---

## 🧭 Eigenvector

An eigenvector tells us:

> **The direction of a principal component**

Each eigenvector defines one PCA axis.

---

## 📊 Eigenvalue

An eigenvalue tells us:

> **How much variance exists along that eigenvector direction**

Remember:

```text
Eigenvector → Direction

Eigenvalue  → Variance captured
```

### 🧠 Memory Trick

> 🧭 **Vector = direction**
> 📊 **Value = variance**

---

## 📈 Ordering Eigenvalues

PCA orders eigenvalues from largest to smallest:

$$
\lambda_1 \ge \lambda_2 \ge \lambda_3 \ge \cdots \ge \lambda_p
$$

Therefore:

```text
Largest eigenvalue
        ↓
       PC1

Second-largest eigenvalue
        ↓
       PC2

Third-largest eigenvalue
        ↓
       PC3
```

---

# 7. 🧩 Principal Components

A principal component is a **linear combination of the original variables**.

Let:

```text
Z1 = standardized DBP
Z2 = standardized SBP
Z3 = standardized Weight
Z4 = standardized Height
```

Then PC1 can be written as:

$$
PC_1 = w_1Z_1 + w_2Z_2 + w_3Z_3 + w_4Z_4
$$

where:

* $w_1$
* $w_2$
* $w_3$
* $w_4$

are the eigenvector coefficients.

---

## 📋 Example PC1

Suppose:

$$
PC_1 = -0.53Z_1 - 0.50Z_2 + 0.48Z_3 + 0.49Z_4
$$

where:

```text
Z1 = DBP
Z2 = SBP
Z3 = Weight
Z4 = Height
```

The component weights are therefore:

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

Therefore, increasing PC1 approximately corresponds to:

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

Suppose PCA produces:

| Variable |   PC1 |   PC2 |   PC3 |   PC4 |
| -------- | ----: | ----: | ----: | ----: |
| DBP      | -0.53 | -0.46 |  0.14 | -0.70 |
| SBP      | -0.50 | -0.52 | -0.16 |  0.68 |
| Weight   |  0.48 | -0.52 |  0.69 |  0.12 |
| Height   |  0.49 | -0.50 | -0.69 | -0.18 |

Each column represents an eigenvector.

```text
Column PC1 → Eigenvector 1
Column PC2 → Eigenvector 2
Column PC3 → Eigenvector 3
Column PC4 → Eigenvector 4
```

---

## Normalized Eigenvectors

Eigenvectors are normally normalized so that:

$$
\sum_{j=1}^{p}v_{jk}^{2} = 1
$$

For PC1:

$$
(-0.53)^2 + (-0.50)^2 + (0.48)^2 + (0.49)^2 \approx 1
$$

Any small difference is due to rounding.

---

# 9. 📍 PCA Scores

This distinction is extremely important:

> **Eigenvectors describe component directions.**

> **Scores describe observations projected onto those directions.**

Suppose one observation has:

```text
DBP     = z1
SBP     = z2
Weight  = z3
Height  = z4
```

Then its PC1 score is:

$$
Score_{PC1} = -0.53z_1 - 0.50z_2 + 0.48z_3 + 0.49z_4
$$

---

## 🧮 Matrix Form

Let:

* $Z$ = standardized data matrix
* $V$ = eigenvector matrix
* $T$ = score matrix

Then:

$$
T = ZV
$$

Conceptually:

```text
Standardized Data
        ×
Eigenvectors
        ↓
     PC Scores
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

> **PC1 and PC2 preserve approximately 96.4% of the total standardized variance.**

```text
4 Original Variables
        ↓
       PCA
        ↓
2 Principal Components
        ↓
≈ 96.4% Variance Retained
```

---

# 11. ✂️ How Many Components Should We Keep?

There is no single universal rule.

Several criteria can be considered together.

---

## 1️⃣ Cumulative Explained Variance

Common heuristic thresholds are:

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

> ✅ PC1 and PC2 would be sufficient using this criterion.

---

## 2️⃣ Kaiser Criterion

For PCA on standardized variables or a correlation matrix:

> **Retain components with eigenvalues greater than 1.**

Why?

Each standardized original variable has approximately:

$$
Var(Z) = 1
$$

Therefore, a component with:

$$
\lambda > 1
$$

explains more variance than one average standardized variable.

Example:

```text
PC1 = 2.41 ✅
PC2 = 1.45 ✅
PC3 = 0.10 ❌
PC4 = 0.04 ❌
```

Therefore:

> ✅ Retain PC1 and PC2.

### ⚠️ Important

The Kaiser criterion is a **heuristic**, not a universal law.

---

## 3️⃣ Scree Plot

A scree plot displays:

> **Eigenvalue vs Principal Component Number**

Example:

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

> 🦵 **Elbow Point**

Here, the large drop occurs after PC2.

Therefore:

> ✅ Retain PC1 and PC2.

---

## 4️⃣ Parallel Analysis

Parallel analysis compares observed eigenvalues with eigenvalues obtained from random data.

Keep a component when:

```text
Observed eigenvalue
        >
Random-data eigenvalue
```

This can be more rigorous than relying only on the Kaiser criterion.

---

## 5️⃣ Scientific Context

Also consider:

* Biological importance
* Interpretability
* Scree plot
* Parallel analysis
* Reconstruction error
* Cross-validation
* Downstream performance

---

# 12. 📐 Standardized PC Scores

PC scores can themselves be standardized.

A simple notation is:

$$
Z_{PC_k} = \frac{PC_k-\overline{PC_k}}{s_{PC_k}}
$$

where:

* $\overline{PC_k}$ = mean PC score
* $s_{PC_k}$ = standard deviation of PC scores

After standardization:

```text
Mean ≈ 0
SD   ≈ 1
```

> ⚠️ Standardizing PC scores is **not a mandatory PCA step**.

---

# 13. 🧲 Eigenvectors vs Loadings

These concepts are related but not identical.

---

## 🧭 Eigenvectors

Eigenvectors define component directions.

Example PC1 eigenvector:

```text
DBP      -0.53
SBP      -0.50
Weight   +0.48
Height   +0.49
```

Normalized eigenvectors satisfy:

$$
\sum_j v_{jk}^{2} = 1
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

For standardized variables, these loadings can be interpreted as correlations between the original variables and the corresponding PC scores.

---

## 📋 Example

| Variable | PC1 Loading |
| -------- | ----------: |
| DBP      |       -0.82 |
| SBP      |       -0.77 |
| Weight   |       +0.75 |
| Height   |       +0.77 |

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

Two groups appear:

```text
Negative side:

DBP
SBP


Positive side:

Weight
Height
```

Therefore PC1 may represent:

> 🩺 **Blood Pressure vs Body Size**

---

## High PC1 Score

A high PC1 score may correspond to:

```text
Higher Weight
Higher Height
Lower DBP
Lower SBP
```

---

## Low PC1 Score

A low PC1 score may correspond to:

```text
Lower Weight
Lower Height
Higher DBP
Higher SBP
```

---

## ➕➖ Eigenvector Signs Are Arbitrary

Suppose an eigenvector is:

```text
v = [-0.53, -0.50, +0.48, +0.49]
```

Then:

```text
-v = [+0.53, +0.50, -0.48, -0.49]
```

is equally valid.

Both describe the same PCA axis pointing in opposite directions.

Therefore:

> ⚠️ Do not attach biological meaning to the absolute positive or negative sign of a PC.

Interpret the:

> **Relative relationships among variables.**

---

# 15. 🔄 Why Rotation Is Used

Sometimes retained PCA components are mathematically useful but difficult to interpret.

Example:

| Variable |   PC1 |   PC2 |
| -------- | ----: | ----: |
| DBP      | -0.53 | -0.46 |
| SBP      | -0.50 | -0.52 |
| Weight   |  0.48 | -0.52 |
| Height   |  0.49 | -0.50 |

Several variables contribute substantially to both components.

This is often described as:

> **Cross-loading**

---

## 🎯 Goal of Rotation

Rotation tries to produce a simpler structure.

Ideally:

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

This makes the components easier to interpret.

---

# 16. 🔄 Varimax Rotation

**Varimax** is an orthogonal rotation method.

Its goal is to:

* Increase large loadings
* Reduce intermediate loadings
* Create a simpler loading structure
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

Now interpretation is much clearer.

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

* $T$ = retained PCA score matrix
* $R$ = rotation matrix
* $T_R$ = rotated score matrix

Then:

$$
T_R = TR
$$

Conceptually:

```text
Original PCA Scores
        ×
Rotation Matrix
        ↓
Rotated Scores
```

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

> 🔒 **The total variance represented by the retained orthogonal subspace is preserved.**

The variance can, however, be redistributed between the rotated components.

---

# 18. 🚀 Post-PCA Analysis

PCA is often followed by additional analysis.

---

## 📊 1. Score Plot

A common PCA visualization plots:

> **PC1 Score vs PC2 Score**

Example:

```text
PC2
 ↑

 │        ● ●
 │   ●
 │                  ●
 │              ●
 │
 │ ●
 └──────────────────────→ PC1
```

A score plot can reveal:

* Clusters
* Outliers
* Group separation
* Trends
* Similar samples
* Batch effects

---

## 🧲 2. Loading Plot

A loading plot helps answer:

> **Which original variables are driving PC1, PC2, etc.?**

---

## 🎯 3. Biplot

A PCA biplot combines:

```text
Observation Scores
        +
Variable Loadings
```

It allows us to examine:

* Sample positions
* Variable directions
* Sample similarities
* Variable relationships

---

## 📐 Interpreting Biplot Angles

Approximately:

```text
Small angle
    ↓
Positive correlation
```

```text
90°
 ↓
Weak linear correlation
```

```text
180°
  ↓
Negative correlation
```

---

## 🤖 4. PCA Before Machine Learning

Instead of training a model with:

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
* Reduced multicollinearity
* Faster computation
* Noise reduction
* Easier visualization

---

## ⚠️ Important Prediction Warning

PCA does not use the target variable $y$.

It analyzes variation only in the predictor matrix $X$.

Therefore:

> **High variance does not automatically mean high predictive importance.**

A low-variance feature could still be highly predictive of the target.

---

## 🧩 5. PCA Before Clustering

A common workflow is:

```text
100 Correlated Variables
          ↓
         PCA
          ↓
10 Principal Components
          ↓
      Clustering
          ↓
        Groups
```

PCA can remove redundant dimensions before clustering.

---

# 19. ⚠️ Common PCA Mistakes

## ❌ Mistake 1: Ignoring Scale

Different measurement units can distort covariance-based PCA.

### ✅ Fix

Standardize when appropriate.

---

## ❌ Mistake 2: Thinking PC1 Is an Original Variable

PC1 is not one original feature.

It is:

> **A weighted linear combination of the original variables**

---

## ❌ Mistake 3: Confusing Scores and Loadings

```text
Scores   → Observations

Loadings → Variables
```

---

## ❌ Mistake 4: Confusing Eigenvalues and Eigenvectors

```text
Eigenvalue  → Variance captured

Eigenvector → Direction
```

---

## ❌ Mistake 5: Treating Eigenvector Signs as Absolute

Eigenvector signs can be reversed without changing the underlying PCA solution.

---

## ❌ Mistake 6: Assuming High Variance Means High Predictive Value

PCA is unsupervised.

It does not know the prediction target.

---

## ❌ Mistake 7: Assuming PCA Finds Causality

PCA identifies:

* Variance structure
* Correlation structure
* Low-dimensional patterns

It does **not** prove:

```text
X causes Y
```

---

## ❌ Mistake 8: Blindly Using an 80–90% Rule

Explained variance should be considered together with:

* Scree plot
* Parallel analysis
* Domain knowledge
* Interpretability
* Validation
* Downstream performance

---

## ❌ Mistake 9: Thinking Rotation Adds Information

Rotation can improve interpretability.

It does not create additional information.

---

## ❌ Mistake 10: Interpreting PCs Without Examining Loadings

A PC number itself has no biological meaning.

You must inspect which variables contribute strongly to the component.

---

# 20. 🧠 Complete PCA Story

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

> Put variables onto comparable numerical scales.

---

## Step 2️⃣ — Calculate Covariance or Correlation

Build the matrix describing how variables vary together.

```text
DBP
SBP
Weight
Height
   ↓
Covariance / Correlation Matrix
```

---

## Step 3️⃣ — Solve the Eigenvalue Problem

$$
Cv = \lambda v
$$

This gives:

```text
Eigenvectors → Directions

Eigenvalues  → Variance along those directions
```

---

## Step 4️⃣ — Order Components

$$
\lambda_1 \ge \lambda_2 \ge \cdots \ge \lambda_p
$$

Therefore:

```text
PC1 → Most variance
PC2 → Second-most variance
PC3 → Third-most variance
...
```

---

## Step 5️⃣ — Construct Principal Components

Example:

$$
PC_1 = -0.53Z_1 - 0.50Z_2 + 0.48Z_3 + 0.49Z_4
$$

where:

```text
Z1 = standardized DBP
Z2 = standardized SBP
Z3 = standardized Weight
Z4 = standardized Height
```

---

## Step 6️⃣ — Calculate Scores

$$
T = ZV
$$

Each observation receives:

```text
PC1 Score
PC2 Score
PC3 Score
...
```

---

## Step 7️⃣ — Calculate Explained Variance

Example:

```text
PC1 → 60.2%
PC2 → 36.2%
PC3 →  2.5%
PC4 →  1.1%
```

---

## Step 8️⃣ — Reduce Dimensions

$$
PC1 + PC2 = 96.4%
$$

Therefore:

```text
4 dimensions
      ↓
2 dimensions
```

while preserving approximately 96.4% of the variance.

---

## Step 9️⃣ — Interpret Components

Inspect:

* Eigenvectors
* Loadings
* Scores
* Scree plots
* Score plots
* Loading plots
* Biplots

---

## Step 🔟 — Optional Rotation

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

## Step 1️⃣1️⃣ — Downstream Analysis

Use PCA results for:

* 📊 Visualization
* 🧩 Clustering
* 🤖 Machine learning
* 🔎 Outlier detection
* 🧬 Omics analysis
* 🏭 Process monitoring

---

# 21. 🧮 PCA Formula Sheet

## Standardization

$$
z = \frac{x-\mu}{\sigma}
$$

---

## Covariance

$$
Cov(X,Y) = \frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}{n-1}
$$

---

## Correlation

$$
r_{XY} = \frac{Cov(X,Y)}{\sigma_X\sigma_Y}
$$

---

## Eigenvalue Equation

$$
Cv = \lambda v
$$

---

## Principal Component

$$
PC_k = Zv_k
$$

---

## PCA Score Matrix

$$
T = ZV
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
Z_{PC_k} = \frac{PC_k-\overline{PC_k}}{s_{PC_k}}
$$

---

## Rotated Scores

$$
T_R = TR
$$

---

# 22. 📝 Quick Cheat Sheet

| Concept                    | Meaning                                  |
| -------------------------- | ---------------------------------------- |
| 📊 **PCA**                 | Dimensionality reduction                 |
| ⚖️ **Standardization**     | Places variables on comparable scales    |
| 🔗 **Covariance**          | How two variables vary together          |
| 🔗 **Correlation**         | Standardized linear relationship         |
| 🧭 **Eigenvector**         | Direction of a principal component       |
| 📈 **Eigenvalue**          | Variance captured by a component         |
| 🧩 **Principal Component** | Linear combination of variables          |
| 📍 **Score**               | Position of an observation along a PC    |
| 🧲 **Loading**             | Relationship between a variable and a PC |
| 📉 **Explained Variance**  | Fraction of total variance captured      |
| 📈 **Cumulative Variance** | Variance captured by first several PCs   |
| 🦵 **Scree Plot**          | Helps select number of PCs               |
| 1️⃣ **Kaiser Criterion**   | Often retain eigenvalues > 1             |
| 🔄 **Varimax**             | Orthogonal rotation for interpretation   |
| 🎯 **Score Plot**          | Displays observations in PCA space       |
| 🧲 **Loading Plot**        | Displays variable contributions          |
| 🎯 **Biplot**              | Combines scores and loadings             |

---

# 23. 🌍 Applications of PCA

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

In omics data, PCA can reveal whether samples separate according to:

```text
Biological Condition
        or
Technical Batch
```

If samples cluster mainly by sequencing run, laboratory batch, or processing date rather than biological condition, this may indicate a technical batch effect.

---

## 🏭 Engineering

PCA can be used for:

* Sensor-data analysis
* Fault detection
* Process monitoring
* Quality control
* Condition monitoring
* Multivariate process control

---

## 🤖 Machine Learning

PCA can be used for:

* Feature reduction
* Multicollinearity reduction
* Noise reduction
* Visualization
* Preprocessing
* Compression

---

## 🖼️ Image Processing

Images contain many correlated pixel values.

```text
Thousands of Pixels
        ↓
       PCA
        ↓
Few Important Components
```

PCA can approximate the original image information using fewer dimensions.

---

## 💰 Finance

PCA can identify common factors across:

* Stocks
* Bond yields
* Interest rates
* Yield curves
* Macroeconomic indicators

---

# 24. 🏁 Final Mental Model

Think of PCA as:

> 🔄 **Rotate → Rank → Project → Reduce → Interpret**

---

## 🔄 Rotate

Find new directions that better describe variation in the data.

---

## 📊 Rank

Order those directions according to the variance captured.

---

## 📍 Project

Project every observation onto the new axes.

---

## ✂️ Reduce

Remove directions containing relatively little useful variance.

---

## 🔎 Interpret

Use:

* Eigenvalues
* Eigenvectors
* Scores
* Loadings
* Scree plots
* Score plots
* Loading plots
* Biplots
* Domain knowledge

to understand the resulting structure.

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
       PC Scores
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

> **PCA transforms correlated variables into orthogonal principal components ordered according to the amount of variance they explain.**

In one line:

```text
Original Correlated Variables
            ↓
           PCA
            ↓
Orthogonal Principal Components
            ↓
Rank by Explained Variance
            ↓
Keep Important Components
            ↓
Simpler Representation
```

### 📌 PCA in one sentence

> **Find the directions in which the data varies most, project the observations onto those directions, and retain the components that preserve the important structure of the dataset.**

---

# 25. 🎥 Recommended Video

## StatQuest: Principal Component Analysis (PCA), Step-by-Step

▶️ **YouTube**

https://www.youtube.com/watch?v=FgakZw6K1QQ

Recommended learning order:

```text
Variance
   ↓
Covariance
   ↓
Correlation
   ↓
Standardization
   ↓
Eigenvectors
   ↓
Eigenvalues
   ↓
Principal Components
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

> 🎯 Once these concepts connect, PCA becomes much easier to understand.
