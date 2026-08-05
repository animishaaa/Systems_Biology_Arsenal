# 🧪 Two-Proportion Z-Test in R

> **Data Analysis for Life Science**

The **Two-Proportion Z-Test** is used to compare **two independent population proportions**.

Unlike the **Independent t-test**, which compares **means**, the Two-Proportion Z-Test compares **proportions (percentages)**.

---

# 📚 Table of Contents

1. Purpose
2. Why Use the Two-Proportion Z-Test?
3. When to Use
4. Difference from Chi-Square Test
5. Data Requirements
6. Assumptions
7. Hypotheses
8. How the Test Works
9. Example Dataset
10. Step 1 – Enter the Data
11. Step 2 – Run the Test
12. Understanding the Output
13. Confidence Interval
14. Interpretation
15. Reporting Results
16. Common Mistakes
17. Related Tests
18. Decision Workflow
19. Quick R Cheat Sheet
20. Key Takeaways

---

# 🎯 Purpose

The **Two-Proportion Z-Test** compares the **proportions of a characteristic** between **two independent groups**.

It answers questions like:

> **"Are the proportions different?"**

---

# 🤔 Why Use the Two-Proportion Z-Test?

Sometimes we are interested in **proportions**, not numerical values.

Examples:

- Smoking rate in males vs females
- Recovery rate with Drug A vs Placebo
- Vaccination success rate
- Disease prevalence between two cities

Since the outcome is a **proportion**, we use the **Two-Proportion Z-Test**.

---

# 📌 When to Use

Use this test when:

- ✅ Two independent groups
- ✅ Outcome is binary
- ✅ Comparing proportions
- ✅ Sample sizes are sufficiently large

---

## Examples

| Group 1 | Group 2 |
|----------|----------|
| Male | Female |
| Drug | Placebo |
| Vaccinated | Unvaccinated |
| Smoker | Non-smoker |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Groups | Two independent groups |
| Outcome | Binary |
| Data | Counts or proportions |
| Sample Size | Large |

---

# 📋 Assumptions

The Two-Proportion Z-Test assumes:

- Independent samples
- Binary outcome
- Random sampling
- Large sample size

Rule of thumb:

```text
np ≥ 5

n(1-p) ≥ 5
```

for both groups.

If these assumptions are not met:

➡️ Use **Fisher's Exact Test**.

---

# 🧪 Hypotheses

Example:

Compare smoking rates in males and females.

### Null Hypothesis

\[
H_0:
\]

The two population proportions are equal.

\[
p_1 = p_2
\]

---

### Alternative Hypothesis

\[
H_1:
\]

The two population proportions are different.

\[
p_1 \neq p_2
\]

---

# 🧠 How the Test Works

The test compares:

- Sample proportion in Group 1
- Sample proportion in Group 2

If the difference is much larger than expected by chance,

↓

Large Z statistic

↓

Small p-value

↓

Reject H₀.

---

## Example

Suppose:

| Group | Smokers | Total |
|--------|---------:|------:|
| Male | 15 | 100 |
| Female | 20 | 100 |

Sample proportions

```text
Male = 15%

Female = 20%
```

The test asks:

> **Is the 5% difference statistically significant?**

---

# 📂 Example Dataset

```r
success <- c(
15,
20
)

total <- c(
100,
100
)
```

---

# 💻 Step 1 – Enter the Data

```r
success <- c(
15,
20
)

total <- c(
100,
100
)
```

---

# 💻 Step 2 – Run the Test

```r
prop.test(
success,
total,
correct = FALSE
)
```

> **Note:** `prop.test()` performs a Chi-Square approximation for comparing proportions. For large samples, this is equivalent to the Two-Proportion Z-Test and is the standard approach in R.

---

# 📊 Example Output

```text
2-sample test for equality of proportions

X-squared = 0.86

df = 1

p-value = 0.35

95 percent confidence interval

-0.06  0.16

sample estimates

prop 1 = 0.15

prop 2 = 0.20
```

---

# 🔍 Understanding the Output

## Sample Proportions

```text
Male = 15%

Female = 20%
```

These are the observed proportions.

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

## Confidence Interval

The confidence interval represents:

```text
Difference in proportions

(p₁ − p₂)
```

Example:

```text
95% CI

[-0.06, 0.16]
```

Since

```text
0 is inside the interval
```

↓

No significant difference.

---

# 📈 Interpretation

Suppose

```text
p = 0.35
```

Since

```text
0.35 > 0.05
```

Do not reject H₀.

Conclusion:

There is **no statistically significant difference** between the smoking proportions of males and females.

---

# 📝 Reporting Results

Example

> A Two-Proportion Z-Test showed no significant difference in smoking prevalence between males (15%) and females (20%), p = 0.35.

---

# ⚠️ Common Mistakes

❌ Using paired data.

The groups must be **independent**.

---

❌ Using small sample sizes.

If expected counts are too small:

➡️ Use **Fisher's Exact Test**.

---

❌ Confusing proportions with means.

This test compares **percentages**, not averages.

---

❌ Ignoring the confidence interval.

If the confidence interval includes **0**, the proportions are not significantly different.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| Two independent proportions | ✅ Two-Proportion Z-Test |
| Two categorical variables | Chi-Square Independence |
| Small 2 × 2 tables | Fisher's Exact Test |
| Paired categorical data | McNemar's Test |
| Compare means | Independent t-test |

---

# 🌳 Decision Workflow

```text
Binary Outcome
        │
        ▼
Independent Groups?
        │
   ┌────┴────┐
   │         │
  Yes        No
   │         │
   ▼         ▼
Large Sample? McNemar's
   │          Test
   ▼
 ┌──────┴──────┐
 │             │
 ▼             ▼
Two-Proportion Fisher's
Z-Test         Exact Test
```

---

# ⚡ Quick R Cheat Sheet

```r
# Number of successes
success <- c(
15,
20
)

# Sample sizes
total <- c(
100,
100
)

# Two-Proportion Test
prop.test(
success,
total,
correct = FALSE
)
```

---

# 📊 Comparison of Categorical Tests

| Test | Purpose |
|------|---------|
| Chi-Square Independence | Two categorical variables |
| Chi-Square Goodness-of-Fit | One categorical variable |
| McNemar's Test | Paired categorical data |
| Fisher's Exact Test | Small sample 2 × 2 table |
| ✅ Two-Proportion Z-Test | Compare two independent proportions |

---

# 📊 Independent t-test vs Two-Proportion Z-Test

| Feature | Independent t-test | Two-Proportion Z-Test |
|----------|-------------------|-----------------------|
| Compares | Means | Proportions |
| Outcome | Continuous | Binary |
| Data Example | Blood pressure | Smoking (Yes/No) |
| Test Statistic | t | Z (approximated by χ² in `prop.test()`) |
| Parametric | Yes | Yes |

---

# 🎯 Key Takeaways

- 🧪 The **Two-Proportion Z-Test** compares **two independent proportions**.
- 📊 It is used for **binary outcomes** such as Yes/No, Success/Failure, or Smoker/Non-smoker.
- 📋 The groups must be **independent**, and sample sizes should be sufficiently large.
- 💻 In R, use `prop.test()` for comparing two proportions.
- 📈 The confidence interval estimates the difference between the two population proportions.
- 🔍 If the p-value is less than 0.05, reject the null hypothesis and conclude that the two proportions differ significantly.
