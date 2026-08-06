# 📦 Outliers and Data Transformation

> **Detecting Outliers and Preparing Data for Statistical Analysis**

Outliers are observations that differ substantially from the rest of the dataset.

Data transformation changes the scale or distribution of data to better satisfy the assumptions of statistical tests.

Both procedures are important parts of **Exploratory Data Analysis (EDA)**.

---

# 📚 Table of Contents

1. What is an Outlier?
2. Why Detect Outliers?
3. Importing Libraries
4. Detecting Outliers
5. Boxplots
6. IQR Rule
7. Identifying Outliers
8. Removing Outliers
9. Data Transformation
10. Log Transformation
11. Log₂ Transformation
12. Square-root Transformation
13. Comparing Distributions
14. Python vs R
15. Biological Examples
16. Common Mistakes
17. Key Takeaways

---

# 📖 What is an Outlier?

An outlier is an observation that lies unusually far from the rest of the data.

Example:

```text
142 145 143 144 141 146 143 210
```

The value **210** is a potential outlier.

---

# 🎯 Why Detect Outliers?

Outliers can:

- 📈 Distort the mean
- 📊 Inflate the standard deviation
- 📉 Affect correlations
- 📦 Influence regression models
- ⚠️ Violate statistical assumptions

Outliers are **not always errors**.

Possible causes include:

- Measurement error
- Data entry error
- Instrument malfunction
- Genuine biological variation

---

# 📦 Import Libraries

```python
import numpy as np
import pandas as pd

import matplotlib.pyplot as plt
import seaborn as sns
```

---

# 📊 Example Dataset

```python
bp = np.array([

142,
145,
143,
144,
141,
146,
143,
210

])
```

---

# 📦 Detecting Outliers with Boxplots

```python
plt.boxplot(bp)

plt.ylabel("Blood Pressure")

plt.show()
```

The boxplot displays:

- Median
- Quartiles
- Whiskers
- Potential outliers

---

Using Seaborn

```python
sns.boxplot(y=bp)

plt.show()
```

---

# 📏 The IQR Rule

The **Interquartile Range (IQR)** is

```text
IQR = Q3 − Q1
```

Where:

- Q1 = 25th percentile
- Q3 = 75th percentile

---

## Lower Limit

```text
Q1 − 1.5 × IQR
```

---

## Upper Limit

```text
Q3 + 1.5 × IQR
```

Values outside these limits are considered potential outliers.

---

# 🧮 Calculating the IQR

```python
Q1 = np.percentile(bp, 25)

Q3 = np.percentile(bp, 75)

IQR = Q3 - Q1

print(IQR)
```

---

Calculate limits.

```python
lower = Q1 - 1.5 * IQR

upper = Q3 + 1.5 * IQR
```

---

# 🔍 Identifying Outliers

```python
outliers = bp[

    (bp < lower)

    |

    (bp > upper)

]

print(outliers)
```

Output

```text
[210]
```

---

# 🧹 Removing Outliers

```python
bp_clean = bp[

    (bp >= lower)

    &

    (bp <= upper)

]
```

Display cleaned data.

```python
print(bp_clean)
```

---

# 📊 Comparing Before and After

Original boxplot

```python
plt.boxplot(bp)

plt.show()
```

---

Cleaned boxplot

```python
plt.boxplot(bp_clean)

plt.show()
```

---

# 📉 Histograms

Original data

```python
plt.hist(bp)

plt.title("Original Data")

plt.show()
```

---

Cleaned data

```python
plt.hist(bp_clean)

plt.title("Without Outliers")

plt.show()
```

---

# 🔄 Data Transformation

Transformation changes the distribution of the data.

Common transformations include:

- Natural logarithm
- Log₂
- Square root

---

# 📉 Natural Log Transformation

```python
log_bp = np.log(bp_clean)
```

Histogram

```python
plt.hist(log_bp)

plt.title("Log Transformation")

plt.show()
```

---

# 📊 Log₂ Transformation

```python
log2_bp = np.log2(bp_clean)
```

---

# 📐 Square-root Transformation

```python
sqrt_bp = np.sqrt(bp_clean)
```

---

# 📈 Comparing Distributions

Original

```python
plt.hist(bp_clean)

plt.title("Original")

plt.show()
```

---

Log

```python
plt.hist(log_bp)

plt.title("Log")

plt.show()
```

---

Square Root

```python
plt.hist(sqrt_bp)

plt.title("Square Root")

plt.show()
```

---

# 📊 Skewness

```python
from scipy.stats import skew

skew(bp_clean)
```

Interpretation

| Skewness | Interpretation |
|----------|----------------|
| 0 | Symmetric |
| > 0 | Right-skewed |
| < 0 | Left-skewed |

---

# 📈 Kurtosis

```python
from scipy.stats import kurtosis

kurtosis(bp_clean)
```

Used to describe:

- Tail heaviness
- Peak shape

---

# 📊 Checking Normality

Shapiro–Wilk test

```python
from scipy.stats import shapiro

shapiro(bp_clean)
```

Interpretation

```text
p > 0.05

↓

Approximately normal
```

---

# ⚖️ Python vs R

| Python | R |
|----------|----|
| `plt.boxplot()` | `boxplot()` |
| `np.percentile()` | `quantile()` |
| `np.log()` | `log()` |
| `np.log2()` | `log2()` |
| `np.sqrt()` | `sqrt()` |
| `shapiro()` | `shapiro.test()` |

---

# 🧬 Biological Example

Gene expression values.

```python
expression = np.array([

4.2,
3.8,
5.1,
2.9,
6.4,
21.5

])
```

Detect outliers.

```python
sns.boxplot(y=expression)

plt.show()
```

Apply log transformation.

```python
expression_log = np.log(expression)
```

Visualize transformed data.

```python
plt.hist(expression_log)

plt.show()
```

---

# ⚠️ Common Mistakes

❌ Automatically deleting outliers.

Investigate the cause before removal.

---

❌ Transforming data without checking the original distribution.

Always inspect histograms first.

---

❌ Using transformed data without documenting the transformation.

Report every preprocessing step.

---

❌ Assuming every non-normal dataset requires transformation.

Sometimes a **non-parametric test** is more appropriate.

---

# 💡 Tips

- 📦 Always inspect boxplots before statistical testing.
- 📊 Use the IQR rule to identify potential outliers.
- 📈 Log transformation is useful for right-skewed data.
- 📉 Square-root transformation often works well for count data.
- 🔍 Recheck normality after transformation.
- 📝 Document every transformation for reproducibility.

---

# 🔄 Typical Workflow

```text
Import Data
      │
      ▼
Histogram
      │
      ▼
Boxplot
      │
      ▼
Calculate IQR
      │
      ▼
Detect Outliers
      │
      ▼
Investigate Outliers
      │
      ▼
Remove (if justified)
      │
      ▼
Transform Data (if necessary)
      │
      ▼
Check Normality
      │
      ▼
Choose Statistical Test
```

---

# 🎯 Key Takeaways

- 📦 Outliers are observations that differ markedly from the rest of the data.
- 📊 The IQR rule is a standard method for identifying potential outliers.
- 📈 Boxplots provide a simple visual summary of distributions and outliers.
- 📉 Logarithmic and square-root transformations can improve distributional properties.
- 📋 Normality should be reassessed after any transformation.
- 🧪 Data transformation is only one option; non-parametric methods may also be appropriate.
- 📚 Every preprocessing decision should be documented to ensure reproducibility.

