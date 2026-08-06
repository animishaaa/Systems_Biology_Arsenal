# 🧪 Kruskal–Wallis Test in R

> **Data Analysis for Life Science**

The **Kruskal–Wallis Test** is the **non-parametric alternative** to the **One-Way ANOVA**.

It compares **three or more independent groups** when the data are **not normally distributed**.

Instead of comparing **group means**, it compares the **distribution (or medians when distributions have similar shapes)** using **ranked observations**.

---

# 📚 Table of Contents

1. Purpose
2. Why Use the Kruskal–Wallis Test?
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

The **Kruskal–Wallis Test** compares **three or more independent groups**.

It is used when the assumptions of a **One-Way ANOVA** are not met.

---

# 🤔 Why Use the Kruskal–Wallis Test?

One-Way ANOVA assumes:

- Normally distributed data
- Equal variances
- Continuous measurements

If these assumptions are violated, the Kruskal–Wallis Test is preferred.

---

# 📌 When to Use

Use this test when:

- ✅ Three or more independent groups
- ✅ Continuous or ordinal data
- ✅ Data are not normally distributed
- ✅ Groups are unrelated

---

## Examples

- Control vs Drug A vs Drug B
- Three diets
- Three fertilizers
- Three exercise programs

---

# ⚖️ Parametric vs Non-Parametric

| Parametric | Non-Parametric |
|------------|----------------|
| One-Way ANOVA | ✅ Kruskal–Wallis Test |
| Tests means | Tests distributions (or medians if distributions have similar shapes) |
| Requires normality | No normality assumption |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Groups | Three or more |
| Relationship | Independent |
| Outcome | Continuous or Ordinal |

---

# 📋 Assumptions

The Kruskal–Wallis Test assumes:

- Independent observations
- Independent groups
- Continuous or ordinal data
- Similar distribution shapes if comparing medians

Unlike ANOVA:

- ❌ Normality is **not required**

---

# 🧪 Hypotheses

Example:

Compare tumor size in three treatment groups.

### Null Hypothesis

\[
H_0:
\]

All groups come from the same distribution.

(No difference.)

---

### Alternative Hypothesis

\[
H_1:
\]

At least one group comes from a different distribution.

---

# 🧠 How the Test Works

Instead of comparing means, the Kruskal–Wallis Test:

1. Combines all observations.
2. Ranks every observation.
3. Calculates the average rank for each group.
4. Compares the rank sums between groups.
5. Calculates the **H statistic**, which approximately follows a **Chi-square (χ²) distribution**.

Large differences in rank sums suggest that at least one group differs.

---

# 📂 Example Dataset

```r
y <- c(
7,8,10,11,
4,5,7,8,
1,2,4,5
)

Group <- factor(c(
rep("Control",4),
rep("Neurohib",4),
rep("Mitostop",4)
))

df <- data.frame(y, Group)
```

---

# 💻 Step 1 – Enter the Data

```r
y <- c(
7,8,10,11,
4,5,7,8,
1,2,4,5
)

Group <- factor(c(
rep("Control",4),
rep("Neurohib",4),
rep("Mitostop",4)
))

df <- data.frame(y, Group)
```

---

# 💻 Step 2 – Explore the Data

```r
summary(df)
```

Median by group

```r
tapply(
df$y,
df$Group,
median
)
```

Boxplot

```r
boxplot(
y ~ Group,
data=df
)
```

---

# 💻 Step 3 – Run the Test

```r
kruskal.test(
y ~ Group,
data=df
)
```

---

# 📊 Example Output

```text
Kruskal-Wallis rank sum test

Chi-squared = 7.64

df = 2

p-value = 0.02
```

---

# 🔍 Understanding the Output

## χ²

The Kruskal–Wallis test statistic.

Although the test is non-parametric, the statistic is compared with a **Chi-square distribution**.

---

## Degrees of Freedom

```text
df = Number of groups − 1
```

Example:

Three groups

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
χ² = 7.64

p = 0.02
```

Since

```text
0.02 < 0.05
```

Reject the null hypothesis.

Conclusion:

At least one treatment group differs from the others.

---

# 🔍 Post-Hoc Testing

Like One-Way ANOVA, the Kruskal–Wallis Test **does not tell you which groups differ**.

After a significant result, perform **Dunn's Test**.

Example:

```r
library(FSA)

dunnTest(
y ~ Group,
data=df,
method="bonferroni"
)
```

---

# 📝 Reporting Results

Example

> A Kruskal–Wallis test showed a significant difference in tumor size among treatment groups (χ²(2) = 7.64, p = 0.02). Dunn's post-hoc test identified which groups differed.

---

# ⚠️ Common Mistakes

❌ Using it for two groups.

Use the **Mann–Whitney U Test**.

---

❌ Using it for paired data.

Use the **Friedman Test**.

---

❌ Assuming it identifies which groups differ.

A post-hoc test is still required.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| Two independent (normal) | Independent t-test |
| Two independent (non-normal) | Mann–Whitney U |
| Three or more independent (normal) | One-Way ANOVA |
| Three or more independent (non-normal) | ✅ Kruskal–Wallis |
| Three or more paired | Friedman Test |

---

# 🌳 Decision Workflow

```text
Three or more groups
        │
        ▼
Independent?
        │
        ▼
Check normality
        │
 ┌──────┴──────┐
 │             │
 ▼             ▼
Normal?      Not normal?
 │             │
 ▼             ▼
One-Way      Kruskal–
ANOVA        Wallis
                 │
                 ▼
         Significant?
                 │
                 ▼
            Dunn's Test
```

---

# ⚡ Quick R Cheat Sheet

```r
# Median
tapply(
df$y,
df$Group,
median
)

# Boxplot
boxplot(
y ~ Group,
data=df
)

# Kruskal–Wallis
kruskal.test(
y ~ Group,
data=df
)

# Dunn's Test
library(FSA)

dunnTest(
y ~ Group,
data=df,
method="bonferroni"
)
```

---

# 📊 Parametric vs Non-Parametric Comparison

| Feature | One-Way ANOVA | Kruskal–Wallis |
|----------|---------------|----------------|
| Groups | ≥3 independent | ≥3 independent |
| Tests | Means | Ranked observations (or medians if distributions have similar shapes) |
| Normality required | ✅ Yes | ❌ No |
| Uses raw values | ✅ Yes | ❌ No |
| Uses ranks | ❌ No | ✅ Yes |
| Post-hoc | Tukey HSD | Dunn's Test |

---

# 🎯 Key Takeaways

- 🧪 The **Kruskal–Wallis Test** is the **non-parametric alternative** to the One-Way ANOVA.
- 📊 It compares **three or more independent groups**.
- 📈 It uses **ranked observations**, making it robust to non-normal data and outliers.
- 🔍 A significant result tells you **that at least one group differs**, but **not which groups differ**.
- 💻 Use **`kruskal.test()`** in R.
- 📋 If significant, follow up with **Dunn's Test**.
