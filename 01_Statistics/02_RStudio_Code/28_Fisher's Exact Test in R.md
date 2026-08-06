# 🧪 Fisher's Exact Test in R

> **Data Analysis for Life Science**

The **Fisher's Exact Test** is used to determine whether **two categorical variables are associated** when the **sample size is small**.

It is the **preferred alternative to the Chi-Square Test of Independence** when the expected frequencies in one or more cells are **less than 5**.

Unlike the Chi-Square Test, Fisher's Exact Test calculates the **exact probability** of observing the data.

---

# 📚 Table of Contents

1. Purpose
2. Why Use Fisher's Exact Test?
3. When to Use
4. Fisher's Test vs Chi-Square Test
5. Data Requirements
6. Assumptions
7. Hypotheses
8. How the Test Works
9. Example Dataset
10. Step 1 – Create a Contingency Table
11. Step 2 – Run Fisher's Exact Test
12. Understanding the Output
13. Interpretation
14. Reporting Results
15. Common Mistakes
16. Related Tests
17. Decision Workflow
18. Quick R Cheat Sheet
19. Key Takeaways

---

# 🎯 Purpose

The **Fisher's Exact Test** determines whether **two categorical variables are associated** when sample sizes are **too small** for the Chi-Square Test.

It answers questions like:

> **"Are these two categorical variables associated, even with a very small sample?"**

---

# 🤔 Why Use Fisher's Exact Test?

The Chi-Square Test assumes that the **expected frequency** in each cell is sufficiently large.

A common guideline is:

```text
Expected frequency ≥ 5
```

If one or more expected frequencies are **less than 5**, the Chi-Square approximation may become inaccurate.

Instead, use **Fisher's Exact Test**, which computes the **exact p-value**.

---

# 📌 When to Use

Use Fisher's Exact Test when:

- ✅ Two categorical variables
- ✅ Independent observations
- ✅ 2 × 2 contingency table
- ✅ Small sample size
- ✅ Expected frequency < 5 in one or more cells

---

## Examples

- Treatment vs Recovery (small clinical trial)
- Disease vs Exposure (rare disease)
- Mutation vs Cancer
- Vaccine vs Infection (small pilot study)

---

# ⚖️ Fisher's Test vs Chi-Square Test

| Chi-Square Test | Fisher's Exact Test |
|-----------------|---------------------|
| Large samples | Small samples |
| Approximate p-value | Exact p-value |
| Expected counts ≥ 5 | Expected counts < 5 |
| Fast for large datasets | Ideal for 2 × 2 tables |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Variable 1 | Categorical |
| Variable 2 | Categorical |
| Observations | Independent |
| Table | Usually 2 × 2 |

---

# 📋 Assumptions

Fisher's Exact Test assumes:

- Independent observations
- Two categorical variables
- Frequency data (counts)
- Small sample size

Unlike the Chi-Square Test:

- No minimum expected frequency is required.

---

# 🧪 Hypotheses

Example:

Does treatment affect recovery?

### Null Hypothesis

\[
H_0:
\]

Treatment and recovery are independent.

(No association.)

---

### Alternative Hypothesis

\[
H_1:
\]

Treatment and recovery are associated.

---

# 🧠 How the Test Works

Instead of using a Chi-Square approximation,

Fisher's Exact Test calculates the **exact probability** of observing the contingency table (or one more extreme) assuming the null hypothesis is true.

This makes it accurate even with very small samples.

---

# 📂 Example Dataset

Suppose we conduct a small clinical study.

| | Recovered | Not Recovered |
|----------------|-----------:|--------------:|
| Drug | 8 | 2 |
| Placebo | 3 | 7 |

---

# 💻 Step 1 – Create a Contingency Table

```r
data <- matrix(
c(
8,2,
3,7
),
nrow = 2,
byrow = TRUE
)

data
```

Output

```text
     [,1] [,2]

[1,]   8   2

[2,]   3   7
```

---

# 💻 Step 2 – Run Fisher's Exact Test

```r
fisher.test(data)
```

---

# 📊 Example Output

```text
Fisher's Exact Test for Count Data

p-value = 0.035

alternative hypothesis:
true odds ratio is not equal to 1

95 percent confidence interval:
1.12  62.5

sample estimates:
odds ratio = 8.5
```

---

# 🔍 Understanding the Output

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

## Odds Ratio

The odds ratio measures the strength of the association.

Interpretation:

| Odds Ratio | Meaning |
|------------|---------|
| = 1 | No association |
| > 1 | Positive association |
| < 1 | Negative association |

Example:

```text
Odds Ratio = 8.5
```

Patients receiving the drug had **8.5 times higher odds of recovery** compared with the placebo group.

---

## Confidence Interval

If the **95% confidence interval** includes **1**:

↓

No significant association.

If it **does not include 1**:

↓

Significant association.

---

# 📈 Interpretation

Suppose

```text
p = 0.035
```

Since

```text
0.035 < 0.05
```

Reject the null hypothesis.

Conclusion:

There is a statistically significant association between treatment and recovery.

---

# 📝 Reporting Results

Example

> Fisher's Exact Test showed a significant association between treatment and recovery (odds ratio = 8.5, p = 0.035).

---

# ⚠️ Common Mistakes

❌ Using Fisher's Test for large datasets.

The Chi-Square Test is generally more appropriate for large samples.

---

❌ Using percentages instead of counts.

Always provide **raw frequencies**.

---

❌ Using dependent observations.

Observations must be independent.

---

❌ Ignoring the odds ratio.

The p-value indicates significance, while the odds ratio describes the strength of the association.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| Two independent categorical variables (large sample) | Chi-Square Independence |
| Two independent categorical variables (small sample) | ✅ Fisher's Exact Test |
| Paired categorical variables | McNemar's Test |
| One categorical variable | Chi-Square Goodness-of-Fit |
| Two independent proportions | Two-Proportion Z-Test |

---

# 🌳 Decision Workflow

```text
Categorical Data
        │
        ▼
Two variables?
        │
        ▼
Independent?
        │
        ▼
Expected counts ≥ 5?
        │
   ┌────┴────┐
   │         │
  Yes        No
   │         │
   ▼         ▼
Chi-Square  Fisher's
Independence Exact Test
```

---

# ⚡ Quick R Cheat Sheet

```r
# Create 2 × 2 table
data <- matrix(
c(
8,2,
3,7
),
nrow = 2,
byrow = TRUE
)

# Fisher's Exact Test
fisher.test(data)
```

---

# 📊 Comparison of Categorical Tests

| Test | Purpose |
|------|---------|
| Chi-Square Independence | Two independent categorical variables (large sample) |
| Fisher's Exact Test | Two independent categorical variables (small sample) |
| Chi-Square Goodness-of-Fit | One categorical variable |
| McNemar's Test | Paired categorical data |
| Two-Proportion Z-Test | Compare two independent proportions |

---

# 🎯 Key Takeaways

- 🧪 Fisher's Exact Test is used for **two independent categorical variables**.
- 📊 It is preferred when **expected cell frequencies are less than 5**.
- 📋 It calculates an **exact p-value**, making it more accurate for small samples.
- 📈 It also reports an **odds ratio**, which measures the strength of the association.
- 💻 In R, use `fisher.test()`.
- 🔍 If the p-value is less than 0.05, reject the null hypothesis and conclude that an association exists.
