# 🧪 One-Sample t-Test in R

> **Data Analysis for Life Science**

The **One-Sample t-test** is used to determine whether the **mean of a single sample** differs significantly from a known or hypothesized population mean.

---

# 📚 Table of Contents

1. [Purpose](#-purpose)
2. [When to Use](#-when-to-use)
3. [Data Requirements](#-data-requirements)
4. [Assumptions](#-assumptions)
5. [Hypotheses](#-hypotheses)
6. [Example Dataset](#-example-dataset)
7. [Step 1 – Enter the Data](#-step-1--enter-the-data)
8. [Step 2 – Explore the Data](#-step-2--explore-the-data)
9. [Step 3 – Check Assumptions](#-step-3--check-assumptions)
10. [Step 4 – Run the One-Sample t-Test](#-step-4--run-the-one-sample-t-test)
11. [Understanding the Output](#-understanding-the-output)
12. [Reporting the Results](#-reporting-the-results)
13. [One-Tailed vs Two-Tailed Tests](#-one-tailed-vs-two-tailed-tests)
14. [Common Mistakes](#-common-mistakes)
15. [Related Tests](#-related-tests)
16. [Quick R Cheat Sheet](#-quick-r-cheat-sheet)

---

# 🎯 Purpose

Use a **One-Sample t-test** when you want to compare the **mean of one sample** with a known or hypothesized population mean.

It answers questions such as:

- Is the average blood pressure greater than **140 mmHg**?
- Is the average plant height different from **20 cm**?
- Is the average enzyme activity equal to the reference value?

---

# 🧠 When to Use

Use a One-Sample t-test when:

- ✅ You have **one sample**
- ✅ The outcome variable is **continuous**
- ✅ You want to compare the sample mean with a known value
- ✅ The population standard deviation is unknown

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Number of groups | One |
| Outcome variable | Continuous |
| Predictor | None |
| Comparison | Sample mean vs known value |

---

# 📋 Assumptions

Before performing a One-Sample t-test, check that:

- Continuous data
- Independent observations
- Approximately normally distributed data
- No serious outliers

---

# 🧪 Hypotheses

Suppose we want to test whether the average systolic blood pressure is greater than **140 mmHg**.

### Null Hypothesis (H₀)

\[
\mu \le 140
\]

The mean blood pressure is **140 mmHg or lower**.

---

### Alternative Hypothesis (H₁)

\[
\mu > 140
\]

The mean blood pressure is **greater than 140 mmHg**.

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

This dataset contains systolic blood pressure measurements from **20 patients**.

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

## View Summary Statistics

```r
summary(SB)
```

Calculate the mean:

```r
mean(SB)
```

Calculate the median:

```r
median(SB)
```

Calculate the standard deviation:

```r
sd(SB)
```

Calculate the standard error:

```r
n <- length(SB)

SE <- sd(SB)/sqrt(n)

SE
```

---

# 💻 Step 3 – Check Assumptions

## Histogram

```r
hist(SB)
```

---

## Q-Q Plot

```r
qqnorm(SB)

qqline(SB)
```

If the points follow the straight line reasonably well, the normality assumption is acceptable.

---

## Shapiro–Wilk Test

```r
shapiro.test(SB)
```

Interpretation:

- **p > 0.05** → No strong evidence against normality
- **p ≤ 0.05** → Evidence of non-normality

---

# 💻 Step 4 – Run the One-Sample t-Test

Test whether the mean is greater than **140**.

```r
t.test(
SB,
mu = 140,
alternative = "greater"
)
```

---

# 💻 Other Alternatives

## Two-sided test

```r
t.test(
SB,
mu = 140
)
```

Equivalent to:

```r
alternative = "two.sided"
```

---

## Less than

```r
t.test(
SB,
mu = 140,
alternative = "less"
)
```

---

## Greater than

```r
t.test(
SB,
mu = 140,
alternative = "greater"
)
```

---

# 📊 Understanding the Output

Example:

```text
One Sample t-test

t = 2.20

df = 19

p-value = 0.02

95 percent confidence interval

140.4 Inf

sample estimates

mean = 141.6
```

---

## Interpretation

Mean:

```text
141.6 mmHg
```

The sample average blood pressure.

---

Degrees of freedom:

```text
19
```

Because:

\[
df=n-1
\]

\[
20-1=19
\]

---

Test statistic:

```text
t = 2.20
```

Larger absolute t-values indicate stronger evidence against the null hypothesis.

---

P-value:

```text
0.02
```

Since

```text
0.02 < 0.05
```

Reject H₀.

There is evidence that the average blood pressure is greater than **140 mmHg**.

---

# 📝 Reporting the Results

Example:

> A one-tailed one-sample t-test showed that the mean systolic blood pressure (**141.6 mmHg**) was significantly greater than **140 mmHg**, *t*(19) = 2.20, *p* = 0.02.

---

# ↔️ One-Tailed vs Two-Tailed Tests

## Two-Tailed

Question:

> Is the mean **different** from 140?

Hypotheses:

\[
H_0:\mu=140
\]

\[
H_1:\mu\neq140
\]

R code:

```r
t.test(SB, mu=140)
```

---

## One-Tailed (Greater)

Question:

> Is the mean **greater than** 140?

```r
t.test(
SB,
mu=140,
alternative="greater"
)
```

---

## One-Tailed (Less)

Question:

> Is the mean **less than** 140?

```r
t.test(
SB,
mu=140,
alternative="less"
)
```

---

# ⚠️ Common Mistakes

❌ Using a One-Sample t-test for two groups

Use an **Independent** or **Paired** t-test instead.

---

❌ Ignoring normality

Always inspect:

- Histogram
- Q-Q plot
- Shapiro–Wilk test

---

❌ Using a one-tailed test after looking at the data

Choose the hypothesis **before** analysing the data.

---

❌ Confusing SD and SE

Remember:

- SD describes variation in the data.
- SE describes the precision of the sample mean.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| One sample (normal) | ✅ One-Sample t-test |
| One sample (non-normal) | One-Sample Wilcoxon Signed-Rank Test |
| Two independent groups | Independent Two-Sample t-test |
| Two paired measurements | Paired t-test |

---

# ⚡ Quick R Cheat Sheet

| Task | R Code |
|------|--------|
| Mean | `mean(SB)` |
| Median | `median(SB)` |
| Standard deviation | `sd(SB)` |
| Standard error | `sd(SB)/sqrt(length(SB))` |
| Histogram | `hist(SB)` |
| Q-Q plot | `qqnorm(SB)` |
| Q-Q line | `qqline(SB)` |
| Shapiro–Wilk test | `shapiro.test(SB)` |
| One-sample t-test | `t.test(SB, mu=140)` |
| One-tailed (greater) | `t.test(SB, mu=140, alternative="greater")` |
| One-tailed (less) | `t.test(SB, mu=140, alternative="less")` |

---

# 🎯 Key Takeaways

- 🧪 Compare **one sample mean** with a known value.
- 📊 Data should be approximately **normally distributed**.
- 📈 Check assumptions before running the test.
- 💻 Use `t.test()` with the `mu` argument.
- 📉 If **p < 0.05**, reject the null hypothesis.
- 📝 Report the mean, *t*-value, degrees of freedom, and *p*-value.
