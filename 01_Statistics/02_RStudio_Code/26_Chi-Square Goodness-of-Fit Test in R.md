# 🧪 Chi-Square Goodness-of-Fit Test in R

> **Data Analysis for Life Science**

The **Chi-Square Goodness-of-Fit Test** is used to determine whether the **observed frequencies of a single categorical variable match an expected (theoretical) distribution**.

Unlike the **Chi-Square Test of Independence**, which compares **two categorical variables**, the Goodness-of-Fit Test analyzes **only one categorical variable**.

---

# 📚 Table of Contents

1. Purpose
2. Why Use the Goodness-of-Fit Test?
3. When to Use
4. Difference from Chi-Square Independence
5. Data Requirements
6. Assumptions
7. Hypotheses
8. How the Test Works
9. Example Dataset
10. Step 1 – Enter the Data
11. Step 2 – Specify Expected Probabilities
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

The **Chi-Square Goodness-of-Fit Test** determines whether **observed frequencies match an expected theoretical distribution**.

It answers questions like:

> **"Does my observed data follow what I expected?"**

---

# 🤔 Why Use the Goodness-of-Fit Test?

Sometimes we already know the expected proportions from:

- Genetics
- Probability
- Previous research
- Theory

We want to check whether our observed data matches those expectations.

---

## Examples

- Is a coin fair?
- Is a dice fair?
- Does offspring follow Mendelian genetics?
- Are blood groups distributed as expected?

---

# 📌 When to Use

Use this test when:

- ✅ One categorical variable
- ✅ Data are frequencies (counts)
- ✅ Expected probabilities are known

---

# 🆚 Difference from Chi-Square Independence

| Chi-Square Independence | Chi-Square Goodness-of-Fit |
|--------------------------|----------------------------|
| Two categorical variables | One categorical variable |
| Tests association | Tests agreement with an expected distribution |
| Example: Sex vs Smoking | Example: Fair coin |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Variable | One categorical variable |
| Data | Counts (frequencies) |
| Expected probabilities | Known beforehand |

---

# 📋 Assumptions

The Goodness-of-Fit Test assumes:

- Independent observations
- Data are frequencies (counts)
- Categories are mutually exclusive
- Expected frequencies should generally be **≥ 5**

---

# 🧪 Hypotheses

Example:

Testing whether a coin is fair.

### Null Hypothesis

\[
H_0:
\]

The observed frequencies follow the expected distribution.

(The coin is fair.)

---

### Alternative Hypothesis

\[
H_1:
\]

The observed frequencies do not follow the expected distribution.

(The coin is not fair.)

---

# 🧠 How the Test Works

The test compares:

- **Observed frequencies**
- **Expected frequencies**

If they are very different,

↓

Large χ² statistic

↓

Small p-value

↓

Reject H₀.

---

## Example

Suppose we flip a coin **100 times**.

Observed

| Outcome | Count |
|----------|------:|
| Heads | 60 |
| Tails | 40 |

Expected

| Outcome | Count |
|----------|------:|
| Heads | 50 |
| Tails | 50 |

The Chi-Square Test asks:

> **Is the difference between 60/40 and 50/50 large enough to conclude the coin is not fair?**

---

# 📂 Example Dataset

Suppose we observed the following genotype counts:

| Genotype | Count |
|-----------|------:|
| AA | 4 |
| Aa | 10 |
| aa | 6 |

Expected Mendelian ratio:

```text
1 : 2 : 1
```

---

# 💻 Step 1 – Enter the Data

```r
observed <- c(
4,
10,
6
)
```

---

# 💻 Step 2 – Specify Expected Probabilities

Expected ratio

```text
1 : 2 : 1
```

Convert to probabilities

```r
expected <- c(
0.25,
0.50,
0.25
)
```

---

# 💻 Step 3 – Run the Test

```r
chisq.test(
observed,
p = expected
)
```

---

# 📊 Example Output

```text
Pearson's Chi-squared test

X-squared = 0.40

df = 2

p-value = 0.82
```

---

# 🔍 Understanding the Output

## χ² Statistic

Measures the difference between:

- Observed counts
- Expected counts

Small χ²

↓

Observed ≈ Expected

Large χ²

↓

Observed differs from Expected

---

## Degrees of Freedom

For Goodness-of-Fit:

```text
df = Number of categories − 1
```

Example

Three genotypes

↓

```text
df = 3 − 1

df = 2
```

---

## p-value

Compare with α = 0.05.

If

```text
p < 0.05
```

Reject H₀.

If

```text
p ≥ 0.05
```

Do not reject H₀.

---

# 📈 Interpretation

Suppose

```text
χ² = 0.40

p = 0.82
```

Since

```text
0.82 > 0.05
```

Do not reject H₀.

Conclusion:

The observed genotype frequencies are **consistent with the expected 1:2:1 Mendelian ratio**.

---

# 📝 Reporting Results

Example

> A Chi-Square Goodness-of-Fit Test showed that the observed genotype frequencies did not differ significantly from the expected 1:2:1 Mendelian ratio, χ²(2) = 0.40, p = 0.82.

---

# ⚠️ Common Mistakes

❌ Using percentages instead of counts.

Always use **raw frequencies**.

---

❌ Forgetting to specify expected probabilities.

Use the `p` argument in `chisq.test()`.

---

❌ Confusing expected counts with probabilities.

R requires **probabilities**, not counts.

Example

```r
p = c(0.25, 0.50, 0.25)
```

---

❌ Using this test for two variables.

Use the **Chi-Square Test of Independence** instead.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| One categorical variable | ✅ Chi-Square Goodness-of-Fit |
| Two categorical variables | Chi-Square Independence |
| Paired categorical variables | McNemar's Test |
| Small expected counts | Fisher's Exact Test |
| Two population proportions | Two-Proportion Z-Test |

---

# 🌳 Decision Workflow

```text
Categorical data
        │
        ▼
How many variables?
        │
 ┌──────┴────────┐
 │               │
 ▼               ▼
One variable   Two variables
 │               │
 ▼               ▼
Expected      Independent?
distribution?      │
 │                  ▼
 ▼          Chi-Square
Goodness-   Independence
of-Fit
```

---

# ⚡ Quick R Cheat Sheet

```r
# Observed counts
observed <- c(
4,
10,
6
)

# Expected probabilities
expected <- c(
0.25,
0.50,
0.25
)

# Chi-Square Goodness-of-Fit Test
chisq.test(
observed,
p = expected
)
```

---

# 📊 Chi-Square Tests Comparison

| Feature | Goodness-of-Fit | Independence |
|----------|-----------------|--------------|
| Variables | One | Two |
| Tests | Observed vs Expected | Association |
| Data | Counts | Counts |
| Example | Fair coin | Sex vs Smoking |

---

# 🎯 Key Takeaways

- 🧪 The **Chi-Square Goodness-of-Fit Test** compares **observed frequencies** with **expected theoretical frequencies**.
- 📊 It is used for **one categorical variable**.
- 📋 Expected probabilities must be known beforehand.
- ⚠️ Data must be **raw counts**, not percentages.
- 💻 In R, use `chisq.test(observed, p = expected)`.
- 🔍 If the p-value is less than 0.05, reject the null hypothesis and conclude that the observed distribution differs from the expected distribution.
