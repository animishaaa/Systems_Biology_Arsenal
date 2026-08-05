# 🧪 One-Sample Wilcoxon Signed-Rank Test in R

> **Data Analysis for Life Science**

The **One-Sample Wilcoxon Signed-Rank Test** is the **non-parametric alternative** to the **One-Sample t-test**.

Instead of testing whether the **mean** equals a known value, it tests whether the **median** equals a known value.

---

# 📚 Table of Contents

1. Purpose
2. Why Use the Wilcoxon Test?
3. When to Use
4. Parametric vs Non-Parametric
5. Data Requirements
6. Assumptions
7. Hypotheses
8. How the Test Works
9. Example Dataset
10. Step 1 – Enter the Data
11. Step 2 – Explore the Data
12. Step 3 – Run the Test
13. Understanding the Output
14. Interpretation
15. Reporting Results
16. Common Mistakes
17. Related Tests
18. Decision Workflow
19. Quick R Cheat Sheet
20. Key Takeaways

---

# 🎯 Purpose

The **One-Sample Wilcoxon Signed-Rank Test** compares the **median** of one sample to a known (hypothesized) value.

It is used when the assumptions of the **One-Sample t-test** are not met.

---

# 🤔 Why Use the Wilcoxon Test?

The One-Sample t-test assumes that the data are **approximately normally distributed**.

If the data are:

- Skewed
- Contain outliers
- Not normally distributed

then the **Wilcoxon Signed-Rank Test** is a better choice.

---

# 📌 When to Use

Use this test when:

- ✅ One numerical sample
- ✅ Compare against a known value
- ✅ Data are **not normally distributed**
- ✅ Interested in the **median**

---

## Examples

- Is the median blood pressure equal to **140 mmHg**?
- Is the median cholesterol level different from **5 mmol/L**?
- Is the median tumor size greater than **10 mm**?

---

# ⚖️ Parametric vs Non-Parametric

| Parametric | Non-Parametric |
|------------|----------------|
| One-Sample t-test | ✅ One-Sample Wilcoxon Signed-Rank Test |
| Tests the **mean** | Tests the **median** |
| Requires normality | No normality assumption |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Groups | One |
| Outcome | Continuous or ordinal |
| Comparison | Against one known value |

---

# 📋 Assumptions

The Wilcoxon Signed-Rank Test assumes:

- Independent observations
- Continuous or ordinal data
- Differences are approximately **symmetrical**
- Data do **not** need to be normally distributed

---

# 🧪 Hypotheses

Suppose we want to test whether the median systolic blood pressure equals **140 mmHg**.

### Null Hypothesis

\[
H_0:\text{Median}=140
\]

There is no difference.

---

### Alternative Hypothesis

\[
H_1:\text{Median}\neq140
\]

The median differs from 140.

---

# 🧠 How the Test Works

Unlike a t-test, the Wilcoxon test **does not use the raw values directly**.

Instead, it:

1. Calculates the difference between each observation and the hypothesized value.
2. Ignores differences equal to zero.
3. Takes the absolute value of each difference.
4. Ranks the absolute differences from smallest to largest.
5. Adds the ranks of positive and negative differences separately.
6. Uses these rank sums to calculate the test statistic (**V**).

Because it uses **ranks instead of raw values**, the test is less affected by outliers.

---

# 📂 Example Dataset

```r
SB <- c(
142,142,144,140,141,
140,142,148,140,137,
144,138,142,139,144,
144,141,134,143,148
)
```

---

# 💻 Step 1 – Enter the Data

```r
SB <- c(
142,142,144,140,141,
140,142,148,140,137,
144,138,142,139,144,
144,141,134,143,148
)
```

---

# 💻 Step 2 – Explore the Data

Summary

```r
summary(SB)
```

Median

```r
median(SB)
```

Histogram

```r
hist(SB)
```

Boxplot

```r
boxplot(SB)
```

---

# 💻 Step 3 – Run the Test

```r
wilcox.test(
SB,
mu = 140,
exact = FALSE,
correct = FALSE
)
```

---

## One-Tailed Test

Greater than 140

```r
wilcox.test(
SB,
mu = 140,
alternative = "greater",
exact = FALSE
)
```

Less than 140

```r
wilcox.test(
SB,
mu = 140,
alternative = "less",
exact = FALSE
)
```

---

# 📊 Example Output

```text
Wilcoxon signed rank test

V = 120.5

p-value = 0.036
```

---

# 🔍 Understanding the Output

## V

The **Wilcoxon test statistic**.

Unlike a t-test, it is based on the **sum of ranks**, not the raw measurements.

---

## p-value

Compare with α = 0.05.

If:

```text
p < 0.05
```

Reject **H₀**.

If:

```text
p ≥ 0.05
```

Do not reject **H₀**.

---

# 📈 Interpretation

Suppose:

```text
Median = 142

p = 0.036
```

Since:

```text
0.036 < 0.05
```

Reject the null hypothesis.

Conclusion:

The median systolic blood pressure is significantly different from **140 mmHg**.

---

# 📝 Reporting Results

Example

> A one-sample Wilcoxon signed-rank test showed that the median systolic blood pressure (142 mmHg) was significantly different from 140 mmHg (V = 120.5, p = 0.036).

---

# ⚠️ Common Mistakes

❌ Reporting the mean instead of the median.

---

❌ Using the test when data are normally distributed.

A One-Sample t-test has greater statistical power when its assumptions are satisfied.

---

❌ Forgetting to specify the hypothesized value (`mu`).

---

❌ Confusing the Wilcoxon statistic (**V**) with the t statistic.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| One sample (normal) | One-Sample t-test |
| One sample (non-normal) | ✅ One-Sample Wilcoxon Signed-Rank Test |
| Two independent groups | Mann–Whitney U Test |
| Two paired groups | Wilcoxon Signed-Rank Test |
| Paired data without symmetry | Sign Test |

---

# 🌳 Decision Workflow

```text
One sample
      │
      ▼
Continuous data?
      │
      ▼
Compare with one value?
      │
      ▼
Check normality
      │
 ┌────┴────┐
 │         │
 ▼         ▼
Normal?   Not normal?
 │         │
 ▼         ▼
One-Sample  One-Sample
t-test      Wilcoxon
```

---

# ⚡ Quick R Cheat Sheet

```r
# Summary
summary(SB)

# Median
median(SB)

# Histogram
hist(SB)

# Boxplot
boxplot(SB)

# One-Sample Wilcoxon
wilcox.test(
SB,
mu = 140
)

# Greater than
wilcox.test(
SB,
mu = 140,
alternative = "greater"
)

# Less than
wilcox.test(
SB,
mu = 140,
alternative = "less"
)
```

---

# 📊 Parametric vs Non-Parametric Comparison

| Feature | One-Sample t-test | One-Sample Wilcoxon |
|----------|-------------------|---------------------|
| Tests | Mean | Median |
| Assumes normality | ✅ Yes | ❌ No |
| Uses raw values | ✅ Yes | ❌ No |
| Uses ranks | ❌ No | ✅ Yes |
| Sensitive to outliers | ✅ Yes | ❌ Less sensitive |

---

# 🎯 Key Takeaways

- 🧪 The **One-Sample Wilcoxon Signed-Rank Test** is the **non-parametric alternative** to the One-Sample t-test.
- 📊 It tests whether the **median** differs from a known value.
- 📈 It uses **ranks instead of raw values**, making it more robust to outliers and skewed data.
- ⚠️ It assumes the differences are approximately **symmetrical**, but **does not require normality**.
- 💻 In R, use `wilcox.test()` with the `mu` argument to specify the hypothesized median.
- 🔍 If the p-value is less than 0.05, reject the null hypothesis.
