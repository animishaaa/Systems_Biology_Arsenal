# 📊 Statistical Tests Cheat Sheet
## Data Analysis for Life Science

---

# 📚 1. Choosing the Correct Statistical Test

```text
START
   │
   ▼
What type of data?
   │
 ┌─┴──────────────┐
 │                │
Continuous     Categorical
 │                │
 ▼                ▼
Normal?       Chi-square Family
 │
 ├──── Yes ───► Parametric Tests
 │
 └──── No ───► Non-parametric Tests
```

---

# 🟢 2. Parametric Tests

## 📖 What are Parametric Tests?

Parametric tests are statistical tests that:

- Assume the data follow an approximately **normal distribution**
- Use the **actual numerical values**
- Compare **means**
- Have **higher statistical power** when assumptions are met

### ✅ Assumptions

- Continuous data
- Approximately normal distribution
- Independent observations
- Similar variances (for some tests)

---

## 📊 Parametric Test Decision Tree

| Situation | Test |
|------------|------|
| One sample vs known value | One-sample t-test |
| Two independent groups | Independent t-test |
| Two paired measurements | Paired t-test |
| Three or more independent groups | One-way ANOVA |
| Three or more paired measurements | Repeated Measures ANOVA |
| Linear relationship | Pearson Correlation |
| Prediction | Linear Regression |

---

# 2.1 One-Sample t-test

## Purpose

Compare the mean of one sample with a known population mean.

### Example

Is the average height different from 170 cm?

### Hypotheses

H₀: μ = 170

H₁: μ ≠ 170

---

# 2.2 Independent t-test

## Purpose

Compare means of two independent groups.

### Examples

- Male vs Female
- Drug vs Control

### Assumptions

- Continuous
- Normal
- Independent
- Equal variance (classic t-test)

### R

```r
t.test(y ~ group)

t.test(y ~ group, var.equal=TRUE)
```

---

# 2.3 Paired t-test

## Purpose

Compare two related measurements.

Examples

- Before vs After
- Left eye vs Right eye

### Assumptions

- Paired observations
- Differences approximately normal

---

# 2.4 One-way ANOVA

## Purpose

Compare means of ≥3 independent groups.

### H₀

All means are equal.

### H₁

At least one mean differs.

### Important

ANOVA tells us **that** a difference exists,
NOT **where** it exists.

Requires Post Hoc Tests.

---

# 2.5 Repeated Measures ANOVA

## Purpose

Compare ≥3 related measurements.

Example

Before

↓

1 Month

↓

3 Months

↓

6 Months

Same patient.

---

# 🔵 3. Post Hoc Tests

## Why?

Performed **after a significant ANOVA** to identify which groups differ.

ANOVA

↓

Difference exists

↓

Post Hoc

↓

Which groups differ?

---

## Types

### Tukey HSD

✔ Compare every pair

Best for all pairwise comparisons.

---

### Bonferroni

Adjusts p-values to reduce Type I error.

Example

p = 0.04

3 comparisons

Adjusted p

= 0.12

---

### Fisher LSD

Like multiple t-tests.

More powerful

Less protection against Type I error.

---

### Dunnett

Compare every treatment against one control.

---

### Holm

Improved Bonferroni.

---

# 🔴 4. Non-Parametric Tests

## What are Non-Parametric Tests?

Used when:

- Data are not normal
- Ordinal data
- Small sample
- Outliers present

Instead of raw values,
they usually compare **ranks**.

---

## Decision Table

| Situation | Test |
|------------|------|
| One sample | Wilcoxon Signed-Rank (one-sample version) |
| Two independent groups | Mann-Whitney U |
| Two paired groups | Wilcoxon Signed-Rank |
| Paired, no symmetry | Sign Test |
| ≥3 independent groups | Kruskal-Wallis |
| ≥3 paired groups | Friedman Test |
| Monotonic relationship | Spearman Correlation |

---

# 4.1 Mann-Whitney U Test

Alternative to Independent t-test.

Used for

- Two independent groups
- Ordinal
- Non-normal continuous

---

# 4.2 Wilcoxon Signed-Rank Test

Alternative to Paired t-test.

Uses

✔ Direction

✔ Magnitude

✔ Ranks

Assumes

Differences approximately symmetric.

---

# 4.3 Sign Test

Simplest paired non-parametric test.

Uses

✔ Direction only

Ignores magnitude.

Use when

Differences are NOT symmetric.

---

# 4.4 Kruskal-Wallis Test

Alternative to One-way ANOVA.

Compare ≥3 independent groups.

---

# 4.5 Friedman Test

Alternative to Repeated Measures ANOVA.

Compare ≥3 paired measurements.

---

# 🟠 5. Categorical Data Tests

These tests analyze counts or frequencies rather than numerical measurements.

---

# 5.1 Chi-square Test of Independence

## Purpose

Tests whether two categorical variables are associated.

Examples

Smoking vs Cancer

Male vs Disease

### H₀

Variables are independent.

---

# 5.2 Chi-square Goodness-of-Fit

## Purpose

Tests whether observed frequencies match expected frequencies.

Example

Fair coin

Expected

50 Heads

50 Tails

---

# 5.3 Fisher's Exact Test

Alternative to Chi-square.

Use when

Expected frequencies are too small.

Especially

Expected cell count <5.

Common for 2×2 contingency tables.

---

# 5.4 McNemar's Test

For paired categorical data.

Example

COVID test

Before

↓

After

Same patients.

---

# 5.5 Two-Proportion Z-test

Purpose

Compare two independent population proportions.

Example

Smoking rates

Men vs Women

Large sample sizes required.

---

# 🟣 6. Correlation & Regression

## Pearson Correlation

Continuous

Normal

Linear relationship

---

## Spearman Correlation

Ordinal

Non-normal

Monotonic relationship

---

## Linear Regression

Predict one continuous variable from another.

---

# 📌 Final Master Table

| Data | Situation | Parametric | Non-parametric |
|------|-----------|------------|----------------|
| Continuous | One sample | One-sample t-test | Wilcoxon (one-sample) |
| Continuous | 2 Independent | Independent t-test | Mann-Whitney U |
| Continuous | 2 Paired | Paired t-test | Wilcoxon Signed-Rank |
| Continuous | ≥3 Independent | One-way ANOVA | Kruskal-Wallis |
| Continuous | ≥3 Paired | Repeated Measures ANOVA | Friedman |
| Categorical | Independent | Chi-square / Fisher / Z-test | — |
| Categorical | Paired | McNemar | — |
| Relationship | Continuous | Pearson | Spearman |

---

# 🎯 Decision Tree

```text
Continuous?

│

├── Normal

│ │

│ ├── 1 Sample → One-sample t-test

│ ├── 2 Independent → Independent t-test

│ ├── 2 Paired → Paired t-test

│ ├── ≥3 Independent → One-way ANOVA

│ └── ≥3 Paired → Repeated Measures ANOVA

│

└── Non-normal

│

├── 2 Independent → Mann-Whitney

├── 2 Paired → Wilcoxon / Sign Test

├── ≥3 Independent → Kruskal-Wallis

└── ≥3 Paired → Friedman

Categorical

├── Chi-square Independence

├── Chi-square Goodness-of-Fit

├── Fisher Exact

├── McNemar

└── Two-Proportion Z-test
```
