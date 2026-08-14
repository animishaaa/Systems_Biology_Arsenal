# 📊 Covariance and Correlation

## Complete Notes: Variance, Covariance, Correlation, Matrices & Standardization

Covariance and correlation are fundamental concepts in **multivariate statistics**.

They help us understand how variables behave **together** and provide the mathematical foundation for methods such as:

* 📊 Principal Component Analysis (PCA)
* 🎯 Linear Discriminant Analysis (LDA)
* 📈 Multivariate regression
* 🧩 Clustering
* 🧬 Gene expression analysis
* 🤖 Machine learning

The main progression is:

```text
Variance
   ↓
Covariance
   ↓
Correlation
   ↓
Covariance Matrix
   ↓
Correlation Matrix
   ↓
Standardization
   ↓
PCA
```

---

# 1. 🔍 Why Covariance and Correlation Matter

In multivariate statistics, we often measure several variables for the same observation.

For example:

| Patient | Weight | Height | Blood Pressure | Temperature |
| ------- | -----: | -----: | -------------: | ----------: |
| 1       |     61 |    157 |            120 |        37.0 |
| 2       |     62 |    168 |            125 |        36.8 |
| 3       |     73 |    170 |            130 |        37.1 |

We may want to know:

* 🔗 Do two variables change together?
* 📈 Does one variable increase when another increases?
* 📉 Does one variable decrease when another increases?
* 🚫 Are the variables linearly unrelated?

Examples:

```text
Body Weight ↔ Body Height
Gene Expression ↔ Phenotype
Blood Pressure ↔ Age
Temperature ↔ Disease Severity
```

Two important statistical quantities help us answer these questions:

```text
Covariance
    ↓
Measures joint variation

Correlation
    ↓
Measures standardized linear association
```

---

# 2. 📏 Variance – How Much Does One Variable Vary?

## What Is Variance?

Variance measures how much the values of **one variable** spread around their mean.

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

> 💡 **Variance asks:**
> How much does one variable move away from its average?

---

# 3. 🧮 The Mean

Suppose we observe:

```math
x_1,x_2,\ldots,x_n
```

The sample mean is:

```math
\bar{x}
=
\frac{1}{n}
\sum_{i=1}^{n}x_i
```

where:

* `x_i` = individual observation
* `\bar{x}` = sample mean
* `n` = number of observations

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

* `x_i` = individual observation
* `\bar{x}` = sample mean
* `n` = number of observations
* `x_i-\bar{x}` = deviation from the mean
* `s_x^2` = sample variance

> 📌 For sample variance, we divide by `n - 1`.

---

# 5. 🧠 Why Do We Square the Deviations?

Suppose deviations from the mean are:

```text
-10, -5, 0, +5, +10
```

If we simply add them:

```math
-10-5+0+5+10=0
```

The positive and negative deviations cancel.

Instead, we square them:

```text
100, 25, 0, 25, 100
```

Now all contributions are positive.

Therefore variance can measure the total spread.

---

# 6. 🧮 Variance Step by Step

The calculation follows:

```text
Raw observations
      ↓
Calculate mean
      ↓
Subtract mean from every observation
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
\sum_{i=1}^{n}(x_i-\bar{x})^2
\rightarrow
s_x^2
```

---

# 7. 📏 Example of Variance

Suppose height measurements in decimeters are:

```math
x=
\begin{bmatrix}
16 \\
17 \\
18
\end{bmatrix}
```

Calculate the mean:

```math
\bar{x}
=
\frac{16+17+18}{3}
=
17
```

Calculate the deviations:

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

Now calculate the sample variance:

```math
s^2
=
\frac{1+0+1}{3-1}
=
1
```

Therefore:

```math
\boxed{s^2=1}
```

---

# 8. 📐 Standard Deviation

Variance has one inconvenience.

If height is measured in centimeters:

```text
Height → cm
```

then variance is measured in:

```text
cm²
```

To return to the original units, we take the square root.

The sample standard deviation is:

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

* 📏 Uses the same units as the original variable
* 📊 Measures spread
* 🧠 Is easier to interpret than variance

Remember:

```text
Variance
   ↓
Spread in squared units

Standard Deviation
   ↓
Spread in original units
```

---

# 9. 🔗 Covariance – Do Two Variables Move Together?

Variance asks:

> How does **X** vary?

Covariance asks:

> When **X changes**, what tends to happen to **Y**?

This is the key transition from **univariate** to **bivariate/multivariate thinking**.

---

# 10. ➕ Positive Covariance

Suppose we observe:

| Person | Height | Weight |
| ------ | -----: | -----: |
| A      |    150 |     50 |
| B      |    160 |     60 |
| C      |    170 |     70 |
| D      |    180 |     80 |

As height increases:

```text
Height ↑
   ↓
Weight ↑
```

Therefore, the two variables have **positive covariance**.

```math
\mathrm{Cov}(X,Y)>0
```

---

# 11. ➖ Negative Covariance

Suppose:

|  X |   Y |
| -: | --: |
|  1 | 100 |
|  2 |  80 |
|  3 |  60 |
|  4 |  40 |

As `X` increases:

```text
X ↑
 ↓
Y ↓
```

Therefore:

```math
\mathrm{Cov}(X,Y)<0
```

This is **negative covariance**.

---

# 12. 🧮 Sample Covariance Formula

For two variables `X` and `Y`:

```math
s_{xy}
=
\mathrm{Cov}(X,Y)
=
\frac{1}{n-1}
\sum_{i=1}^{n}
(x_i-\bar{x})(y_i-\bar{y})
```

where:

* `x_i` = observation from variable X
* `y_i` = observation from variable Y
* `\bar{x}` = mean of X
* `\bar{y}` = mean of Y
* `n` = number of paired observations

---

# 13. 🧠 The Most Important Part of Covariance

Focus on:

```math
(x_i-\bar{x})(y_i-\bar{y})
```

This compares whether X and Y are above or below their respective means.

---

## Case 1: Both Above Their Means

```math
(x_i-\bar{x})>0
```

and:

```math
(y_i-\bar{y})>0
```

Therefore:

```math
(+)(+)=+
```

✅ Positive contribution to covariance.

---

## Case 2: Both Below Their Means

```math
(x_i-\bar{x})<0
```

and:

```math
(y_i-\bar{y})<0
```

Therefore:

```math
(-)(-)=+
```

✅ Also a positive contribution.

---

## Case 3: X Above, Y Below

```math
(x_i-\bar{x})>0
```

but:

```math
(y_i-\bar{y})<0
```

Therefore:

```math
(+)(-) = -
```

❌ Negative contribution.

---

## Case 4: X Below, Y Above

```math
(x_i-\bar{x})<0
```

but:

```math
(y_i-\bar{y})>0
```

Therefore:

```math
(-)(+) = -
```

❌ Negative contribution.

---

# 14. 📋 The Four Covariance Possibilities

| X relative to mean | Y relative to mean | Product |
| ------------------ | ------------------ | ------: |
| Above              | Above              |       + |
| Below              | Below              |       + |
| Above              | Below              |       − |
| Below              | Above              |       − |

Therefore:

> ✅ **Same-side deviations → positive covariance**

> ❌ **Opposite-side deviations → negative covariance**

---

# 15. 0️⃣ Zero Covariance

If:

```math
\mathrm{Cov}(X,Y)\approx0
```

there is little or no **linear co-movement** between the two variables.

However:

> ⚠️ Zero covariance does **not necessarily mean no relationship**.

A nonlinear relationship may exist even if covariance is zero.

---

# 16. 📊 Covariance Sign Interpretation

| Covariance | Meaning                                          |
| ---------- | ------------------------------------------------ |
| `> 0`      | 📈 Variables tend to move together               |
| `< 0`      | 📉 Variables tend to move in opposite directions |
| `≈ 0`      | ➖ Little or no linear co-movement                |

---

# 17. ⚠️ Why Covariance Magnitude Is Hard to Interpret

Suppose:

```text
Weight → kg
Height → cm
```

Then covariance has units:

```text
kg × cm
```

Suppose:

```math
\mathrm{Cov}(X,Y)=80
```

Is `80` strong?

We cannot tell immediately.

The value depends heavily on:

* Measurement units
* Variable scales

If height changes from centimeters to meters, covariance changes numerically even though the biological relationship is unchanged.

This motivates **correlation**.

---

# 18. 🔗 Correlation – Standardized Covariance

Pearson correlation standardizes covariance.

The formula is:

```math
r_{xy}
=
\frac{s_{xy}}{s_xs_y}
```

Equivalently:

```math
r_{xy}
=
\frac{\mathrm{Cov}(X,Y)}
{s_xs_y}
```

where:

* `s_{xy}` = covariance between X and Y
* `s_x` = standard deviation of X
* `s_y` = standard deviation of Y

---

# 19. 🎯 Range of Correlation

Pearson correlation always satisfies:

```math
-1\leq r\leq1
```

This gives correlation a very useful standardized scale.

| Correlation | Interpretation                        |
| ----------: | ------------------------------------- |
|        `+1` | Perfect positive linear relationship  |
|      `+0.8` | Strong positive linear relationship   |
|      `+0.4` | Moderate positive linear relationship |
|         `0` | No linear relationship                |
|      `-0.4` | Moderate negative linear relationship |
|      `-0.8` | Strong negative linear relationship   |
|        `-1` | Perfect negative linear relationship  |

> 📌 Exact labels such as *weak*, *moderate*, and *strong* depend on the scientific context.

---

# 20. 📈 Correlation Scale

```text
-1                  0                  +1
│-------------------│-------------------│
Strong negative     No linear          Strong positive
relationship        relationship       relationship
```

Values close to:

```math
+1
```

indicate strong positive linear association.

Values close to:

```math
-1
```

indicate strong negative linear association.

Values close to:

```math
0
```

indicate weak linear association.

---

# 21. 🆚 Covariance vs Correlation

### Covariance asks:

> In which direction do X and Y move together?

### Correlation asks:

> In which direction, and how strongly, are X and Y linearly associated after removing scale?

Conceptually:

```text
Covariance
    ↓
Divide by SD(X) × SD(Y)
    ↓
Correlation
```

Mathematically:

```math
r_{xy}
=
\frac{s_{xy}}{s_xs_y}
```

---

# 22. 📋 Covariance vs Correlation Table

| Property                      | Covariance | Correlation |
| ----------------------------- | ---------- | ----------- |
| Measures joint variation      | ✅          | ✅           |
| Shows direction               | ✅          | ✅           |
| Standardized                  | ❌          | ✅           |
| Fixed range                   | ❌          | `[-1,1]`    |
| Depends on units              | ✅          | ❌           |
| Scale-independent             | ❌          | ✅           |
| Easy magnitude interpretation | ❌          | ✅           |

---

# 23. ⚖️ Worked Example: Weight and Height

Suppose we have:

| Person | Weight (kg) | Height (cm) |
| -----: | ----------: | ----------: |
|      1 |          61 |         157 |
|      2 |          62 |         168 |
|      3 |          73 |         170 |
|      4 |          74 |         181 |
|      5 |          82 |         191 |
|      6 |          86 |         185 |

Represent the variables as:

```math
X=
\begin{bmatrix}
61 \\
62 \\
73 \\
74 \\
82 \\
86
\end{bmatrix}
```

and:

```math
Y=
\begin{bmatrix}
157 \\
168 \\
170 \\
181 \\
191 \\
185
\end{bmatrix}
```

---

# 24. 🧮 Step 1: Calculate the Mean Weight

```math
\bar{x}
=
\frac{61+62+73+74+82+86}{6}
```

Therefore:

```math
\bar{x}=73
```

---

# 25. 🧮 Step 2: Calculate the Mean Height

```math
\bar{y}
=
\frac{157+168+170+181+191+185}{6}
```

Therefore:

```math
\bar{y}\approx175.33
```

---

# 26. 🧮 Step 3: Calculate Deviations

For the first person:

```math
x_1-\bar{x}
=
61-73
=
-12
```

and:

```math
y_1-\bar{y}
=
157-175.33
\approx
-18.33
```

Multiply the deviations:

```math
(-12)(-18.33)>0
```

Because both variables are below their means, this observation contributes positively to covariance.

---

# 27. 🧮 Step 4: Calculate Sample Covariance

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
s_{xy}\approx132.4
```

Therefore:

```math
\boxed{
\mathrm{Cov}(X,Y)\approx132.4
}
```

The positive value indicates that weight and height tend to increase together.

---

# 28. 📐 Step 5: Calculate Standard Deviations

The approximate sample standard deviations are:

```math
s_x\approx10.04
```

and:

```math
s_y\approx12.47
```

---

# 29. 🔗 Step 6: Calculate Pearson Correlation

Use:

```math
r
=
\frac{s_{xy}}{s_xs_y}
```

Substitute:

```math
r
=
\frac{132.4}
{(10.04)(12.47)}
```

Therefore:

```math
\boxed{r\approx0.94}
```

📌 This indicates a **strong positive linear relationship** in this small sample.

---

# 30. 📈 Visual Interpretation with Scatter Plots

A scatter plot represents every observation as:

```math
(x_i,y_i)
```

The shape of the point cloud helps us interpret correlation.

---

# 31. 🟢 Perfect Positive Correlation

```text
Y
│             ●
│          ●
│       ●
│    ●
│ ●
└──────────────── X
```

The points lie exactly on an increasing straight line.

```math
r=1
```

---

# 32. 📈 Strong Positive Correlation

```text
Y
│             ●
│        ● ●
│      ●
│   ●    ●
│ ●
└──────────────── X
```

The points approximately follow an increasing straight line.

For example:

```math
r\approx0.79
```

---

# 33. 🔹 Weak Positive Correlation

```text
Y
│       ●      ●
│  ●
│          ●
│     ●
│ ●            ●
└──────────────── X
```

A weak upward trend may exist.

For example:

```math
r\approx0.38
```

---

# 34. 0️⃣ No Linear Correlation

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

# 35. 📉 Negative Correlation

```text
Y
│ ●
│    ●
│       ●
│          ●
│             ●
└──────────────── X
```

As X increases, Y decreases.

Therefore:

```math
r<0
```

For a perfect negative linear relationship:

```math
r=-1
```

---

# 36. ⚠️ Pearson Correlation Measures Linear Association

Consider a U-shaped relationship:

```text
Y
│ ●           ●
│   ●       ●
│
│      ●
└──────────────── X
```

X and Y clearly have a relationship.

However, Pearson correlation may still be close to:

```math
r=0
```

because there is little overall **linear** association.

Therefore:

> 📌 `r ≈ 0` means little or no **linear relationship**, not necessarily no relationship at all.

---

# 37. ⚠️ Correlation Does Not Imply Causation

Suppose:

```math
r_{\mathrm{ice\ cream,\ sunburn}}>0
```

Does eating ice cream cause sunburn?

No.

A third variable may affect both.

For example:

```text
Temperature ↑
      │
      ├────────→ Ice cream sales ↑
      │
      └────────→ Sun exposure ↑
```

Therefore:

> 📌 **Correlation measures association. It does not prove causation.**

---

# 38. ⚠️ Correlation Can Be Influenced by Outliers

Suppose most observations form one pattern:

```text
● ● ● ● ●
```

but there is one extreme observation:

```text
                     ●
```

That single observation may strongly change Pearson correlation.

Therefore:

> 📌 Always inspect the scatter plot before interpreting the correlation coefficient.

---

# 39. 📊 Covariance Matrix

With many variables, calculating every pairwise covariance separately becomes inconvenient.

Suppose we have:

```math
X_1,\ X_2,\ X_3
```

The covariance matrix is:

```math
S=
\begin{bmatrix}
\mathrm{Var}(X_1) &
\mathrm{Cov}(X_1,X_2) &
\mathrm{Cov}(X_1,X_3)
\\
\mathrm{Cov}(X_2,X_1) &
\mathrm{Var}(X_2) &
\mathrm{Cov}(X_2,X_3)
\\
\mathrm{Cov}(X_3,X_1) &
\mathrm{Cov}(X_3,X_2) &
\mathrm{Var}(X_3)
\end{bmatrix}
```

---

# 40. 🔍 Structure of a Covariance Matrix

The diagonal contains variances:

```math
S_{ii}
=
\mathrm{Var}(X_i)
```

The off-diagonal elements contain covariances:

```math
S_{ij}
=
\mathrm{Cov}(X_i,X_j)
```

Conceptually:

```text
               X₁              X₂              X₃

X₁          Variance       Covariance      Covariance

X₂         Covariance       Variance       Covariance

X₃         Covariance      Covariance       Variance
```

---

# 41. 💡 Variance Is Covariance with Itself

A very important identity is:

```math
\mathrm{Cov}(X,X)
=
\mathrm{Var}(X)
```

Therefore:

> 🧠 **Variance is simply the covariance of a variable with itself.**

This explains why variances appear on the diagonal of a covariance matrix.

---

# 42. 🪞 Why Is the Covariance Matrix Symmetric?

Covariance satisfies:

```math
\mathrm{Cov}(X,Y)
=
\mathrm{Cov}(Y,X)
```

Therefore:

```math
S_{12}=S_{21}
```

and in general:

```math
S_{ij}=S_{ji}
```

Thus:

```math
\boxed{S=S^T}
```

So every covariance matrix is symmetric.

---

# 43. 📊 Example Covariance Matrix

```math
S=
\begin{bmatrix}
4 & 2 & -1 \\
2 & 9 & 3 \\
-1 & 3 & 16
\end{bmatrix}
```

The diagonal values:

```math
4,\ 9,\ 16
```

are variances.

The off-diagonal values:

```math
2,\ -1,\ 3
```

are covariances.

Notice:

```math
S_{12}=S_{21}=2
```

```math
S_{13}=S_{31}=-1
```

```math
S_{23}=S_{32}=3
```

Therefore the matrix is symmetric.

---

# 44. 🔗 Correlation Matrix

A correlation matrix has the same structure as a covariance matrix, but contains correlations instead of covariances.

For three variables:

```math
R=
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
\mathrm{Corr}(X_i,X_j)
```

---

# 45. 1️⃣ Why Is the Diagonal of a Correlation Matrix Equal to 1?

The correlation of a variable with itself is:

```math
\mathrm{Corr}(X,X)
=
\frac{
\mathrm{Cov}(X,X)
}{
s_xs_x
}
```

Since:

```math
\mathrm{Cov}(X,X)
=
\mathrm{Var}(X)
=
s_x^2
```

we obtain:

```math
\mathrm{Corr}(X,X)
=
\frac{s_x^2}{s_x^2}
=
1
```

Therefore:

```math
\boxed{r_{ii}=1}
```

---

# 46. 🪞 Correlation Matrix Is Symmetric

Because:

```math
\mathrm{Corr}(X,Y)
=
\mathrm{Corr}(Y,X)
```

we have:

```math
R=R^T
```

and:

```math
r_{ij}=r_{ji}
```

---

# 47. 📊 Example Correlation Matrix

Suppose:

```math
R=
\begin{bmatrix}
1 & 0.40 & 0.20 \\
0.40 & 1 & 0.04 \\
0.20 & 0.04 & 1
\end{bmatrix}
```

The diagonal contains:

```text
1, 1, 1
```

because each variable is perfectly correlated with itself.

The off-diagonal values represent relationships between different variables.

---

# 48. 🆚 Covariance Matrix vs Correlation Matrix

Example covariance matrix:

```math
S=
\begin{bmatrix}
100 & 20 \\
20 & 25
\end{bmatrix}
```

A corresponding correlation matrix might be:

```math
R=
\begin{bmatrix}
1 & 0.40 \\
0.40 & 1
\end{bmatrix}
```

The major distinction is:

```text
Covariance Matrix
        ↓
Depends on measurement scale

Correlation Matrix
        ↓
Standardized
        ↓
Scale-independent
```

---

# 49. ⚖️ Standardization of Data

Multivariate datasets often contain variables measured in very different units.

For example:

| Variable        | Unit   |
| --------------- | ------ |
| Weight          | kg     |
| Height          | cm     |
| Blood pressure  | mmHg   |
| Temperature     | °C     |
| Gene expression | counts |

Their numerical scales may be very different.

For example:

```text
Weight          = 70
Height          = 180
Temperature     = 37
Gene expression = 24,000
```

These numbers are not directly comparable.

Standardization removes the effect of scale.

---

# 50. 📐 Z-Score Standardization

The standardized value is:

```math
z_i
=
\frac{x_i-\bar{x}}{s_x}
```

where:

* `x_i` = original value
* `\bar{x}` = mean
* `s_x` = standard deviation
* `z_i` = standardized value

A z-score tells us:

> How many standard deviations is this observation away from the mean?

---

# 51. 🧠 Example of a Z-Score

Suppose:

```math
\bar{x}=70
```

and:

```math
s_x=10
```

For someone weighing 90 kg:

```math
z
=
\frac{90-70}{10}
=
2
```

Therefore:

> The observation is **2 standard deviations above the mean**.

For someone weighing 60 kg:

```math
z
=
\frac{60-70}{10}
=
-1
```

Therefore:

> The observation is **1 standard deviation below the mean**.

---

# 52. 🔄 Standardization Step by Step

```text
Original data
      ↓
Subtract the mean
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

# 53. 1️⃣ Stage 1: Original Data

Suppose:

```math
X=
\begin{bmatrix}
10 \\
20 \\
30
\end{bmatrix}
```

The mean is:

```math
\bar{x}=20
```

---

# 54. 2️⃣ Stage 2: Center the Data

Subtract the mean:

```math
X-\bar{x}
=
\begin{bmatrix}
10-20 \\
20-20 \\
30-20
\end{bmatrix}
```

Therefore:

```math
X_{\mathrm{centered}}
=
\begin{bmatrix}
-10 \\
0 \\
10
\end{bmatrix}
```

The centered data have:

```math
\boxed{\mathrm{Mean}=0}
```

---

# 55. 3️⃣ Stage 3: Divide by Standard Deviation

For these data:

```math
s=10
```

Therefore:

```math
Z
=
\frac{X-\bar{x}}{s}
```

giving:

```math
Z=
\begin{bmatrix}
-1 \\
0 \\
1
\end{bmatrix}
```

After standardization:

```math
\boxed{\mathrm{Mean}=0}
```

and:

```math
\boxed{\mathrm{SD}=1}
```

---

# 56. 🔑 What Standardization Does

Before standardization:

```text
Height
Mean = 175 cm
SD   = 12 cm
```

After standardization:

```text
Mean = 0
SD   = 1
```

Now kilograms, centimeters, blood pressure, gene-expression counts, etc. are expressed in the same conceptual unit:

> **Number of standard deviations from the mean**

---

# 57. ⭐ Why Covariance of Standardized Variables Equals Correlation

Suppose:

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

The covariance between the standardized variables becomes:

```math
\mathrm{Cov}(Z_X,Z_Y)
=
\frac{
\mathrm{Cov}(X,Y)
}{
s_Xs_Y
}
```

But Pearson correlation is:

```math
\mathrm{Corr}(X,Y)
=
\frac{
\mathrm{Cov}(X,Y)
}{
s_Xs_Y
}
```

Therefore:

```math
\boxed{
\mathrm{Cov}(Z_X,Z_Y)
=
\mathrm{Corr}(X,Y)
}
```

---

# 58. 📊 Key Matrix Result

For an entire standardized dataset:

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
Standardize every variable
      ↓
Mean = 0
SD = 1
      ↓
Calculate covariance matrix
      ↓
Correlation Matrix
```

This relationship is extremely important for **PCA**.

---

# 59. 📊 Reading a Correlation Matrix

Consider:

|            | Weight | Height |   DBP |   SBP |  Temp |
| ---------- | -----: | -----: | ----: | ----: | ----: |
| **Weight** |      1 |  0.40* |  0.20 |  0.22 | -0.03 |
| **Height** |  0.40* |      1 |  0.04 | -0.09 | -0.01 |
| **DBP**    |   0.20 |   0.04 |     1 | 0.79* |  0.04 |
| **SBP**    |   0.22 |  -0.09 | 0.79* |     1 | -0.09 |
| **Temp**   |  -0.03 |  -0.01 |  0.04 | -0.09 |     1 |

where:

```text
DBP = Diastolic Blood Pressure
SBP = Systolic Blood Pressure
```

---

# 60. 🔍 Weight and Height

From the matrix:

```math
r_{\mathrm{Weight,Height}}
=
0.40
```

This indicates a positive linear association.

Conceptually:

```text
Weight ↑
   ↕
Height tends to ↑
```

---

# 61. 🩸 DBP and SBP

From the matrix:

```math
r_{\mathrm{DBP,SBP}}
=
0.79
```

This represents a relatively strong positive linear relationship.

```text
DBP ↑
  ↕
SBP ↑
```

---

# 62. 🌡️ Weight and Temperature

From the matrix:

```math
r_{\mathrm{Weight,Temp}}
=
-0.03
```

Because this value is extremely close to zero:

> There is very little linear association between weight and temperature in this sample.

---

# 63. 📉 Height and SBP

From the matrix:

```math
r_{\mathrm{Height,SBP}}
=
-0.09
```

This represents a very weak negative linear relationship.

---

# 64. 🪞 Why Does Each Correlation Appear Twice?

Because:

```math
\mathrm{Corr}(X,Y)
=
\mathrm{Corr}(Y,X)
```

therefore:

```math
r_{\mathrm{Weight,Height}}
=
r_{\mathrm{Height,Weight}}
```

Both are:

```math
0.40
```

Therefore the upper and lower parts of the matrix contain duplicate information.

---

# 65. ⭐ What Does `*` Mean?

If a correlation table contains:

```text
0.40*
```

or:

```text
0.79*
```

the asterisk often indicates statistical significance.

For example:

```math
p<0.05
```

However:

> ⚠️ Always check the table legend because the meaning of `*` depends on the source.

Also remember:

> **Correlation magnitude and statistical significance are not the same thing.**

A small correlation may become statistically significant with a very large sample.

A larger correlation may fail to reach significance with a very small sample.

---

# 66. 🧮 Covariance Matrix in Matrix Form

Suppose the data matrix is:

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

After subtracting each variable's mean, let the centered matrix be:

```math
X_c
```

The sample covariance matrix is:

```math
\boxed{
S=
\frac{1}{n-1}
X_c^T X_c
}
```

This is one of the most important formulas in multivariate statistics.

---

# 67. 🧠 Understanding the Matrix Formula

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
Matrix multiplication
        ↓
      XcᵀXc
        ↓
Divide by n - 1
        ↓
Covariance Matrix
```

---

# 68. 📐 Dimensions of the Covariance Matrix

Suppose:

```math
X_c
```

has dimensions:

```math
n\times p
```

where:

```text
n = number of observations
p = number of variables
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
X_c^TX_c
```

has dimensions:

```math
(p\times n)(n\times p)
```

giving:

```math
p\times p
```

Therefore:

> 📌 The covariance matrix has one row and one column for every variable.

---

# 69. 🔗 Relationship Between Variance, Covariance and Correlation

These three concepts are directly connected.

```text
                  VARIANCE
                     │
                     ▼
          Spread of one variable
                     │
                     ▼
                 COVARIANCE
                     │
                     ▼
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
\mathrm{Var}(X)
=
\mathrm{Cov}(X,X)
```

and:

```math
\mathrm{Corr}(X,Y)
=
\frac{
\mathrm{Cov}(X,Y)
}{
s_Xs_Y
}
```

---

# 70. 🧠 Easy Way to Remember

### 📏 Variance

> How much does **one variable** vary?

```math
\mathrm{Var}(X)
```

### 🔗 Covariance

> How do **two variables** vary together?

```math
\mathrm{Cov}(X,Y)
```

### 📊 Correlation

> How strongly and in what direction are **two variables linearly associated**, after removing scale?

```math
\mathrm{Corr}(X,Y)
```

---

# 71. 📊 Variance vs Covariance vs Correlation vs Standardization

| Concept            | Main Question                                       | Scale            |
| ------------------ | --------------------------------------------------- | ---------------- |
| 📏 Variance        | How spread out is one variable?                     | Depends on units |
| 🔗 Covariance      | How do two variables vary together?                 | Depends on units |
| 📊 Correlation     | How strongly are two variables linearly associated? | −1 to +1         |
| ⚖️ Standardization | How can variables be put on comparable scales?      | Mean 0, SD 1     |

---

# 72. ⭐ Connection to Eigenvalues and Eigenvectors

The covariance matrix is directly connected to the eigenvector equation.

```math
Sv=\lambda v
```

where:

* `S` = covariance matrix
* `v` = eigenvector
* `\lambda` = eigenvalue

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

# 73. 🚀 Connection to PCA

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

This is why we learn:

```text
Variance
   ↓
Covariance
   ↓
Correlation
   ↓
Standardization
   ↓
Eigenvalues + Eigenvectors
   ↓
PCA
```

---

# 74. ⚖️ Covariance-Based PCA vs Correlation-Based PCA

If all variables are measured on similar scales, PCA can reasonably be based on the **covariance matrix**.

If variables have very different units or scales, standardization is often appropriate.

Then PCA is effectively based on the **correlation matrix**.

```text
Variables on very different scales?
            │
      ┌─────┴─────┐
      │           │
     YES          NO
      │           │
      ▼           ▼
Standardize    Covariance PCA
      │        may be reasonable
      ▼
Correlation-based PCA
```

> 📌 Standardization should ultimately depend on the scientific meaning of the variables, not only on an automatic rule.

---

# 75. 🧬 Why This Matters in Biological Data

Biological datasets may contain:

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

We may ask:

```text
Which variables vary together?
            ↓
        Covariance

How strong is the linear relationship?
            ↓
        Correlation

How can different scales be compared?
            ↓
      Standardization

How can many variables be summarized?
            ↓
            PCA
```

---

# 76. 🔬 Applications in Multivariate Statistics

Covariance and correlation matrices are important in:

* 📊 Principal Component Analysis
* 🎯 Linear Discriminant Analysis
* 📈 Multivariate regression
* 🧩 Clustering
* 🧬 Gene expression analysis
* 🧪 Metabolomics
* 🧫 Proteomics
* 🧠 Systems biology
* 🤖 Machine learning

---

# 77. 🔑 Key Formulas

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
\frac{1}{n-1}X_c^TX_c
```

---

## Eigenvector Equation

```math
Sv=\lambda v
```

---

# 78. 🧠 Important Distinctions

## Variance vs Standard Deviation

```text
Variance
   ↓
Squared units

Standard Deviation
   ↓
Original units
```

---

## Covariance vs Correlation

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

---

## Centering vs Standardization

### Centering

```math
x_i^{(c)}
=
x_i-\bar{x}
```

Result:

```math
\mathrm{Mean}=0
```

### Standardization

```math
z_i
=
\frac{x_i-\bar{x}}{s_x}
```

Result:

```math
\mathrm{Mean}=0
```

and:

```math
\mathrm{SD}=1
```

---

# 79. 🎯 Quick Summary Table

| Concept               | Formula   | Main Purpose                               |
| --------------------- | --------- | ------------------------------------------ |
| 📊 Mean               | `\bar{x}` | Center of the data                         |
| 📏 Variance           | `s^2`     | Spread of one variable                     |
| 📐 Standard deviation | `s`       | Spread in original units                   |
| 🔗 Covariance         | `s_{xy}`  | Joint variation                            |
| 📈 Correlation        | `r_{xy}`  | Standardized linear association            |
| ⚖️ Z-score            | `z`       | Standardize observations                   |
| 📊 Covariance matrix  | `S`       | Joint variation among many variables       |
| 🔗 Correlation matrix | `R`       | Standardized relationships among variables |

---

# 80. 🗺️ Complete Concept Map

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

# 81. 🌟 Key Takeaways

* 📏 **Variance** measures the spread of one variable around its mean.
* 📐 **Standard deviation** is the square root of variance and uses the original measurement units.
* 🔗 **Covariance** measures how two variables vary together.
* ➕ Positive covariance means the variables tend to move in the same direction.
* ➖ Negative covariance means they tend to move in opposite directions.
* 📊 **Correlation** is standardized covariance.
* 🎯 Pearson correlation ranges from **−1 to +1**.
* ⚠️ A correlation near zero means little or no **linear** association, not necessarily no relationship.
* ⚠️ Correlation does not prove causation.
* 📊 A covariance matrix contains **variances on the diagonal** and **covariances off the diagonal**.
* 🔗 A correlation matrix contains **1s on the diagonal** and correlations off the diagonal.
* 🪞 Covariance and correlation matrices are symmetric.
* ⚖️ Standardization transforms variables to **mean 0 and standard deviation 1**.
* ⭐ The covariance matrix of standardized variables equals the corresponding correlation matrix when the same sample conventions are used.
* 📊 These concepts form a major mathematical foundation for **PCA and multivariate statistics**.

---

# 82. 🚀 Final Takeaway

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
> **Variance** = How does **one variable** vary?
> **Covariance** = How do **two variables** vary together?
> **Correlation** = How strongly and in what direction are they **linearly associated after removing scale**?
> **Standardization** = Put variables onto a **common scale**.
> **PCA** = Use the covariance/correlation structure to find the **major directions of variation**.
