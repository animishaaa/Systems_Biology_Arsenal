# 🧪 McNemar's Test in R

> **Data Analysis for Life Science**

The **McNemar's Test** is used to determine whether there is a **significant change in paired categorical (binary) data**.

It is the **non-parametric equivalent of the paired t-test for categorical data**.

Unlike the Chi-Square Test of Independence, McNemar's Test is used when **the same subjects are measured twice**.

---

# 📚 Table of Contents

1. Purpose
2. Why Use McNemar's Test?
3. When to Use
4. Difference from Chi-Square Test
5. Data Requirements
6. Assumptions
7. Hypotheses
8. How the Test Works
9. Example Dataset
10. Step 1 – Create the Contingency Table
11. Step 2 – Run McNemar's Test
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

The **McNemar's Test** determines whether the **proportion of subjects changes between two paired categorical measurements**.

It answers questions like:

> **Did the treatment change the outcome?**

---

# 🤔 Why Use McNemar's Test?

Sometimes we measure the **same individuals twice**.

Examples:

- Before treatment vs After treatment
- Before vaccination vs After vaccination
- Positive vs Negative test before and after surgery
- Diagnostic Test A vs Diagnostic Test B on the same patient

Since the observations are **paired**, we cannot use the Chi-Square Test of Independence.

Instead, we use **McNemar's Test**.

---

# 📌 When to Use

Use McNemar's Test when:

- ✅ Two paired categorical measurements
- ✅ Binary outcome (Yes/No, Positive/Negative, Success/Failure)
- ✅ Same subjects measured twice

---

## Examples

| Before | After |
|---------|--------|
| Positive | Negative |
| Smoker | Non-Smoker |
| Disease | Healthy |
| Passed | Failed |

---

# 🆚 Difference from Chi-Square Independence

| Chi-Square Independence | McNemar's Test |
|--------------------------|----------------|
| Independent groups | Same subjects |
| Two categorical variables | Paired categorical data |
| Tests association | Tests change over time or conditions |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Variables | Two categorical measurements |
| Outcome | Binary |
| Subjects | Same individuals |
| Design | Paired |

---

# 📋 Assumptions

McNemar's Test assumes:

- Paired observations
- Binary outcome
- Each subject contributes only one paired observation
- Pairs are independent of other pairs

---

# 🧪 Hypotheses

Example:

Recovery before and after treatment.

### Null Hypothesis

\[
H_0:
\]

The probability of change is the same in both directions.

(No treatment effect.)

---

### Alternative Hypothesis

\[
H_1:
\]

The probabilities are different.

(The treatment changes the outcome.)

---

# 🧠 How the Test Works

McNemar's Test focuses **only on subjects who changed**.

Suppose:

| Before | After | Count |
|---------|--------|------:|
| Yes | Yes | 20 |
| Yes | No | 10 |
| No | Yes | 5 |
| No | No | 15 |

Notice:

- 20 stayed Yes
- 15 stayed No

These **do not contribute** to the test.

Only these matter:

- Yes → No = 10
- No → Yes = 5

The test asks:

> **Are these changes balanced?**

If one direction is much larger than the other,

↓

Treatment likely had an effect.

---

# 📂 Example Dataset

Create a 2 × 2 contingency table.

```r
data <- matrix(
c(
20,10,
5,15
),
nrow = 2,
byrow = TRUE
)

data
```

Output

```text
     [,1] [,2]

[1,]   20   10

[2,]    5   15
```

---

# 💻 Step 1 – Run McNemar's Test

```r
mcnemar.test(data)
```

---

# 📊 Example Output

```text
McNemar's Chi-squared test

McNemar's chi-squared = 1.67

df = 1

p-value = 0.30
```

---

# 🔍 Understanding the Output

## McNemar χ²

Measures whether the number of changes in one direction differs from the number of changes in the opposite direction.

Large χ²

↓

Large imbalance

↓

Evidence against H₀.

---

## Degrees of Freedom

Always

```text
df = 1
```

because the table is always **2 × 2**.

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
p = 0.30
```

Since

```text
0.30 > 0.05
```

Do not reject H₀.

Conclusion:

There is **no statistically significant change** between the before and after measurements.

---

# 📝 Reporting Results

Example

> McNemar's Test showed no significant difference in recovery status before and after treatment, χ²(1) = 1.67, p = 0.30.

---

# ⚠️ Common Mistakes

❌ Using McNemar's Test for independent groups.

Use the **Chi-Square Test of Independence** instead.

---

❌ Using more than two outcome categories.

McNemar's Test is designed for **binary outcomes**.

---

❌ Including unpaired observations.

Each row must correspond to the **same subject measured twice**.

---

❌ Thinking all cells contribute equally.

McNemar's Test mainly evaluates the **discordant pairs**:

- Yes → No
- No → Yes

The concordant pairs (Yes → Yes and No → No) do not determine the test statistic.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| Two independent categorical variables | Chi-Square Independence |
| One categorical variable | Chi-Square Goodness-of-Fit |
| Two paired categorical variables | ✅ McNemar's Test |
| Small independent 2×2 table | Fisher's Exact Test |
| Two independent proportions | Two-Proportion Z-Test |

---

# 🌳 Decision Workflow

```text
Categorical Data
        │
        ▼
Same subjects?
        │
   ┌────┴────┐
   │         │
  Yes        No
   │         │
   ▼         ▼
Binary?   Chi-Square
   │      Independence
   ▼
McNemar's
Test
```

---

# ⚡ Quick R Cheat Sheet

```r
# Create 2×2 table
data <- matrix(
c(
20,10,
5,15
),
nrow = 2,
byrow = TRUE
)

# Run McNemar's Test
mcnemar.test(data)
```

---

# 📊 Comparison of Categorical Tests

| Test | Purpose |
|------|---------|
| Chi-Square Independence | Two independent categorical variables |
| Chi-Square Goodness-of-Fit | One categorical variable |
| McNemar's Test | Two paired categorical measurements |
| Fisher's Exact Test | Small sample 2×2 table |
| Two-Proportion Z-Test | Compare two independent proportions |

---

# 🎯 Key Takeaways

- 🧪 McNemar's Test compares **paired categorical data**.
- 👥 It is used when the **same subjects are measured twice**.
- 📊 The outcome must be **binary**.
- 🔄 The test focuses on **subjects who changed categories**.
- 💻 In R, use `mcnemar.test()`.
- 🔍 If the p-value is less than 0.05, reject the null hypothesis and conclude that there is a significant change between the paired measurements.
