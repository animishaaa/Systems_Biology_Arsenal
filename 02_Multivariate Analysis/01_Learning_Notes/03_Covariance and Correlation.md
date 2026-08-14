# 📊 Covariance and Correlation  
## Complete Notes: Variance, Covariance, Correlation, Matrices & Standardization

Covariance and correlation are fundamental concepts in **multivariate statistics**.

They help us understand how variables behave **together** and form the mathematical foundation for techniques such as:

- 📊 Principal Component Analysis (PCA)
- 🧬 Gene expression analysis
- 🤖 Machine learning
- 📈 Multivariate regression
- 🧩 Clustering
- 🎯 Linear Discriminant Analysis (LDA)

---

# 1. 🔍 Why Covariance and Correlation Matter

In multivariate statistics, we usually measure several variables for the same observations.

For example:

| Patient | Weight | Height | Blood Pressure | Temperature |
|---|---:|---:|---:|---:|
| 1 | 61 | 157 | 120 | 37.0 |
| 2 | 62 | 168 | 125 | 36.8 |
| 3 | 73 | 170 | 130 | 37.1 |

We may want to know:

- 🔗 Do two variables change together?
- 📈 Does one variable increase when another increases?
- 📉 Does one variable decrease when another increases?
- 🚫 Are the variables linearly unrelated?

Examples include:

```text
Body Weight ↔ Body Height
Gene Expression ↔ Phenotype
Blood Pressure ↔ Age
Temperature ↔ Disease Severity
```

Two important statistical tools help answer these questions:

```text
Covariance
    ↓
Measures joint variation

Correlation
    ↓
Measures standardized linear association
```

---

# 2. 📏 Variance – The Foundation

Before understanding covariance, we need to understand **variance**.

## What Is Variance?

Variance measures how much the values of a variable **spread around their mean**.

If observations are close to the mean:

```text
Small spread
    ↓
Small variance
```

If observations are far from the mean:

```text
Large spread
    ↓
Large variance
```

---

# 3. 🧮 Mean

For observations:

```math
x_1,x_2,\ldots,x_n
```

the sample mean is:

```math
\bar{x}
=
\frac{1}{n}
\sum_{i=1}^{n}x_i
```

where:

- $x_i$ = individual observation
- $\bar{x}$ = sample mean
- $n$ = number of observations

---

# 4. 📐 Sample Variance

The sample variance is:

```math
s_x^2
=
\frac{1}{n-1}
\sum_{i=1}^{n}
(x_i-\bar{x})^2
```

where:

- $x_i$ = individual observation
- $\bar{x}$ = sample mean
- $n$ = number of observations
- $x_i-\bar{x}$ = deviation from the mean
- $s_x^2$ = sample variance

> 📌 We use $n-1$ when calculating the variance from a **sample**.

---

# 5. 🧠 Understanding Variance Step by Step

Variance is calculated through the following process:

```text
Raw observations
      ↓
Calculate mean
      ↓
Subtract mean from each observation
      ↓
Calculate deviations
      ↓
Square deviations
      ↓
Add squared deviations
      ↓
Divide by n - 1
      ↓
Variance
```

Mathematically:

```math
x_i
\rightarrow
(x_i-\bar{x})
\rightarrow
(x_i-\bar{x})^2
\rightarrow
\sum(x_i-\bar{x})^2
\rightarrow
s^2
```

---

# 6. 📏 Example: Variance

Suppose height measurements in decimeters are:

```math
x=
\begin{bmatrix}
16 \\
17 \\
18
\end{bmatrix}
```

The mean is:

```math
\bar{x}
=
\frac{16+17+18}{3}
=
17
```

The deviations are:

```math
\begin{bmatrix}
16-17 \\
17-17 \\
18-17
\end{bmatrix}
=
\begin{bmatrix}
-1 \\
0 \\
1
\end{bmatrix}
```

Square the deviations:

```math
\begin{bmatrix}
(-1)^2 \\
0^2 \\
1^2
\end{bmatrix}
=
\begin{bmatrix}
1 \\
0 \\
1
\end{bmatrix}
```

Therefore:

```math
s^2
=
\frac{1+0+1}{3-1}
=
1
```

So the sample variance is:

```math
\boxed{s^2=1}
```

---

# 7. 📏 Standard Deviation

Variance is measured in **squared units**.

For example:

```text
Height measured in cm
        ↓
Variance measured in cm²
```

This can make variance difficult to interpret directly.

The **standard deviation** solves this problem.

---

## Mathematical Definition

Standard deviation is the square root of variance:

```math
s
=
\sqrt{s^2}
```

or:

```math
s
=
\sqrt{
\frac{1}{n-1}
\sum_{i=1}^{n}
(x_i-\bar{x})^2
}
```

---

## 💡 Why Standard Deviation Is Useful

Standard deviation:

- 📏 Has the same units as the original variable
- 📊 Describes the spread of observations
- 🧠 Is easier to interpret than variance

For example:

```text
Height → cm
Standard deviation → cm
Variance → cm²
```

---

# 8. 🔗 Covariance – Measuring Joint Variation

## What Is Covariance?

Variance describes the variation of **one variable**.

Covariance extends this idea to **two variables**.

```text
Variance
   ↓
How does ONE variable vary?

Covariance
   ↓
How do TWO variables vary together?
```

Covariance measures whether two variables tend to move together.

---

# 9. 🧮 Sample Covariance Formula

For two variables $X$ and $Y$:

```math
s_{xy}
=
\operatorname{Cov}(X,Y)
=
\frac{1}{n-1}
\sum_{i=1}^{n}
(x_i-\bar{x})
(y_i-\bar{y})
```

where:

- $x_i$ = observation from variable $X$
- $y_i$ = observation from variable $Y$
- $\bar{x}$ = mean of $X$
- $\bar{y}$ = mean of $Y$
- $n$ = number of paired observations

---

# 10. 🧠 Understanding Covariance Step by Step

The calculation follows:

```text
X values                   Y values
   ↓                          ↓
Mean of X                  Mean of Y
   ↓                          ↓
xᵢ - x̄                     yᵢ - ȳ
        ↘                  ↙
          Multiply deviations
                  ↓
       (xᵢ-x̄)(yᵢ-ȳ)
                  ↓
               Sum
                  ↓
            Divide by n-1
                  ↓
             Covariance
```

---

# 11. ➕ Positive Covariance

Positive covariance occurs when the variables tend to move in the **same direction**.

```text
X increases
    ↓
Y tends to increase
```

and:

```text
X decreases
    ↓
Y tends to decrease
```

Example:

```text
Height ↑
Weight ↑
```

This may produce:

```math
\operatorname{Cov}(X,Y)>0
```

---

# 12. ➖ Negative Covariance

Negative covariance occurs when the variables tend to move in **opposite directions**.

```text
X increases
    ↓
Y tends to decrease
```

Example:

```text
X ↑
Y ↓
```

This produces:

```math
\operatorname{Cov}(X,Y)<0
```

---

# 13. 0️⃣ Zero Covariance

If:

```math
\operatorname{Cov}(X,Y)\approx0
```

there is little or no **linear association** between the variables.

> ⚠️ Zero covariance does **not necessarily mean the variables are completely unrelated**. A strong nonlinear relationship can exist even when covariance is zero.

---

# 14. 📊 Interpretation of Covariance

| Covariance | Interpretation |
|---|---|
| $>0$ | 📈 Variables tend to move together |
| $<0$ | 📉 Variables tend to move oppositely |
| $\approx0$ | ➖ Little or no linear association |

---

# 15. ⚠️ Limitation of Covariance

The magnitude of covariance depends on the **units and scale** of the variables.

Suppose:

```text
Weight → kg
Height → cm
```

Then covariance has units:

```text
kg × cm
```

If height is changed from centimeters to meters, the numerical covariance changes.

Therefore:

> 📌 The **sign** of covariance is easy to interpret, but its magnitude is difficult to compare across differently scaled variables.

This motivates **correlation**.

---

# 16. 🔗 Pearson Correlation Coefficient

## What Is Correlation?

Correlation is essentially **standardized covariance**.

The Pearson correlation coefficient is:

```math
r_{xy}
=
\frac{
\operatorname{Cov}(X,Y)
}{
s_xs_y
}
```

or:

```math
r_{xy}
=
\frac{
s_{xy}
}{
s_xs_y
}
```

where:

- $s_{xy}$ = covariance between $X$ and $Y$
- $s_x$ = standard deviation of $X$
- $s_y$ = standard deviation of $Y$

---

# 17. 🎯 Range of Pearson Correlation

Correlation is bounded between:

```math
-1\leq r\leq1
```

Therefore:

| $r$ | Meaning |
|---:|---|
| $+1$ | 📈 Perfect positive linear relationship |
| $0$ | ➖ No linear relationship |
| $-1$ | 📉 Perfect negative linear relationship |

---

# 18. 🧠 Correlation Scale

A useful conceptual scale is:

```text
-1                  0                  +1
│-------------------│-------------------│
Strong negative     No linear          Strong positive
relationship        relationship       relationship
```

Values closer to either:

```math
-1
```

or:

```math
+1
```

indicate a stronger **linear association**.

Values closer to:

```math
0
```

indicate a weaker linear association.

> 📌 The exact labels "weak", "moderate", and "strong" depend on the scientific field and context.

---

# 19. 🆚 Covariance vs Correlation

| Property | Covariance | Correlation |
|---|---|---|
| Measures joint variation | ✅ | ✅ |
| Shows direction | ✅ | ✅ |
| Standardized | ❌ | ✅ |
| Fixed range | ❌ | $[-1,1]$ |
| Depends on units | ✅ | ❌ |
| Easy magnitude interpretation | ❌ | ✅ |
| Scale-independent | ❌ | ✅ |

---

# 20. ⚖️ Worked Example: Body Weight & Height

Suppose we have:

| Person | Weight (kg) | Height (cm) |
|---:|---:|---:|
| 1 | 61 | 157 |
| 2 | 62 | 168 |
| 3 | 73 | 170 |
| 4 | 74 | 181 |
| 5 | 82 | 191 |
| 6 | 86 | 185 |

Represent the variables as:

```math
X=
\begin{bmatrix}
61\\
62\\
73\\
74\\
82\\
86
\end{bmatrix}
```

and:

```math
Y=
\begin{bmatrix}
157\\
168\\
170\\
181\\
191\\
185
\end{bmatrix}
```

---

# 21. 🧮 Step 1: Calculate the Means

For weight:

```math
\bar{x}
=
\frac{
61+62+73+74+82+86
}{6}
```

```math
\bar{x}
=
73
```

For height:

```math
\bar{y}
=
\frac{
157+168+170+181+191+185
}{6}
```

```math
\bar{y}
=
175.33
```

approximately.

---

# 22. 🧮 Step 2: Calculate Deviations

For each observation calculate:

```math
x_i-\bar{x}
```

and:

```math
y_i-\bar{y}
```

For example, for the first observation:

```math
61-73=-12
```

and:

```math
157-175.33=-18.33
```

Both deviations are negative.

Therefore their product is positive:

```math
(-12)(-18.33)>0
```

This contributes to a **positive covariance**.

---

# 23. 🧮 Step 3: Calculate Covariance

Use:

```math
s_{xy}
=
\frac{
\sum_{i=1}^{n}
(x_i-\bar{x})(y_i-\bar{y})
}{
n-1
}
```

For these data:

```math
s_{xy}
\approx
132.4
```

Therefore:

```math
\boxed{
\operatorname{Cov}(X,Y)\approx132.4
}
```

The positive value indicates that weight and height tend to increase together.

---

# 24. 📐 Step 4: Calculate Standard Deviations

The sample standard deviations are approximately:

```math
s_x\approx10.04
```

and:

```math
s_y\approx12.47
```

---

# 25. 🔗 Step 5: Calculate Correlation

Use:

```math
r
=
\frac{s_{xy}}{s_xs_y}
```

Therefore:

```math
r
=
\frac{
132.4
}{
(10.04)(12.47)
}
```

which gives approximately:

```math
\boxed{r\approx0.94}
```

📌 This indicates a **strong positive linear relationship** between weight and height in this small example dataset.

---

# 26. 📈 Visual Interpretation with Scatter Plots

A scatter plot is one of the best ways to understand correlation.

Each observation is represented by:

```math
(x_i,y_i)
```

---

## 🟢 Perfect Positive Correlation

```text
Y
│             ●
│          ●
│       ●
│    ●
│ ●
└──────────────── X
```

The observations lie exactly on an increasing straight line.

```math
r=1
```

---

# 27. 📈 Strong Positive Correlation

```text
Y
│             ●
│        ● ●
│      ●
│   ●    ●
│ ●
└──────────────── X
```

The observations approximately follow an increasing line.

For example:

```math
r\approx0.79
```

---

# 28. 🔹 Weak Positive Correlation

```text
Y
│       ●      ●
│  ●
│          ●
│     ●
│ ●            ●
└──────────────── X
```

A weak upward tendency may exist.

For example:

```math
r\approx0.38
```

---

# 29. 0️⃣ No Linear Correlation

```text
Y
│   ●       ●
│       ●
│ ●           ●
│      ●
│          ●
└──────────────── X
```

There is no obvious linear trend.

```math
r\approx0
```

---

# 30. 📉 Negative Correlation

```text
Y
│ ●
│    ●
│       ●
│          ●
│             ●
└──────────────── X
```

As $X$ increases, $Y$ decreases.

Therefore:

```math
r<0
```

A perfect negative linear relationship has:

```math
r=-1
```

---

# 31. ⚠️ Correlation Measures Linear Association

Pearson correlation measures **linear** association.

For example, imagine a perfect U-shaped relationship:

```text
Y
│ ●           ●
│   ●       ●
│
│      ●
└──────────────── X
```

There may be a very strong relationship between $X$ and $Y$, but Pearson correlation could still be close to:

```math
r=0
```

Therefore:

> 📌 **Correlation near zero does not automatically mean "no relationship." It means little or no linear relationship.**

---

# 32. 📊 Covariance Matrix

When we have more than two variables, calculating every covariance separately becomes inconvenient.

Instead, we construct a **covariance matrix**.

Suppose we have three variables:

```math
X_1,\ X_2,\ X_3
```

The covariance matrix is:

```math
S =
\begin{bmatrix}
\operatorname{Var}(X_1)
&
\operatorname{Cov}(X_1,X_2)
&
\operatorname{Cov}(X_1,X_3)
\\
\operatorname{Cov}(X_2,X_1)
&
\operatorname{Var}(X_2)
&
\operatorname{Cov}(X_2,X_3)
\\
\operatorname{Cov}(X_3,X_1)
&
\operatorname{Cov}(X_3,X_2)
&
\operatorname{Var}(X_3)
\end{bmatrix}
```

---

# 33. 🔍 Structure of a Covariance Matrix

The diagonal contains **variances**:

```math
S_{ii}
=
\operatorname{Var}(X_i)
```

The off-diagonal elements contain **covariances**:

```math
S_{ij}
=
\operatorname{Cov}(X_i,X_j)
```

Therefore:

```text
               Variable 1    Variable 2    Variable 3

Variable 1     Variance       Covariance     Covariance

Variable 2     Covariance     Variance       Covariance

Variable 3     Covariance     Covariance     Variance
```

---

# 34. 🪞 Covariance Matrix Is Symmetric

Covariance satisfies:

```math
\operatorname{Cov}(X,Y)
=
\operatorname{Cov}(Y,X)
```

Therefore:

```math
S=S^T
```

For example:

```math
S =
\begin{bmatrix}
4 & 2 & -1 \\
2 & 9 & 3 \\
-1 & 3 & 16
\end{bmatrix}
```

Notice:

```math
S_{12}=S_{21}=2
```

and:

```math
S_{13}=S_{31}=-1
```

Therefore, the matrix is symmetric.

---

# 35. 🧠 Covariance Matrix – Key Properties

A covariance matrix has several important properties:

- 📐 It is square
- 🪞 It is symmetric
- 📊 Diagonal entries are variances
- 🔗 Off-diagonal entries are covariances
- ➕ Diagonal entries are non-negative
- ⭐ Its eigenvalues are non-negative, apart from tiny numerical rounding errors

These properties become extremely important in **PCA**.

---

# 36. 🔗 Correlation Matrix

A correlation matrix has the same structure as a covariance matrix, but contains **correlations instead of covariances**.

For three variables:

```math
R =
\begin{bmatrix}
1 & r_{12} & r_{13} \\
r_{21} & 1 & r_{23} \\
r_{31} & r_{32} & 1
\end{bmatrix}
```

where:

```math
r_{ij}
=
\operatorname{Corr}(X_i,X_j)
```

---

# 37. 1️⃣ Why Is the Diagonal Always 1?

The correlation of a variable with itself is:

```math
\operatorname{Corr}(X,X)
=
\frac{
\operatorname{Cov}(X,X)
}{
s_xs_x
}
```

But:

```math
\operatorname{Cov}(X,X)
=
\operatorname{Var}(X)
=
s_x^2
```

Therefore:

```math
\operatorname{Corr}(X,X)
=
\frac{s_x^2}{s_x^2}
=
1
```

So:

```math
r_{ii}=1
```

---

# 38. 🪞 Correlation Matrix Is Symmetric

Because:

```math
\operatorname{Corr}(X,Y)
=
\operatorname{Corr}(Y,X)
```

we have:

```math
R=R^T
```

Therefore:

```math
r_{ij}=r_{ji}
```

---

# 39. 🆚 Covariance Matrix vs Correlation Matrix

Suppose:

```math
S =
\begin{bmatrix}
100 & 20 \\
20 & 25
\end{bmatrix}
```

The diagonal contains variances.

A corresponding correlation matrix might be:

```math
R =
\begin{bmatrix}
1 & 0.40 \\
0.40 & 1
\end{bmatrix}
```

The major difference is:

```text
Covariance Matrix
      ↓
Depends on measurement scale

Correlation Matrix
      ↓
Standardized and scale-independent
```

---

# 40. 📏 Standardization of Data

## Why Standardize?

Multivariate datasets often contain variables measured in different units.

For example:

| Variable | Unit |
|---|---|
| Weight | kg |
| Height | cm |
| Blood pressure | mmHg |
| Temperature | °C |
| Gene expression | arbitrary units |

A variable with a large numerical scale can dominate calculations based on raw variance.

Standardization removes these scale differences.

---

# 41. 🧮 Standardization Formula

The standardized value, or **z-score**, is:

```math
z_i
=
\frac{
x_i-\bar{x}
}{
s_x
}
```

where:

- $x_i$ = original observation
- $\bar{x}$ = mean
- $s_x$ = standard deviation
- $z_i$ = standardized observation

---

# 42. 🧠 Standardization Step by Step

The process is:

```text
Original data
      ↓
Subtract mean
      ↓
Centered data
      ↓
Divide by standard deviation
      ↓
Standardized data
```

Mathematically:

```math
x_i
\rightarrow
x_i-\bar{x}
\rightarrow
\frac{x_i-\bar{x}}{s_x}
```

---

# 43. 1️⃣ Stage 1: Original Data

Suppose:

```math
X=
\begin{bmatrix}
10\\
20\\
30
\end{bmatrix}
```

The mean is:

```math
\bar{x}=20
```

---

# 44. 2️⃣ Stage 2: Center the Data

Subtract the mean:

```math
X-\bar{x}
=
\begin{bmatrix}
10-20\\
20-20\\
30-20
\end{bmatrix}
```

Therefore:

```math
X_{\text{centered}}
=
\begin{bmatrix}
-10\\
0\\
10
\end{bmatrix}
```

The centered data have:

```math
\text{Mean}=0
```

---

# 45. 3️⃣ Stage 3: Divide by Standard Deviation

The sample standard deviation is:

```math
s=10
```

Therefore:

```math
Z
=
\frac{
X-\bar{x}
}{
s
}
```

giving:

```math
Z=
\begin{bmatrix}
-1\\
0\\
1
\end{bmatrix}
```

After standardization:

```math
\boxed{\text{Mean}=0}
```

and:

```math
\boxed{\text{SD}=1}
```

---

# 46. 🔑 Standardization – Key Result

For standardized variables:

```math
Z_X
=
\frac{X-\bar{X}}{s_X}
```

and:

```math
Z_Y
=
\frac{Y-\bar{Y}}{s_Y}
```

their covariance is:

```math
\operatorname{Cov}(Z_X,Z_Y)
=
\frac{
\operatorname{Cov}(X,Y)
}{
s_Xs_Y
}
```

But this is exactly the correlation:

```math
\operatorname{Corr}(X,Y)
=
\frac{
\operatorname{Cov}(X,Y)
}{
s_Xs_Y
}
```

Therefore:

```math
\boxed{
\operatorname{Cov}(Z_X,Z_Y)
=
\operatorname{Corr}(X,Y)
}
```

---

# 47. ⭐ Covariance Matrix of Standardized Data

This gives one of the most important results in multivariate statistics:

```math
\boxed{
\text{Covariance matrix of standardized data}
=
\text{Correlation matrix of original data}
}
```

Conceptually:

```text
Original Data
      ↓
Standardize each variable
      ↓
Mean = 0
SD = 1
      ↓
Calculate covariance matrix
      ↓
Correlation Matrix
```

This result is extremely important for **PCA**.

---

# 48. 📊 Reading a Correlation Matrix

Consider:

| | Weight | Height | DBP | SBP | Temp |
|---|---:|---:|---:|---:|---:|
| **Weight** | 1 | 0.40* | 0.20 | 0.22 | -0.03 |
| **Height** | 0.40* | 1 | 0.04 | -0.09 | -0.01 |
| **DBP** | 0.20 | 0.04 | 1 | 0.79* | 0.04 |
| **SBP** | 0.22 | -0.09 | 0.79* | 1 | -0.09 |
| **Temp** | -0.03 | -0.01 | 0.04 | -0.09 | 1 |

where:

```text
DBP = Diastolic Blood Pressure
SBP = Systolic Blood Pressure
```

---

# 49. 🔍 Interpreting Weight and Height

From the matrix:

```math
r_{\text{Weight,Height}}
=
0.40
```

This indicates a **positive linear association**.

Conceptually:

```text
Weight ↑
Height tends to ↑
```

The relationship is not perfect because:

```math
0.40<1
```

---

# 50. 🩸 Interpreting DBP and SBP

From the matrix:

```math
r_{\text{DBP,SBP}}
=
0.79
```

This indicates a relatively strong positive linear association.

```text
DBP ↑
   ↕
SBP ↑
```

---

# 51. 🌡️ Interpreting Weight and Temperature

From the matrix:

```math
r_{\text{Weight,Temp}}
=
-0.03
```

This value is very close to zero.

Therefore, these data show very little **linear association** between weight and temperature.

---

# 52. 📉 Interpreting Height and SBP

From the matrix:

```math
r_{\text{Height,SBP}}
=
-0.09
```

This indicates a very weak negative linear association.

Because the value is close to zero, the linear relationship is weak.

---

# 53. 🪞 Reading Both Halves of the Matrix

Because correlation matrices are symmetric:

```math
r_{\text{Weight,Height}}
=
r_{\text{Height,Weight}}
```

Therefore:

```math
0.40=0.40
```

This means the upper and lower triangles contain duplicate information.

Conceptually:

```text
        X₁    X₂    X₃
X₁      1     a     b
X₂      a     1     c
X₃      b     c     1
```

---

# 54. ⭐ What Does the Asterisk Mean?

If a table uses:

```text
*
```

to mark some correlations, it **often** indicates statistical significance.

For example:

```text
* p < 0.05
```

However:

> ⚠️ The exact meaning of `*` must be checked in the table legend or accompanying notes.

Correlation strength and statistical significance are **not the same thing**.

---

# 55. ⚠️ Correlation Does Not Imply Causation

Suppose:

```math
r_{XY}=0.90
```

This means $X$ and $Y$ have a strong linear association.

It does **not** prove:

```text
X causes Y
```

Possible explanations include:

```text
X → Y

Y → X

Z → X and Y

Coincidence / sampling variation

More complex relationships
```

Therefore:

> 📌 **Correlation measures association, not causation.**

---

# 56. ⚠️ Correlation Can Be Affected by Outliers

Pearson correlation can be strongly influenced by unusual observations.

For example:

```text
● ● ● ● ●

                     ●
```

A single extreme point may substantially change the calculated correlation.

Therefore:

> 📌 Always inspect the scatter plot before interpreting a correlation coefficient.

---

# 57. 📈 Recommended Workflow

When examining relationships between variables:

```text
Step 1
Inspect raw data
      ↓
Step 2
Create scatter plots
      ↓
Step 3
Check for outliers
      ↓
Step 4
Calculate covariance
      ↓
Step 5
Calculate correlation
      ↓
Step 6
Interpret direction and strength
      ↓
Step 7
Consider standardization
      ↓
Step 8
Proceed to multivariate analysis
```

---

# 58. 🧮 Matrix Representation of Covariance

Suppose our data matrix contains:

```math
X=
\begin{bmatrix}
x_{11} & x_{12} & \cdots & x_{1p}\\
x_{21} & x_{22} & \cdots & x_{2p}\\
\vdots & \vdots & \ddots & \vdots\\
x_{n1} & x_{n2} & \cdots & x_{np}
\end{bmatrix}
```

where:

```text
Rows    → observations
Columns → variables
```

After centering each column, let the centered matrix be:

```math
X_c
```

Then the sample covariance matrix can be written compactly as:

```math
\boxed{
S=
\frac{1}{n-1}
X_c^T X_c
}
```

This equation is extremely important in multivariate statistics.

---

# 59. 🧠 Understanding the Matrix Formula

```math
S=
\frac{1}{n-1}
X_c^T X_c
```

can be understood as:

```text
Original Data Matrix
        ↓
Center each variable
        ↓
        Xc
        ↓
Transpose
        ↓
       Xcᵀ
        ↓
Multiply
        ↓
      XcᵀXc
        ↓
Divide by n - 1
        ↓
Covariance Matrix
```

---

# 60. 📐 Dimensions of the Covariance Matrix

Suppose:

```math
X_c
```

has:

```math
n\times p
```

dimensions.

That means:

```text
n = observations
p = variables
```

Then:

```math
X_c^T
```

has dimensions:

```math
p\times n
```

Therefore:

```math
X_c^T X_c
```

has dimensions:

```math
(p\times n)(n\times p)
```

giving:

```math
p\times p
```

Thus the covariance matrix has:

```text
Number of rows    = number of variables
Number of columns = number of variables
```

---

# 61. 🔗 Relationship Between Variance, Covariance and Correlation

The three concepts are directly connected:

```text
                    VARIANCE
                       │
                       │
          Spread of one variable
                       │
                       ▼
                   COVARIANCE
                       │
                       │
           Joint variation of two
                 variables
                       │
                       ▼
        Divide by both standard
               deviations
                       │
                       ▼
                  CORRELATION
```

Mathematically:

```math
\operatorname{Var}(X)
=
\operatorname{Cov}(X,X)
```

and:

```math
\operatorname{Corr}(X,Y)
=
\frac{
\operatorname{Cov}(X,Y)
}{
s_Xs_Y
}
```

---

# 62. 🧠 Easy Way to Remember

### 📏 Variance

> **How much does ONE variable vary?**

```math
\operatorname{Var}(X)
```

### 🔗 Covariance

> **How do TWO variables vary together?**

```math
\operatorname{Cov}(X,Y)
```

### 📊 Correlation

> **How strongly and in what direction are TWO variables linearly associated, on a standardized scale?**

```math
\operatorname{Corr}(X,Y)
```

---

# 63. 📊 Covariance vs Correlation vs Standardization

| Concept | Main Question | Scale |
|---|---|---|
| 📏 Variance | How spread out is one variable? | Depends on units |
| 🔗 Covariance | How do two variables vary together? | Depends on units |
| 📊 Correlation | How strongly are two variables linearly associated? | $-1$ to $+1$ |
| ⚖️ Standardization | How can variables be put on comparable scales? | Mean 0, SD 1 |

---

# 64. ⭐ Connection to Eigenvalues and Eigenvectors

The covariance matrix is directly connected to the eigenvector equation:

```math
Sv=\lambda v
```

where:

- $S$ = covariance matrix
- $v$ = eigenvector
- $\lambda$ = eigenvalue

In PCA:

```text
Covariance Matrix
       ↓
Eigenvalue Decomposition
       ↓
Eigenvectors
       ↓
Principal Component Directions
```

while:

```text
Eigenvalues
       ↓
Amount of Variance
       ↓
Explained by Each Component
```

---

# 65. 🚀 Connection to PCA

The basic PCA workflow is:

```text
Raw Multivariate Data
         ↓
Center / Standardize
         ↓
Covariance or Correlation Matrix
         ↓
Eigenvalues + Eigenvectors
         ↓
Principal Components
         ↓
Dimensionality Reduction
```

This is why covariance, correlation, standardization, eigenvalues, and eigenvectors are usually learned before PCA.

---

# 66. ⚖️ Covariance PCA vs Correlation PCA

If variables are measured on similar scales, PCA may be based on the:

```text
Covariance Matrix
```

If variables have very different units or scales, standardization is often appropriate.

Then PCA effectively works with the:

```text
Correlation Matrix
```

Conceptually:

```text
Different scales?
      │
      ├── YES → Standardize → Correlation-based PCA
      │
      └── NO  → Covariance-based PCA may be reasonable
```

> 📌 Whether to standardize should depend on the scientific meaning of the variables, not only on an automatic rule.

---

# 67. 🧬 Why This Matters in Biology

Biological datasets often contain many variables with different scales.

For example:

```text
Patient / Sample
       ↓
┌────────────────────────────┐
│ Gene Expression            │
│ Protein Concentration      │
│ Metabolite Abundance       │
│ Weight                     │
│ Height                     │
│ Blood Pressure             │
│ Temperature                │
└────────────────────────────┘
```

We may want to know:

```text
Which variables vary together?
            ↓
Covariance

How strong are their linear relationships?
            ↓
Correlation

How can differently scaled variables be compared?
            ↓
Standardization

How can many correlated variables be summarized?
            ↓
PCA
```

---

# 68. 🔬 Applications in Multivariate Statistics

Covariance and correlation matrices are fundamental to:

- 📊 **Principal Component Analysis (PCA)**
- 🎯 **Linear Discriminant Analysis (LDA)**
- 📈 **Multivariate regression**
- 🧩 **Clustering and exploratory analysis**
- 🧬 **Gene expression analysis**
- 🧪 **Metabolomics**
- 🧫 **Proteomics**
- 🧠 **Systems biology**
- 🤖 **Machine learning**

---

# 69. 🔑 Key Formulas to Remember

## Mean

```math
\bar{x}
=
\frac{1}{n}
\sum_{i=1}^{n}x_i
```

---

## Sample Variance

```math
s_x^2
=
\frac{1}{n-1}
\sum_{i=1}^{n}
(x_i-\bar{x})^2
```

---

## Sample Standard Deviation

```math
s_x
=
\sqrt{
\frac{1}{n-1}
\sum_{i=1}^{n}
(x_i-\bar{x})^2
}
```

---

## Sample Covariance

```math
s_{xy}
=
\frac{1}{n-1}
\sum_{i=1}^{n}
(x_i-\bar{x})(y_i-\bar{y})
```

---

## Pearson Correlation

```math
r_{xy}
=
\frac{s_{xy}}{s_xs_y}
```

---

## Standardization

```math
z_i
=
\frac{x_i-\bar{x}}{s_x}
```

---

## Covariance Matrix

```math
S=
\frac{1}{n-1}X_c^T X_c
```

---

## Eigenvector Equation

```math
Sv=\lambda v
```

---

# 70. 🧠 Important Distinctions

### Variance vs Standard Deviation

```text
Variance
   ↓
Squared units

Standard Deviation
   ↓
Original units
```

### Covariance vs Correlation

```text
Covariance
   ↓
Depends on units

Correlation
   ↓
Standardized
   ↓
Between -1 and +1
```

### Centering vs Standardization

```text
Centering
   ↓
Subtract mean
   ↓
Mean = 0
```

```text
Standardization
   ↓
Subtract mean
+
Divide by SD
   ↓
Mean = 0
SD = 1
```

---

# 71. 🎯 Quick Summary Table

| Concept | Formula | Main Purpose |
|---|---|---|
| 📊 Mean | $\bar{x}$ | Center of data |
| 📏 Variance | $s^2$ | Spread of one variable |
| 📐 Standard deviation | $s$ | Spread in original units |
| 🔗 Covariance | $s_{xy}$ | Joint variation |
| 📈 Correlation | $r_{xy}$ | Standardized linear association |
| ⚖️ Z-score | $z$ | Standardize observations |
| 📊 Covariance matrix | $S$ | Joint variation among many variables |
| 🔗 Correlation matrix | $R$ | Standardized relationships among many variables |

---

# 72. 🗺️ Complete Concept Map

```text
                    MULTIVARIATE DATA
                           │
                           ▼
                 Multiple Variables
                           │
              ┌────────────┴────────────┐
              │                         │
              ▼                         ▼
           VARIANCE                 COVARIANCE
              │                         │
     Spread of one variable    Joint variation of two
              │                         │
              ▼                         ▼
      STANDARD DEVIATION          STANDARDIZE
              │                         │
              └────────────┬────────────┘
                           ▼
                     CORRELATION
                           │
                           ▼
                  CORRELATION MATRIX
                           │
                           ▼
              COVARIANCE / CORRELATION
                       MATRIX
                           │
                           ▼
                EIGEN DECOMPOSITION
                           │
                 ┌─────────┴─────────┐
                 ▼                   ▼
            Eigenvalues         Eigenvectors
                 │                   │
                 ▼                   ▼
        Amount of Variance     Directions in Data
                 │                   │
                 └─────────┬─────────┘
                           ▼
                          PCA
                           │
                           ▼
              DIMENSIONALITY REDUCTION
```

---

# 73. 🌟 Final Key Takeaways

- 📏 **Variance** measures the spread of one variable around its mean.
- 📐 **Standard deviation** is the square root of variance and uses the original measurement units.
- 🔗 **Covariance** measures how two variables vary together.
- ➕ Positive covariance means the variables tend to move in the same direction.
- ➖ Negative covariance means they tend to move in opposite directions.
- 📊 **Correlation** is standardized covariance.
- 🎯 Pearson correlation ranges from **−1 to +1**.
- ⚠️ A correlation of zero means no **linear** association, not necessarily no relationship.
- ⚠️ Correlation does not establish causation.
- 📊 A covariance matrix contains **variances on the diagonal** and **covariances off the diagonal**.
- 🔗 A correlation matrix contains **1s on the diagonal** and correlations off the diagonal.
- 🪞 Covariance and correlation matrices are symmetric.
- ⚖️ Standardization transforms variables to **mean 0 and standard deviation 1**.
- ⭐ The covariance matrix of standardized variables equals their correlation matrix when the conventions are matched.
- 📊 Covariance and correlation matrices form a major mathematical foundation for **PCA and other multivariate methods**.

---

# 74. 🚀 Final Takeaway

The complete progression is:

```text
Individual Observations
        ↓
      Mean
        ↓
    Deviations
        ↓
     Variance
        ↓
Standard Deviation
        ↓
    Covariance
        ↓
    Correlation
        ↓
Covariance / Correlation Matrix
        ↓
   Standardization
        ↓
Eigenvalues + Eigenvectors
        ↓
       PCA
        ↓
Dimensionality Reduction
        ↓
Advanced Multivariate Statistics
```

> 🧠 **Easy memory trick:**  
>
> **Variance** = How does **one** variable vary?  
> **Covariance** = How do **two** variables vary together?  
> **Correlation** = How strongly and in what direction are they **linearly associated on a standardized scale**?  
> **Standardization** = Put variables onto a **common scale**.  
> **PCA** = Use these relationships to find the **major directions of variation**.
