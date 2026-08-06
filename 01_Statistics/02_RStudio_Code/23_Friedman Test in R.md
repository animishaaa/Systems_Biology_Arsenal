# 🧪 Friedman Test in R

> **Data Analysis for Life Science**

The **Friedman Test** is the **non-parametric alternative** to the **Repeated-Measures ANOVA**.

It compares **three or more related (paired) groups** when the data are **not normally distributed**.

Instead of comparing **means**, it compares the **ranked observations** across repeated measurements.

---

# 📚 Table of Contents

1. Purpose
2. Why Use the Friedman Test?
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
15. Post-Hoc Testing
16. Reporting Results
17. Common Mistakes
18. Related Tests
19. Decision Workflow
20. Quick R Cheat Sheet
21. Key Takeaways

---

# 🎯 Purpose

The **Friedman Test** compares **three or more related measurements**.

It is used when the assumptions of a **Repeated-Measures ANOVA** are not met.

---

# 🤔 Why Use the Friedman Test?

Repeated-Measures ANOVA assumes:

- Normally distributed repeated measurements
- Continuous data
- Related observations

If these assumptions are violated, use the **Friedman Test**.

---

# 📌 When to Use

Use the Friedman Test when:

- ✅ Three or more related groups
- ✅ Same subjects measured multiple times
- ✅ Continuous or ordinal data
- ✅ Data are not normally distributed

---

## Examples

- Blood pressure measured:
  - Before treatment
  - After Drug A
  - After Drug B

- Pain score:
  - Week 1
  - Week 2
  - Week 3

- Cholesterol measured every month

---

# ⚖️ Parametric vs Non-Parametric

| Parametric | Non-Parametric |
|------------|----------------|
| Repeated-Measures ANOVA | ✅ Friedman Test |
| Tests means | Tests ranked observations |
| Requires normality | No normality assumption |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Groups | Three or more |
| Relationship | Related (Paired) |
| Outcome | Continuous or Ordinal |

---

# 📋 Assumptions

The Friedman Test assumes:

- Related observations
- Same subjects measured repeatedly
- Continuous or ordinal data

Unlike Repeated-Measures ANOVA:

- ❌ Normality is **not required**

---

# 🧪 Hypotheses

Example:

Compare blood pressure:

- Before treatment
- After Drug A
- After Drug B

### Null Hypothesis

\[
H_0:
\]

All treatment conditions have the same distribution.

(No treatment effect.)

---

### Alternative Hypothesis

\[
H_1:
\]

At least one treatment condition differs.

---

# 🧠 How the Test Works

Instead of comparing means, the Friedman Test:

1. Looks at each subject separately.
2. Ranks that subject's repeated measurements.
3. Repeats this for every subject.
4. Adds the ranks for each treatment.
5. Calculates a Friedman χ² statistic.

Because each subject is compared with themselves, differences between subjects are removed.

---

## Example

| Subject | Before | Drug A | Drug B |
|----------|---------|---------|---------|
|1|64|81|79|
|2|77|82|76|
|3|63|77|78|
|4|71|80|76|

Each row is ranked separately.

The test compares the total ranks of each treatment.

---

# 📂 Example Dataset

```r
y <- c(
64,77,63,71,
81,82,77,80,
79,76,78,76
)

Group <- factor(c(
rep("Before",4),
rep("DrugA",4),
rep("DrugB",4)
))

Subject <- factor(rep(1:4,3))

df <- data.frame(
y,
Group,
Subject
)
```

---

# 💻 Step 1 – Enter the Data

```r
y <- c(
64,77,63,71,
81,82,77,80,
79,76,78,76
)

Group <- factor(c(
rep("Before",4),
rep("DrugA",4),
rep("DrugB",4)
))

Subject <- factor(rep(1:4,3))

df <- data.frame(
y,
Group,
Subject
)
```

---

# 💻 Step 2 – Explore the Data

Summary

```r
summary(df)
```

Boxplots

```r
boxplot(
y ~ Group,
data=df
)
```

Median

```r
tapply(
df$y,
df$Group,
median
)
```

---

# 💻 Step 3 – Run the Test

```r
friedman.test(
y ~ Group | Subject,
data=df
)
```

---

# 📊 Example Output

```text
Friedman rank sum test

Chi-squared = 11.83

df = 2

p-value = 0.008
```

---

# 🔍 Understanding the Output

## χ²

The Friedman test statistic.

Although it is non-parametric, it is compared with a **Chi-square distribution**.

---

## Degrees of Freedom

```text
df = Number of groups − 1
```

Example:

3 treatments

↓

```text
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
χ² = 11.83

p = 0.008
```

Since

```text
0.008 < 0.05
```

Reject the null hypothesis.

Conclusion:

At least one treatment differs significantly.

---

# 🔍 Post-Hoc Testing

Like Repeated-Measures ANOVA, the Friedman Test **does not identify which groups differ**.

Use **Pairwise Wilcoxon Signed-Rank Tests**.

```r
pairwise.wilcox.test(
df$y,
df$Group,
paired=TRUE,
p.adjust.method="bonferroni"
)
```

---

# 📝 Reporting Results

Example

> A Friedman Test showed a significant difference among treatment conditions (χ²(2) = 11.83, p = 0.008). Pairwise Wilcoxon Signed-Rank Tests with Bonferroni correction identified which treatments differed.

---

# ⚠️ Common Mistakes

❌ Using the Friedman Test for independent groups.

Use **Kruskal–Wallis** instead.

---

❌ Forgetting to specify the blocking variable (`Subject`).

Always use:

```r
Group | Subject
```

---

❌ Assuming the Friedman Test identifies which groups differ.

A post-hoc test is still required.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| Two paired (normal) | Paired t-test |
| Two paired (non-normal) | Wilcoxon Signed-Rank |
| Three or more independent (normal) | One-Way ANOVA |
| Three or more independent (non-normal) | Kruskal–Wallis |
| Three or more paired (normal) | Repeated-Measures ANOVA |
| Three or more paired (non-normal) | ✅ Friedman Test |

---

# 🌳 Decision Workflow

```text
Three or more groups
          │
          ▼
Same subjects?
          │
     ┌────┴────┐
     │         │
    Yes        No
     │         │
     ▼         ▼
Check        Check
normality    normality
     │         │
 ┌───┴───┐ ┌───┴───┐
 │       │ │       │
 ▼       ▼ ▼       ▼
Repeated Friedman One-way Kruskal-
ANOVA     Test    ANOVA   Wallis
```

---

# ⚡ Quick R Cheat Sheet

```r
# Summary
summary(df)

# Boxplot
boxplot(
y ~ Group,
data=df
)

# Median
tapply(
df$y,
df$Group,
median
)

# Friedman Test
friedman.test(
y ~ Group | Subject,
data=df
)

# Pairwise Wilcoxon Post-Hoc
pairwise.wilcox.test(
df$y,
df$Group,
paired=TRUE,
p.adjust.method="bonferroni"
)
```

---

# 📊 Parametric vs Non-Parametric Comparison

| Feature | Repeated-Measures ANOVA | Friedman Test |
|----------|-------------------------|---------------|
| Groups | ≥3 paired | ≥3 paired |
| Tests | Means | Ranked observations |
| Normality required | ✅ Yes | ❌ No |
| Uses raw values | ✅ Yes | ❌ No |
| Uses ranks | ❌ No | ✅ Yes |
| Post-hoc | Pairwise t-tests | Pairwise Wilcoxon |

---

# 🎯 Key Takeaways

- 🧪 The **Friedman Test** is the **non-parametric alternative** to the Repeated-Measures ANOVA.
- 👥 It compares **three or more related (paired) groups**.
- 📊 It uses **ranks instead of raw values**, making it suitable for non-normal data.
- 🔍 A significant result indicates that **at least one treatment differs**, but **does not identify which one**.
- 💻 Use `friedman.test()` in R.
- 📋 If significant, perform **Pairwise Wilcoxon Signed-Rank Tests** with a multiple-comparison correction (e.g., Bonferroni).
