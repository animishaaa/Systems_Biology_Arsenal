# 🔄 Outliers and Data Transformation in R

>  **Data Analysis for Life Science**

This chapter explains how to:

- Detect potential outliers
- Investigate unusual observations
- Remove incorrect values carefully
- Transform skewed data
- Recheck distributions after transformation
- Report transformed analyses correctly

---

# 📚 Table of Contents

1. [What Is an Outlier?](#-what-is-an-outlier)
2. [Why Outliers Matter](#-why-outliers-matter)
3. [The IQR Rule](#-the-iqr-rule)
4. [Detecting Outliers with Boxplots](#-detecting-outliers-with-boxplots)
5. [Extracting Outlier Values](#-extracting-outlier-values)
6. [Interactive Point Identification](#-interactive-point-identification)
7. [Removing an Outlier](#-removing-an-outlier)
8. [When Should an Outlier Be Removed?](#-when-should-an-outlier-be-removed)
9. [Data Transformation](#-data-transformation)
10. [Natural Log Transformation](#-natural-log-transformation)
11. [Log₂ Transformation](#-log₂-transformation)
12. [Square-Root Transformation](#-square-root-transformation)
13. [Checking the Transformed Data](#-checking-the-transformed-data)
14. [Comparing Original and Transformed Data](#-comparing-original-and-transformed-data)
15. [Reporting Transformed Analyses](#-reporting-transformed-analyses)
16. [Common Mistakes](#-common-mistakes)
17. [Quick R Cheat Sheet](#-quick-r-cheat-sheet)

---

# 📍 What Is an Outlier?

An **outlier** is an observation that lies unusually far from the rest of the data.

Example:

```r
data <- c(10, 12, 15, 9, 8, 7, 12, 25)
```

Most values are between `7` and `15`, but `25` is much larger.

It may be a potential outlier.

---

# ⚠️ Why Outliers Matter

Outliers can strongly influence:

- The mean
- Standard deviation
- Correlation
- Regression coefficients
- Confidence intervals
- Parametric statistical tests

For example:

```r
x1 <- c(4, 5, 5, 6, 5)
mean(x1)
```

```text
5
```

Now add an extreme value:

```r
x2 <- c(4, 5, 5, 6, 50)
mean(x2)
```

```text
14
```

The mean changes dramatically because of one observation.

The median is less affected:

```r
median(x2)
```

```text
5
```

---

# 📏 The IQR Rule

The **interquartile range** measures the spread of the middle 50% of the data.

\[
IQR = Q_3 - Q_1
\]

A value is commonly considered a potential outlier if it is:

\[
x < Q_1 - 1.5 \times IQR
\]

or

\[
x > Q_3 + 1.5 \times IQR
\]

---

## 💻 Calculate the IQR in R

```r
data <- c(10, 12, 15, 9, 8, 7, 12, 25)

IQR(data)
```

---

## Calculate Quartiles

```r
Q1 <- quantile(data, 0.25)
Q3 <- quantile(data, 0.75)

Q1
Q3
```

---

## Calculate the Outlier Limits

```r
iqr_value <- IQR(data)

lower_limit <- Q1 - 1.5 * iqr_value
upper_limit <- Q3 + 1.5 * iqr_value

lower_limit
upper_limit
```

---

## Identify Values Outside the Limits

```r
data[data < lower_limit | data > upper_limit]
```

This returns the potential outlier values.

---

# 📦 Detecting Outliers with Boxplots

A boxplot displays:

- Median
- First quartile
- Third quartile
- Interquartile range
- Whiskers
- Potential outliers

---

## Basic Boxplot

```r
data <- c(10, 12, 15, 9, 8, 7, 12, 25)

boxplot(data)
```

Potential outliers are displayed as separate points beyond the whiskers.

---

## Add Labels and a Title

```r
boxplot(
  data,
  main = "Boxplot of Experimental Data",
  ylab = "Measurement"
)
```

---

## Horizontal Boxplot

```r
boxplot(
  data,
  horizontal = TRUE,
  main = "Boxplot of Experimental Data",
  xlab = "Measurement"
)
```

---

# 🔍 Extracting Outlier Values

The function `boxplot.stats()` returns detailed boxplot information.

```r
stats <- boxplot.stats(data)

stats
```

---

## Extract Only the Outliers

```r
stats$out
```

---

## Extract the Whisker and Quartile Statistics

```r
stats$stats
```

The result contains approximately:

```text
Minimum whisker
First quartile
Median
Third quartile
Maximum whisker
```

---

## Complete Example

```r
data <- c(10, 12, 15, 9, 8, 7, 12, 25)

result <- boxplot.stats(data)

result$stats
result$out
```

---

# 🖱️ Interactive Point Identification

The `identify()` function lets you click on a point in a graph and display its observation number.

This works best in an interactive R or RStudio graphics window.

---

## Example

```r
data <- c(10, 12, 15, 9, 8, 7, 12, 25)

plot(
  rep(1, length(data)),
  data,
  xlab = "",
  ylab = "Measurement",
  xaxt = "n"
)

identify(
  rep(1, length(data)),
  data,
  labels = seq_along(data),
  n = 1
)
```

Click the unusual point.

R displays its index.

For this dataset, the value `25` is observation:

```text
8
```

---

## Windows Graphics Device

On some Windows systems:

```r
win.graph()

plot(
  rep(1, length(data)),
  data,
  xlab = "",
  ylab = "Measurement",
  xaxt = "n"
)

identify(
  rep(1, length(data)),
  data,
  labels = seq_along(data),
  n = 1
)
```

> `win.graph()` is Windows-specific and is not required in every RStudio setup.

---

# 🗑️ Removing an Outlier

Do not remove an outlier automatically.

First investigate why it occurred.

Suppose observation 8 is confirmed as a data-entry error:

```r
data <- c(10, 12, 15, 9, 8, 7, 12, 25)
```

Remove it using:

```r
clean_data <- data[-8]
```

Check the result:

```r
clean_data
```

Create a new boxplot:

```r
boxplot(
  clean_data,
  main = "Data After Removing Confirmed Error",
  ylab = "Measurement"
)
```

---

## Remove by Value

```r
clean_data <- data[data != 25]
```

This removes every occurrence of `25`.

Use this method carefully because several observations may have the same value.

---

## Remove Using the IQR Rule

```r
Q1 <- quantile(data, 0.25)
Q3 <- quantile(data, 0.75)
iqr_value <- IQR(data)

lower_limit <- Q1 - 1.5 * iqr_value
upper_limit <- Q3 + 1.5 * iqr_value

clean_data <- data[
  data >= lower_limit &
  data <= upper_limit
]
```

This mechanically removes all values outside the IQR limits.

> This should not be done without scientific justification.

---

# 🧠 When Should an Outlier Be Removed?

An outlier should only be removed when there is a defensible reason.

| Cause | Recommended action |
|---|---|
| Data-entry error | Correct or remove |
| Instrument failure | Consider removal |
| Measurement error | Investigate and possibly remove |
| Participant not eligible | Exclude if justified by predefined criteria |
| Natural biological variation | Usually keep |
| Unknown cause | Keep and perform sensitivity analysis |

---

## ✅ Good Practice

Document:

- Which observation was removed
- Why it was removed
- Whether the decision was made before or after analysis
- Whether conclusions changed after removal

---

## Sensitivity Analysis

Compare the analysis:

- With the outlier
- Without the outlier

Example:

```r
mean(data)
mean(clean_data)

sd(data)
sd(clean_data)
```

If the conclusion changes substantially, report this.

---

# 🔄 Data Transformation

A transformation changes the scale of the data.

Transformations are often used when data are:

- Right-skewed
- Heteroscedastic
- Influenced by large values
- Multiplicative rather than additive

Common transformations include:

- Natural logarithm
- Log base 2
- Square root

---

# 📈 Why Transform Data?

Many parametric analyses assume:

- Approximately normal residuals
- Similar variances
- Linear relationships

A transformation may help satisfy these assumptions.

Example of right-skewed data:

```r
data <- c(
  0.3, 0.5, 0.7, 0.8, 1.1,
  1.4, 1.8, 2.2, 4.5, 12.0
)
```

---

## Histogram of Original Data

```r
hist(
  data,
  main = "Original Data",
  xlab = "Measurement"
)
```

The long right tail indicates positive skew.

---

# 🌿 Natural Log Transformation

The natural logarithm is written as:

\[
y_{\text{transformed}} = \ln(y)
\]

In R, use:

```r
logged_data <- log(data)
```

---

## Plot the Transformed Data

```r
hist(
  logged_data,
  main = "Natural Log-Transformed Data",
  xlab = "log(Measurement)"
)
```

---

## Summary Before and After

```r
summary(data)
summary(logged_data)
```

---

## Important Restriction

The logarithm is only defined for positive values.

This works:

```r
log(c(0.5, 1, 2, 10))
```

This produces invalid values:

```r
log(c(-1, 0, 1))
```

---

## If the Data Contain Zero

A common approach is:

```r
logged_data <- log1p(data)
```

`log1p(x)` calculates:

\[
\ln(1+x)
\]

Example:

```r
data_with_zero <- c(0, 1, 2, 5, 10)

log1p(data_with_zero)
```

> Adding a constant changes the interpretation and should be scientifically justified.

---

# 2️⃣ Log₂ Transformation

A log base 2 transformation is useful when changes are interpreted as doubling or halving.

```r
log2_data <- log2(data)
```

---

## Interpretation

A difference of `1` on the log₂ scale corresponds to a two-fold change.

Example:

```r
log2(2)
log2(4)
log2(8)
```

```text
1
2
3
```

Moving from `2` to `4` is a one-unit increase on the log₂ scale.

---

## Plot Log₂-Transformed Data

```r
hist(
  log2_data,
  main = "Log2-Transformed Data",
  xlab = "log2(Measurement)"
)
```

---

# √ Square-Root Transformation

The square-root transformation is often used for count data.

\[
y_{\text{transformed}} = \sqrt{y}
\]

In R:

```r
sqrt_data <- sqrt(data)
```

---

## Example with Count Data

```r
counts <- c(0, 1, 2, 3, 5, 8, 15, 25, 40)

sqrt_counts <- sqrt(counts)

sqrt_counts
```

---

## Plot Before and After

```r
hist(
  counts,
  main = "Original Counts",
  xlab = "Count"
)
```

```r
hist(
  sqrt_counts,
  main = "Square-Root-Transformed Counts",
  xlab = "Square Root of Count"
)
```

---

# 🔎 Checking the Transformed Data

Do not assume a transformation worked.

Check the distribution and assumptions again.

---

## Histogram

```r
hist(logged_data)
```

---

## Q–Q Plot

```r
qqnorm(logged_data)
qqline(logged_data)
```

---

## Shapiro–Wilk Test

```r
shapiro.test(logged_data)
```

Interpretation:

| P-value | Interpretation |
|---|---|
| `p > 0.05` | No strong evidence against normality |
| `p ≤ 0.05` | Evidence of non-normality |

Always combine the Shapiro–Wilk result with graphical assessment.

---

## Boxplot

```r
boxplot(logged_data)
```

---

# 📊 Comparing Original and Transformed Data

```r
data <- c(
  0.3, 0.5, 0.7, 0.8, 1.1,
  1.4, 1.8, 2.2, 4.5, 12.0
)

logged_data <- log(data)

summary(data)
summary(logged_data)

sd(data)
sd(logged_data)

shapiro.test(data)
shapiro.test(logged_data)
```

---

# 🧪 Using Transformed Data in a Statistical Test

Suppose you compare a concentration between two independent groups.

```r
concentration <- c(
  1.2, 1.5, 1.9, 2.2, 8.5,
  0.9, 1.1, 1.3, 1.6, 4.2
)

group <- factor(c(
  rep("Control", 5),
  rep("Treatment", 5)
))
```

Transform the outcome:

```r
log_concentration <- log(concentration)
```

Check assumptions:

```r
shapiro.test(log_concentration[group == "Control"])
shapiro.test(log_concentration[group == "Treatment"])
```

Run the test using transformed values:

```r
t.test(log_concentration ~ group)
```

---

# 🔁 Back-Transformation

If a statistical analysis is performed on the natural log scale, exponentiation converts values back to the original scale.

```r
mean_log <- mean(logged_data)

exp(mean_log)
```

This produces the **geometric mean**.

---

## Back-Transform a Confidence Interval

```r
ci_log <- c(0.2, 0.8)

exp(ci_log)
```

The result is interpreted on the original measurement scale.

---

# 📝 Reporting Transformed Analyses

## Example: Log Transformation

> The outcome was positively skewed and was therefore natural log-transformed before analysis. Assumptions were assessed using histograms, Q–Q plots, and residual diagnostics. Statistical testing was performed on the transformed scale, and estimates were back-transformed for interpretation.

---

## Example: Geometric Mean

> The geometric mean concentration was 2.4 mg/L, with a 95% confidence interval from 1.8 to 3.2 mg/L.

---

## Example: Sensitivity to an Outlier

> One observation was identified as potentially influential. Because no measurement or data-entry error was found, it was retained. A sensitivity analysis excluding the observation produced a similar conclusion.

---

## Example: Confirmed Measurement Error

> One observation was excluded because instrument failure was documented during data collection. The exclusion criterion was applied before hypothesis testing.

---

# ⚠️ Common Mistakes

## ❌ Mistake 1: Automatically deleting every boxplot outlier

A boxplot marks unusual values, not necessarily incorrect values.

---

## ❌ Mistake 2: Removing an outlier because it changes the p-value

This introduces bias.

Removal must be scientifically justified.

---

## ❌ Mistake 3: Applying `log()` to zero or negative values

```r
log(0)
log(-1)
```

These are not valid finite log-transformed measurements.

---

## ❌ Mistake 4: Assuming transformation guarantees normality

Always recheck:

- Histogram
- Q–Q plot
- Residuals
- Shapiro–Wilk test

---

## ❌ Mistake 5: Reporting only transformed values without explanation

State:

- Why the transformation was used
- Which transformation was applied
- Whether results were back-transformed

---

## ❌ Mistake 6: Saying non-parametric tests are always better for outliers

Rank-based tests are less sensitive to extreme values, but the test must still match:

- The study design
- The data type
- The scientific question

---

# 🧭 Recommended Workflow

```text
Inspect the data
      ↓
Create histogram and boxplot
      ↓
Identify potential outliers
      ↓
Investigate their cause
      ↓
Keep, correct, or remove with justification
      ↓
Check distribution and assumptions
      ↓
Transform if scientifically appropriate
      ↓
Recheck assumptions
      ↓
Run the statistical analysis
      ↓
Report all decisions clearly
```

---

# ⚡ Quick R Cheat Sheet

| Task | R command |
|---|---|
| Calculate IQR | `IQR(x)` |
| Calculate quartiles | `quantile(x)` |
| Create boxplot | `boxplot(x)` |
| Extract outliers | `boxplot.stats(x)$out` |
| Extract boxplot statistics | `boxplot.stats(x)$stats` |
| Identify points interactively | `identify()` |
| Remove observation by index | `x[-index]` |
| Natural log | `log(x)` |
| Log base 2 | `log2(x)` |
| Log of `1 + x` | `log1p(x)` |
| Square root | `sqrt(x)` |
| Histogram | `hist(x)` |
| Q–Q plot | `qqnorm(x)` |
| Q–Q reference line | `qqline(x)` |
| Normality test | `shapiro.test(x)` |
| Geometric mean | `exp(mean(log(x)))` |
| Back-transform log values | `exp(x)` |

---

# 📌 Complete Example

```r
# Clear workspace
rm(list = ls(all = TRUE))

# Enter data
data <- c(
  0.3, 0.5, 0.7, 0.8, 1.1,
  1.4, 1.8, 2.2, 4.5, 12.0
)

# Inspect data
summary(data)
sd(data)
IQR(data)

# Detect potential outliers
boxplot(data)
boxplot.stats(data)$out

# Calculate IQR limits
Q1 <- quantile(data, 0.25)
Q3 <- quantile(data, 0.75)
iqr_value <- IQR(data)

lower_limit <- Q1 - 1.5 * iqr_value
upper_limit <- Q3 + 1.5 * iqr_value

data[data < lower_limit | data > upper_limit]

# Examine original distribution
hist(data)
qqnorm(data)
qqline(data)
shapiro.test(data)

# Apply natural log transformation
logged_data <- log(data)

# Recheck transformed distribution
hist(logged_data)
qqnorm(logged_data)
qqline(logged_data)
shapiro.test(logged_data)

# Compare summaries
summary(data)
summary(logged_data)

# Calculate geometric mean
geometric_mean <- exp(mean(logged_data))
geometric_mean
```

---

# 🎯 Key Takeaways

- 📍 An outlier is unusual, not automatically incorrect.
- 📦 Boxplots and the IQR rule identify potential outliers.
- 🔍 Every unusual observation should be investigated.
- 🗑️ Remove observations only with scientific justification.
- 🔄 Transformations may reduce skewness and stabilize variance.
- 🌿 Use `log()` for positive right-skewed data.
- 2️⃣ Use `log2()` when fold changes are meaningful.
- √ Use `sqrt()` commonly for counts.
- 🔎 Always reassess assumptions after transformation.
- 📝 Report exclusions and transformations transparently.
