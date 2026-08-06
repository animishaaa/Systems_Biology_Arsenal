# 📊 Descriptive Statistics

> **Summarizing and Exploring Data with Python**

Descriptive statistics summarize, organize, and describe datasets before formal statistical analysis.

They provide information about:

- 📍 Central tendency
- 📈 Dispersion
- 📦 Distribution
- 📊 Frequency
- 📉 Shape of the data

Descriptive statistics are always the **first step** before performing hypothesis tests or regression analyses.

---

# 📚 Table of Contents

1. What are Descriptive Statistics?
2. Why are They Important?
3. Measures of Central Tendency
4. Measures of Dispersion
5. Frequency Tables
6. Summary Statistics
7. Percentiles and Quartiles
8. Histograms
9. Boxplots
10. Distribution Shape
11. R vs Python
12. Biological Examples
13. Common Mistakes
14. Key Takeaways

---

# 📖 What are Descriptive Statistics?

Descriptive statistics summarize datasets without drawing conclusions about populations.

They describe:

- 📊 The center of the data
- 📈 The spread of the data
- 📦 The distribution of the data
- 🔍 Possible outliers

---

# 🎯 Why are Descriptive Statistics Important?

Descriptive statistics help to:

- 📊 Understand the dataset
- 🔍 Detect errors
- 📈 Identify outliers
- 📉 Assess distributions
- 📦 Check assumptions before statistical testing

---

# 📥 Import Libraries

```python
import numpy as np
import pandas as pd
```

---

# 📋 Example Dataset

```python
bp = np.array([
    142,
    145,
    139,
    141,
    148,
    150,
    143,
    144
])
```

---

# 📍 Measures of Central Tendency

## Mean

The arithmetic average.

```python
np.mean(bp)
```

Equivalent R code

```r
mean(bp)
```

---

## Median

The middle observation.

```python
np.median(bp)
```

Equivalent R code

```r
median(bp)
```

---

## Mode

```python
from scipy import stats

stats.mode(bp)
```

Equivalent R

```r
table(bp)
```

---

# 📈 Measures of Dispersion

## Minimum

```python
np.min(bp)
```

---

## Maximum

```python
np.max(bp)
```

---

## Range

```python
np.max(bp) - np.min(bp)
```

Equivalent R

```r
range(bp)
```

---

## Variance

Sample variance

```python
np.var(
    bp,
    ddof=1
)
```

Equivalent R

```r
var(bp)
```

---

## Standard Deviation

```python
np.std(
    bp,
    ddof=1
)
```

Equivalent R

```r
sd(bp)
```

---

## Standard Error

```python
n = len(bp)

sd = np.std(
    bp,
    ddof=1
)

se = sd / np.sqrt(n)

print(se)
```

Equivalent R

```r
SE <- sd(bp) / sqrt(length(bp))
```

---

# 📦 Quartiles

25th percentile

```python
np.percentile(
    bp,
    25
)
```

---

Median

```python
np.percentile(
    bp,
    50
)
```

---

75th percentile

```python
np.percentile(
    bp,
    75
)
```

---

Interquartile Range (IQR)

```python
from scipy.stats import iqr

iqr(bp)
```

Equivalent R

```r
IQR(bp)
```

---

# 📊 Summary Statistics

Using NumPy

```python
print("Mean:", np.mean(bp))
print("Median:", np.median(bp))
print("SD:", np.std(bp, ddof=1))
```

---

Using Pandas

```python
df = pd.DataFrame({
    "BP": bp
})

df.describe()
```

Output includes:

- Count
- Mean
- Standard deviation
- Minimum
- Quartiles
- Maximum

Equivalent R

```r
summary(df)
```

---

# 📋 Frequency Tables

```python
df["BP"].value_counts()
```

Sort frequencies

```python
df["BP"].value_counts().sort_index()
```

Equivalent R

```r
table(bp)
```

---

# 📊 Histograms

```python
import matplotlib.pyplot as plt

plt.hist(
    bp,
    bins=5
)

plt.xlabel("Blood Pressure")

plt.ylabel("Frequency")

plt.title("Histogram")

plt.show()
```

---

# 📦 Boxplots

```python
plt.boxplot(bp)

plt.ylabel("Blood Pressure")

plt.show()
```

Useful for:

- Detecting outliers
- Comparing distributions
- Viewing median and quartiles

---

# 📈 Distribution Shape

A histogram can suggest whether data are:

- ✅ Approximately normal
- 📈 Right-skewed
- 📉 Left-skewed
- 🔀 Bimodal

Formal normality testing will be covered in a later chapter.

---

# 🔢 Five-Number Summary

```python
np.min(bp)
```

```python
np.percentile(bp, 25)
```

```python
np.median(bp)
```

```python
np.percentile(bp, 75)
```

```python
np.max(bp)
```

Equivalent R

```r
summary(bp)
```

---

# ⚖️ Python vs R

| Python | R |
|----------|----|
| `np.mean()` | `mean()` |
| `np.median()` | `median()` |
| `np.std(ddof=1)` | `sd()` |
| `np.var(ddof=1)` | `var()` |
| `iqr()` | `IQR()` |
| `value_counts()` | `table()` |
| `describe()` | `summary()` |

---

# 🧬 Biological Example

```python
df = pd.DataFrame({

    "Patient":[1,2,3,4,5],

    "Age":[35,42,28,51,46],

    "BloodPressure":[142,145,138,150,143],

    "BMI":[24.5,27.8,22.1,30.2,26.7]

})
```

Average BMI

```python
df["BMI"].mean()
```

Average blood pressure

```python
df["BloodPressure"].mean()
```

Standard deviation

```python
df["BloodPressure"].std()
```

Summary statistics

```python
df.describe()
```

---

# ⚠️ Common Mistakes

❌ Using `np.std()` without `ddof=1`.

Incorrect

```python
np.std(bp)
```

Correct

```python
np.std(bp, ddof=1)
```

---

❌ Performing hypothesis tests before exploring the data.

Always begin with descriptive statistics.

---

❌ Ignoring outliers.

Visualize the data before analysis.

---

# 💡 Tips

- 📊 Always calculate descriptive statistics before inferential statistics.
- 📦 Boxplots quickly identify potential outliers.
- 📈 Histograms help assess data distributions.
- 📋 `describe()` provides a rapid statistical summary.
- 📉 Standard error is calculated from the standard deviation and sample size.

---

# 🎯 Key Takeaways

- 📊 Descriptive statistics summarize datasets before formal analysis.
- 📍 Measures of central tendency include the mean, median, and mode.
- 📈 Measures of dispersion include the range, variance, standard deviation, standard error, and interquartile range.
- 📋 Frequency tables summarize categorical or repeated values.
- 📦 Histograms and boxplots are essential tools for exploratory data analysis.
- 📉 Data distributions should always be assessed before hypothesis testing.

