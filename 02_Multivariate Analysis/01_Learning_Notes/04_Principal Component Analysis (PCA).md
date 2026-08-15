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
11. [How Many Components Should Be Retained?](#11--how-many-components-should-be-retained)
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

It converts a dataset containing many potentially correlated variables into a smaller set of new variables called:

> **Principal Components (PCs)**

These principal components:

* 📈 Capture as much variance as possible
* 🔗 Are mutually uncorrelated
* 🥇 Are ordered from most informative to least informative
* 📉 Can reduce the dimensionality of a dataset
* 🧩 Represent combinations of the original variables

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

These variables may not be independent.

For example:

* 🩺 DBP may correlate with SBP
* ⚖️ Weight may correlate with height
* 📏 Height and weight may both describe **body size**
* ❤️ Blood-pressure variables may share common physiological variation

This means four measured variables may contain fewer than four genuinely independent dimensions of information.

---

## 💡 What PCA Tries to Do

Suppose we have a cloud of observations in two dimensions:

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

The data clearly varies more strongly along a diagonal direction than along the original X or Y axes.

PCA effectively rotates the coordinate system:

```text
                     ↗ PC1
                  •
              •
          •
      •
  •

            ↖ PC2
```

The new axes are:

* **PC1** → direction of greatest variance
* **PC2** → direction of the next greatest variance
* **PC3** → next largest variance
* and so on

---

## 🥇 First Principal Component

The first principal component is chosen so that it captures the:

> **Maximum possible variance in the data**

---

## 🥈 Second Principal Component

The second principal component captures the:

> **Maximum remaining variance while remaining orthogonal to PC1**

The same principle continues for PC3, PC4, etc.

---

# 3. ⚖️ Why Standardization Matters

PCA is driven by **variance**.

That means variables with numerically larger variances can dominate the principal components.

Consider:

| Variable | Example Scale |
| -------- | ------------: |
| Weight   |         70 kg |
| Height   |        170 cm |
| Height   |        1.70 m |

Height in centimeters and height in meters represent the same biological information.

However, their numerical variances are completely different.

Example:

```text
Variance(weight)       ≈ 37.7
Variance(height in cm) ≈ 33
Variance(height in m)  ≈ 0.003
```

If PCA were performed directly on these differently scaled variables, variables with large numerical variance could dominate the result.

---

## 🔧 Z-Score Standardization

A common solution is to standardize every variable using a Z-score.

$$
z = \frac{x-\mu}{\sigma}
$$

where:

* $x$ = original observation
* $\mu$ = mean of the variable
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

| Variable |  Mean |  SD |
| -------- | ----: | --: |
| DBP      |  80.2 | 2.6 |
| SBP      | 130.0 | 2.5 |
| Weight   |  69.6 | 6.6 |
| Height   | 169.7 | 6.4 |

Suppose a person's DBP is 78.

Then:

$$
z_{\text{DBP}}
==============

\frac{78-80.2}{2.6}
$$

which produces the standardized DBP value.

---

## 🧠 Important Note

Standardization is strongly recommended when variables have:

* Different units
* Different numerical scales
* Very different variances

However:

> ⚠️ **Standardization is not mathematically mandatory for every PCA problem.**

PCA can also be performed directly on a covariance matrix when the original scales themselves are scientifically meaningful.

### 📌 Practical Rule

> If variables have different units or substantially different scales, standardize them before PCA unless there is a specific scientific reason not to.

---

# 4. 🗺️ Complete PCA Workflow

The complete PCA workflow can be represented as:

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

---

## 🔢 PCA Step-by-Step

1. 🧹 Prepare and clean the data
2. ⚖️ Standardize variables when appropriate
3. 🔗 Compute covariance or correlation matrix
4. 🧮 Calculate eigenvalues
5. 🧭 Calculate eigenvectors
6. 🧩 Construct principal components
7. 📍 Calculate PCA scores
8. 📊 Calculate explained variance
9. ✂️ Decide how many PCs to retain
10. 🔎 Interpret component loadings
11. 📉 Visualize the PCA
12. 🔄 Optionally rotate retained components
13. 🚀 Perform downstream analysis

---

# 5. 🔗 Covariance and Correlation

PCA needs information about how variables vary together.

---

## Covariance

For two variables $X$ and $Y$:

$$
\operatorname{Cov}(X,Y)
=======================

\frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}{n-1}
$$

where:

* $x_i$ = observation $i$ for variable $X$
* $y_i$ = observation $i$ for variable $Y$
* $\bar{x}$ = mean of $X$
* $\bar{y}$ = mean of $Y$
* $n$ = number of observations

---

## 🧠 Covariance Interpretation

```text
Positive covariance

X ↑
Y ↑

The variables tend to increase together.
```

```text
Negative covariance

X ↑
Y ↓

One variable tends to increase while the other decreases.
```

```text
Covariance ≈ 0

No strong linear co-movement.
```

---

## 📦 Covariance Matrix

For several variables, all pairwise covariances are stored in a covariance matrix.

For two variables:

$$
\mathbf{C}
==========

\begin{bmatrix}
\operatorname{Var}(X_1) & \operatorname{Cov}(X_1,X_2) \
\operatorname{Cov}(X_2,X_1) & \operatorname{Var}(X_2)
\end{bmatrix}
$$

For our four variables, conceptually:

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

## 🔗 Correlation Matrix

Correlation removes the scale effect.

For variables $X$ and $Y$:

$$
r_{XY}
======

\frac{\operatorname{Cov}(X,Y)}
{\sigma_X\sigma_Y}
$$

Correlation ranges between:

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

> PCA using standardized data is equivalent to PCA using the **correlation matrix**.

---

# 6. 🧮 Eigenvalues and Eigenvectors

This is the mathematical heart of PCA.

Suppose the covariance or correlation matrix is:

$$
\mathbf{C}
$$

PCA solves:

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

> **The direction of a principal component**

Each eigenvector defines one new PCA axis.

---

## 📊 Eigenvalue

An eigenvalue tells us:

> **How much variance is captured along that eigenvector direction**

Therefore:

```text
Eigenvector → Direction
Eigenvalue  → Variance captured
```

---

## 🧠 Memory Trick

> 🧭 **Vector = direction**

> 📊 **Value = amount of variance**

---

## 📈 Ordering Components

PCA orders eigenvalues from largest to smallest:

$$
\lambda_1
\ge
\lambda_2
\ge
\lambda_3
\ge
\cdots
\ge
\lambda_p
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

Suppose the standardized variables are:

* $Z_{\text{DBP}}$
* $Z_{\text{SBP}}$
* $Z_{\text{Weight}}$
* $Z_{\text{Height}}$

Then:

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

The coefficients:

$$
w_1,w_2,w_3,w_4
$$

come from the eigenvector corresponding to PC1.

---

## 📋 Example PC1

Suppose:

$$
PC_1
====

-0.53Z_{\text{DBP}}
-0.50Z_{\text{SBP}}
+0.48Z_{\text{Weight}}
+0.49Z_{\text{Height}}
$$

This means:

| Variable | PC1 Weight |
| -------- | ---------: |
| DBP      |      -0.53 |
| SBP      |      -0.50 |
| Weight   |      +0.48 |
| Height   |      +0.49 |

---

## 🔍 How Do We Read the Coefficients?

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

So an increasing PC1 score roughly corresponds to:

```text
↑ Weight
↑ Height

↓ DBP
↓ SBP
```

This suggests that PC1 describes a contrast between:

> 🩺 **Blood Pressure** ↔ ⚖️ **Body Size**

---

# 8. 🧱 Component Matrix

Suppose the PCA produces:

| Variable |   PC1 |   PC2 |   PC3 |   PC4 |
| -------- | ----: | ----: | ----: | ----: |
| DBP      | -0.53 | -0.46 |  0.14 | -0.70 |
| SBP      | -0.50 | -0.52 | -0.16 |  0.68 |
| Weight   |  0.48 | -0.52 |  0.69 |  0.12 |
| Height   |  0.49 | -0.50 | -0.69 | -0.18 |

Each **column** represents an eigenvector.

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
\sum_{j=1}^{p}v_{jk}^{2}
========================

1
$$

For example, for PC1:

$$
(-0.53)^2
+
(-0.50)^2
+
(0.48)^2
+
(0.49)^2
\approx
1
$$

The small difference is due to rounding.

---

# 9. 📍 PCA Scores

This is one of the most important PCA distinctions.

> **Eigenvectors describe the component directions.**

> **Scores describe where observations lie along those directions.**

---

## 🧍 Example Observation

Suppose one person has standardized measurements:

```text
DBP     = z₁
SBP     = z₂
Weight  = z₃
Height  = z₄
```

If PC1 is:

$$
PC_1
====

-0.53Z_{\text{DBP}}
-0.50Z_{\text{SBP}}
+0.48Z_{\text{Weight}}
+0.49Z_{\text{Height}}
$$

then this person's PC1 score is:

$$
\operatorname{Score}_{PC1}
==========================

-0.53z_1
-0.50z_2
+0.48z_3
+0.49z_4
$$

---

## 🧮 Matrix Form

If:

* $\mathbf{Z}$ = standardized data matrix
* $\mathbf{V}$ = matrix containing eigenvectors

then the PCA scores are:

$$
\mathbf{T}
==========

\mathbf{Z}\mathbf{V}
$$

where:

* $\mathbf{T}$ = PCA score matrix

Conceptually:

```text
Standardized Data
        ×
Eigenvector Matrix
        ↓
    PCA Scores
```

---

## 🧠 What Does a Score Mean?

A PCA score tells us:

> **Where an observation lies along a particular principal-component axis.**

Example:

```text
Person A → PC1 = -2.1
Person B → PC1 =  0.3
Person C → PC1 =  2.4
```

Person A and Person C are far apart along PC1.

That means their profiles differ strongly according to the pattern represented by PC1.

---

# 10. 📊 Explained Variance

Suppose PCA produces the following eigenvalues:

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
\text{Explained Variance Ratio}_k
=================================

\frac{\lambda_k}
{\sum_{j=1}^{p}\lambda_j}
$$

For standardized PCA with four variables:

$$
\sum_{j=1}^{4}\lambda_j
\approx
4
$$

because each standardized variable has variance approximately 1.

---

## 📌 PC1

$$
\frac{2.41}{4}
\approx
0.6025
$$

Therefore:

$$
PC1
\approx
60.2%
$$

---

## 📌 PC2

$$
\frac{1.45}{4}
\approx
0.3625
$$

Therefore:

$$
PC2
\approx
36.2%
$$

---

## 🔥 PC1 + PC2

$$
60.2%
+
36.2%
=====

96.4%
$$

Therefore:

> **Two dimensions preserve approximately 96.4% of the variance originally contained in four standardized variables.**

This is the essence of dimensionality reduction.

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

# 11. ✂️ How Many Components Should Be Retained?

There is no single universal rule.

Several criteria are commonly used together.

---

## 1️⃣ Cumulative Explained Variance

A common heuristic is to retain enough PCs to explain approximately:

```text
80%
90%
95%
```

of the total variance.

Here:

$$
PC1 + PC2
=========

96.4%
$$

Therefore:

> ✅ PC1 and PC2 would be retained.

---

## 2️⃣ Kaiser Criterion

For PCA performed on a correlation matrix or standardized variables:

> **Retain components with eigenvalues greater than 1.**

Why 1?

Each standardized original variable contributes approximately:

$$
\operatorname{Var}(Z)=1
$$

So a component with:

$$
\lambda > 1
$$

captures more variance than one average standardized original variable.

Here:

```text
PC1 = 2.41 ✅
PC2 = 1.45 ✅
PC3 = 0.10 ❌
PC4 = 0.04 ❌
```

Therefore:

> ✅ Retain PC1 and PC2.

### ⚠️ Important

The Kaiser criterion is a **heuristic**, not a universal rule.

---

## 3️⃣ Scree Plot

A scree plot shows:

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

Here there is a large drop after PC2.

Therefore:

> ✅ Retain PC1 and PC2.

---

## 4️⃣ Parallel Analysis

A more rigorous approach is **parallel analysis**.

It compares observed eigenvalues with eigenvalues obtained from random datasets.

Keep a component only when its observed eigenvalue is larger than expected from random noise.

---

## 5️⃣ Domain Knowledge

Statistical rules should not replace scientific reasoning.

A component may explain less variance but still represent an important biological mechanism.

Therefore, component retention should consider:

* Explained variance
* Scree plot
* Parallel analysis
* Interpretability
* Biological relevance
* Downstream performance

---

# 12. 📐 Standardized PC Scores

PC scores themselves may have different variances.

A PC score can be standardized:

$$
Z_{PC_k}
========

\frac{PC_k-\overline{PC_k}}
{SD(PC_k)}
$$

After standardization:

```text
Mean ≈ 0
SD   ≈ 1
```

This can be useful if PC scores will later be combined or compared on equal scales.

> ⚠️ Standardizing PCA scores is **not a mandatory PCA step**.

---

# 13. 🧲 Eigenvectors vs Loadings

This is one of the most commonly confused concepts in PCA.

---

## 🧭 Eigenvectors

Eigenvectors define the directions of the principal components.

Example PC1 eigenvector:

```text
DBP      -0.53
SBP      -0.50
Weight   +0.48
Height   +0.49
```

The normalized eigenvector satisfies:

$$
\sum_j v_{jk}^{2}
=================

1
$$

---

## 🧲 Loadings

Under a common standardized-PCA convention:

$$
l_{jk}
======

v_{jk}\sqrt{\lambda_k}
$$

where:

* $l_{jk}$ = loading for variable $j$ on component $k$
* $v_{jk}$ = eigenvector coefficient
* $\lambda_k$ = eigenvalue

For standardized variables, these loadings can be interpreted as correlations between the original variables and the PC scores.

---

## 📋 Example PC1 Loadings

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
Strong relationship with PC

|Loading| close to 0
        ↓
Weak relationship with PC
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

Suppose the PC1 loadings are:

```text
DBP      -0.82
SBP      -0.77
Weight   +0.75
Height   +0.77
```

We can see two groups:

```text
Negative side:

DBP
SBP

Positive side:

Weight
Height
```

Therefore, PC1 can be interpreted as:

> 🩺 **Blood Pressure vs Body Size**

---

## 📍 Interpreting PC1 Scores

A high PC1 score might represent:

```text
Higher Weight
Higher Height
Lower DBP
Lower SBP
```

A low PC1 score might represent:

```text
Lower Weight
Lower Height
Higher DBP
Higher SBP
```

---

## PC2 Interpretation

Suppose all four variables have loadings in approximately the same direction on PC2.

Then PC2 may represent:

> **Overall magnitude/common variation**

The exact biological interpretation depends on the actual loading values and the scientific context.

---

## ➕➖ Important: Eigenvector Signs Are Arbitrary

Suppose an eigenvector is:

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

is equally valid.

Both describe the same PCA axis.

Therefore:

> ⚠️ Do not assign intrinsic biological meaning to whether a component happens to be positive or negative.

Focus on:

> **Relative relationships among variables.**

---

# 15. 🔄 Why Rotation Is Used

Sometimes PCA components explain variance well but are difficult to interpret.

Consider:

| Variable |   PC1 |   PC2 |
| -------- | ----: | ----: |
| DBP      | -0.53 | -0.46 |
| SBP      | -0.50 | -0.52 |
| Weight   |  0.48 | -0.52 |
| Height   |  0.49 | -0.50 |

Several variables contribute substantially to both components.

This is called:

> **Cross-loading**

Cross-loading makes component interpretation less clear.

---

## 🎯 Goal of Rotation

Rotation tries to produce a simpler structure.

Ideally:

```text
Variable A → High loading on Component 1
             Low loading on Component 2

Variable B → Low loading on Component 1
             High loading on Component 2
```

This can make the latent structure easier to interpret.

---

# 16. 🔄 Varimax Rotation

**Varimax** is an orthogonal rotation method.

Its goal is to:

* Maximize large loadings
* Minimize small/intermediate loadings
* Produce simpler components
* Keep rotated components orthogonal

Conceptually:

```text
Original Components
        ↓
     Rotation
        ↓
Cleaner Loading Structure
```

---

## 📋 Before Rotation

| Variable |   PC1 |   PC2 |
| -------- | ----: | ----: |
| DBP      | -0.53 | -0.46 |
| SBP      | -0.50 | -0.52 |
| Weight   |  0.48 | -0.52 |
| Height   |  0.49 | -0.50 |

Interpretation is not immediately clean.

---

## 📋 After Varimax Rotation

| Variable |       RC1 |       RC2 |
| -------- | --------: | --------: |
| DBP      | **-0.97** |      0.18 |
| SBP      | **-0.98** |      0.10 |
| Weight   |      0.09 | **-0.97** |
| Height   |      0.12 | **-0.97** |

Now the interpretation is much clearer.

---

## 🩺 RC1

High absolute loadings:

```text
DBP
SBP
```

Therefore:

> **RC1 ≈ Blood Pressure Component**

---

## ⚖️ RC2

High absolute loadings:

```text
Weight
Height
```

Therefore:

> **RC2 ≈ Body Size Component**

---

## 🧠 Important Rotation Concept

Rotation does not create new information.

It changes the orientation of the retained component axes.

```text
Before Rotation

PC1 + PC2
      ↓
Same 2D subspace
      ↓
RC1 + RC2

After Rotation
```

The retained subspace remains the same.

---

# 17. 🔃 Rotated Scores

Suppose:

* $\mathbf{T}$ = original retained PCA score matrix
* $\mathbf{R}$ = rotation matrix

Then, under the corresponding orthogonal rotation convention:

$$
\mathbf{T}_{\text{rotated}}
===========================

\mathbf{T}\mathbf{R}
$$

Conceptually:

```text
Original PC Scores
        ×
Rotation Matrix
        ↓
Rotated Scores
```

---

## 📊 Variance Before Rotation

Suppose:

```text
PC1 variance = 2.41
PC2 variance = 1.45
```

Total:

$$
2.41+1.45
=========

3.86
$$

---

## 📊 Variance After Rotation

Suppose:

```text
RC1 variance = 1.94
RC2 variance = 1.92
```

Then:

$$
1.94+1.92
=========

3.86
$$

Therefore:

> 🔒 **The total variance represented by the retained orthogonal subspace is preserved.**

However:

> The variance may be redistributed among the rotated components.

---

# 18. 🚀 Post-PCA Analysis

PCA is often not the final analysis.

The resulting scores and loadings can be used for further investigation.

---

## 📊 1. Score Plot

A common PCA plot is:

> **PC1 Score vs PC2 Score**

Example:

```text
PC2
 ↑

 │        ● ●
 │   ●
 │                    ●
 │                ●
 │
 │ ●
 └────────────────────────→ PC1
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

A loading plot shows how variables contribute to PCs.

It helps answer:

> **Which variables are responsible for the observed sample patterns?**

---

## 🎯 3. Biplot

A PCA biplot combines:

```text
Sample Scores
      +
Variable Loadings
```

into one visualization.

This helps answer two questions simultaneously:

1. Where are the observations?
2. Which variables explain those positions?

---

## 🔎 Interpreting Vectors in a Biplot

Conceptually:

```text
Long vector
    ↓
Strong contribution to displayed PCs

Short vector
    ↓
Weak contribution to displayed PCs
```

Angles between variable vectors also provide information about correlation.

```text
Small angle
    ↓
Positive correlation

≈ 90°
    ↓
Weak correlation

≈ 180°
    ↓
Negative correlation
```

---

## 🤖 4. PCA Before Machine Learning

Instead of training a model using:

```text
X1
X2
X3
...
X100
```

we might use:

```text
PC1
PC2
...
PC10
```

Potential benefits include:

* Reduced dimensionality
* Reduced multicollinearity
* Lower computational cost
* Noise reduction
* Easier visualization

---

## ⚠️ Important Prediction Warning

PCA does not use the target variable $y$.

It only analyzes variation in the predictor matrix $\mathbf{X}$.

Therefore:

> **High variance does not automatically mean high predictive importance.**

A low-variance feature could still be highly predictive of the target.

---

## 🧩 5. PCA Before Clustering

A common workflow is:

```text
100 correlated variables
          ↓
         PCA
          ↓
10 important PCs
          ↓
      Clustering
          ↓
 Biological Groups
```

PCA can reduce noise and redundant dimensions before clustering.

---

# 19. ⚠️ Common PCA Mistakes

## ❌ Mistake 1: Ignoring Variable Scale

If variables have very different units, covariance-based PCA may be dominated by variables with large numerical variance.

### ✅ Solution

Standardize when scientifically appropriate.

---

## ❌ Mistake 2: Thinking PC1 Is an Original Variable

PC1 is not one original variable.

It is a:

> **Weighted linear combination of the original variables**

---

## ❌ Mistake 3: Confusing Scores and Loadings

Remember:

```text
Scores
  ↓
Observations

Loadings
  ↓
Variables
```

---

## ❌ Mistake 4: Confusing Eigenvalues and Eigenvectors

```text
Eigenvalue
    ↓
Variance captured

Eigenvector
    ↓
Direction
```

---

## ❌ Mistake 5: Treating Eigenvector Signs as Absolute

The sign may be reversed without changing the underlying PCA solution.

---

## ❌ Mistake 6: Assuming High Variance Means High Predictive Value

PCA is unsupervised.

It does not know the target variable.

---

## ❌ Mistake 7: Thinking PCA Finds Causality

PCA identifies:

* Variance structure
* Correlation structure
* Low-dimensional patterns

It does **not** prove:

```text
X causes Y
```

---

## ❌ Mistake 8: Automatically Using the 80–90% Rule

The explained-variance threshold is only a heuristic.

Also consider:

* Scree plot
* Parallel analysis
* Domain knowledge
* Interpretability
* Validation
* Downstream model performance

---

## ❌ Mistake 9: Thinking Rotation Adds Information

Rotation improves interpretability.

It does **not** create additional information.

---

## ❌ Mistake 10: Interpreting PCs Without Looking at Loadings

A PC number alone has no biological meaning.

You must inspect the variables contributing strongly to that component.

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

For every measurement:

$$
z
=

\frac{x-\mu}{\sigma}
$$

Why?

> Put variables onto comparable numerical scales.

---

## Step 2️⃣ — Calculate Covariance or Correlation Matrix

Construct:

$$
\mathbf{C}
$$

Why?

> Describe how variables vary together.

---

## Step 3️⃣ — Solve the Eigenvalue Problem

$$
\mathbf{C}\mathbf{v}
====================

\lambda\mathbf{v}
$$

This gives:

```text
Eigenvector
    ↓
Direction of PC

Eigenvalue
    ↓
Variance captured
```

---

## Step 4️⃣ — Order Components

Order components by eigenvalue:

$$
\lambda_1
\ge
\lambda_2
\ge
\cdots
\ge
\lambda_p
$$

Therefore:

```text
PC1 captures most variance
PC2 captures second-most
PC3 captures third-most
...
```

---

## Step 5️⃣ — Construct Principal Components

Example:

$$
PC_1
====

-0.53Z_{\text{DBP}}
-0.50Z_{\text{SBP}}
+0.48Z_{\text{Weight}}
+0.49Z_{\text{Height}}
$$

---

## Step 6️⃣ — Project Observations

Calculate:

$$
\mathbf{T}
==========

\mathbf{Z}\mathbf{V}
$$

Each sample receives:

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

## Step 8️⃣ — Reduce Dimensionality

$$
PC1+PC2
=======

96.4%
$$

Therefore:

```text
4 dimensions
      ↓
     PCA
      ↓
2 dimensions
```

while retaining approximately 96.4% of total standardized variance.

---

## Step 9️⃣ — Interpret Components

Inspect:

```text
Eigenvectors
Loadings
Scores
Score Plot
Loading Plot
Biplot
```

---

## Step 🔟 — Optional Rotation

If the retained PCs are difficult to interpret:

```text
PC1 + PC2
    ↓
 Varimax
    ↓
RC1 + RC2
```

Example interpretation:

```text
RC1 → Blood Pressure
RC2 → Body Size
```

---

## Step 1️⃣1️⃣ — Downstream Analysis

Use PCA for:

* 📊 Visualization
* 🧩 Clustering
* 🤖 Machine learning
* 🔎 Outlier detection
* 🧬 Omics analysis
* 📉 Dimensionality reduction
* 🏭 Process monitoring

---

# 21. 🧮 PCA Formula Sheet

## 1. Standardization

$$
z
=

\frac{x-\mu}{\sigma}
$$

---

## 2. Sample Covariance

$$
\operatorname{Cov}(X,Y)
=======================

\frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}
{n-1}
$$

---

## 3. Correlation

$$
r_{XY}
======

\frac{\operatorname{Cov}(X,Y)}
{\sigma_X\sigma_Y}
$$

---

## 4. Eigenvalue Equation

$$
\mathbf{C}\mathbf{v}
====================

\lambda\mathbf{v}
$$

---

## 5. Principal Component

$$
PC_k
====

\mathbf{Z}\mathbf{v}_k
$$

---

## 6. PCA Score Matrix

$$
\mathbf{T}
==========

\mathbf{Z}\mathbf{V}
$$

---

## 7. Explained Variance Ratio

$$
EVR_k
=====

\frac{\lambda_k}
{\sum_j\lambda_j}
$$

---

## 8. Cumulative Explained Variance

$$
CEV_m
=====

\frac{\sum_{k=1}^{m}\lambda_k}
{\sum_{j=1}^{p}\lambda_j}
$$

---

## 9. Loading

Under a common standardized-PCA convention:

$$
l_{jk}
======

v_{jk}\sqrt{\lambda_k}
$$

---

## 10. Standardized PC Score

$$
Z_{PC_k}
========

\frac{PC_k-\overline{PC_k}}
{SD(PC_k)}
$$

---

## 11. Orthogonal Rotated Scores

$$
\mathbf{T}_{\text{rotated}}
===========================

\mathbf{T}\mathbf{R}
$$

---

# 22. 📝 Quick Cheat Sheet

| Concept                | Meaning                                         |
| ---------------------- | ----------------------------------------------- |
| 📊 PCA                 | Dimensionality-reduction technique              |
| ⚖️ Standardization     | Places variables on comparable scales           |
| 🔗 Covariance          | Describes how variables vary together           |
| 🔗 Correlation         | Standardized linear relationship                |
| 🧭 Eigenvector         | Direction of a principal component              |
| 📈 Eigenvalue          | Variance captured by a principal component      |
| 🧩 Principal Component | Weighted combination of original variables      |
| 📍 Score               | Position of an observation along a PC           |
| 🧲 Loading             | Strength of a variable's relationship with a PC |
| 📉 Explained Variance  | Fraction of total variance captured             |
| 📈 Cumulative Variance | Total variance explained by first $k$ PCs       |
| 🦵 Scree Plot          | Helps determine number of PCs                   |
| 1️⃣ Kaiser Criterion   | Often retain $\lambda>1$ for correlation PCA    |
| 🔄 Varimax             | Orthogonal rotation for interpretability        |
| 🎯 Score Plot          | Shows observations in PCA space                 |
| 🧲 Loading Plot        | Shows variable contributions                    |
| 🎯 Biplot              | Shows observations and variables together       |

---

# 23. 🌍 Applications of PCA

## 🧬 Biology and Omics

PCA is widely used in:

* Gene-expression analysis
* RNA-seq
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

If samples cluster by sequencing batch rather than biology, that may indicate a technical artifact.

---

## 🏭 Engineering

PCA can be used for:

* Sensor-data analysis
* Process monitoring
* Fault detection
* Quality control
* Condition monitoring
* Multivariate process control

---

## 🤖 Machine Learning

Applications include:

* Feature reduction
* Multicollinearity reduction
* Noise reduction
* Visualization
* Preprocessing
* Compression

---

## 🖼️ Image Processing

Images contain highly correlated pixel information.

PCA can represent images using fewer dimensions.

Conceptually:

```text
Thousands of Pixels
        ↓
       PCA
        ↓
Few Important Components
```

---

## 💰 Finance

PCA can identify common factors across:

* Stocks
* Bond yields
* Interest rates
* Macroeconomic indicators
* Yield curves

---

# 24. 🏁 Final Mental Model

Think of PCA as:

> 🔄 **Rotate → Rank → Project → Reduce → Interpret**

---

## 🔄 Rotate

Find new directions that better describe variation in the data.

---

## 📊 Rank

Order those directions according to the amount of variance captured.

---

## 📍 Project

Project observations onto the new axes.

---

## ✂️ Reduce

Discard low-variance directions if they contribute little useful information.

---

## 🔎 Interpret

Use:

* Eigenvectors
* Loadings
* Scores
* Scree plots
* Score plots
* Loading plots
* Biplots
* Domain knowledge

to understand the data structure.

---

# 🧠 PCA in One Minute

```text
Many correlated variables
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
Project observations
          ↓
       PC Scores
          ↓
Calculate Explained Variance
          ↓
Keep Important Components
          ↓
Reduce Dimensionality
          ↓
Interpret Loadings
          ↓
Visualize / Cluster / Model
```

---

# ⭐ Most Important PCA Relationships

```text
Eigenvector
    ↓
Direction of a PC


Eigenvalue
    ↓
Variance captured by a PC


Score
    ↓
Position of a sample along a PC


Loading
    ↓
Relationship between a variable and a PC
```

---

# ✅ Final Takeaway

> **PCA transforms correlated variables into a new set of orthogonal directions that capture decreasing amounts of variance.**

The essential idea is:

```text
Original Correlated Variables
            ↓
           PCA
            ↓
New Orthogonal Components
            ↓
Rank by Explained Variance
            ↓
Keep Important Components
            ↓
Simpler Representation of Data
```

### 📌 PCA in one sentence

> **Find the directions where the data varies most, project the observations onto those directions, and retain the components that preserve the important structure of the dataset.**

---

# 25. 🎥 Recommended Video

## StatQuest: Principal Component Analysis (PCA), Step-by-Step

▶️ **YouTube**

https://www.youtube.com/watch?v=FgakZw6K1QQ

The video provides an intuitive visual explanation of:

* Principal components
* Variance
* Eigenvectors
* Eigenvalues
* Projection
* Dimensionality reduction
* PCA interpretation

---

## 📚 Recommended Learning Order

```text
1. Understand variance
        ↓
2. Understand covariance
        ↓
3. Understand standardization
        ↓
4. Understand eigenvectors
        ↓
5. Understand eigenvalues
        ↓
6. Understand PC scores
        ↓
7. Understand explained variance
        ↓
8. Understand loadings
        ↓
9. Understand score plots / biplots
        ↓
10. Understand rotation
```

> 🎯 Once these concepts are connected, PCA becomes much easier to understand than the mathematics initially suggests.
