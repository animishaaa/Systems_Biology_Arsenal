# 🔄 Repeated-Measures ANOVA in R

> **Data Analysis for Life Science**

The **Repeated-Measures ANOVA** compares the **means of three or more related measurements** taken from the **same subjects**.

It is the **parametric alternative** for repeated measurements and can be thought of as an extension of the **Paired t-test**.

---

# 📚 Table of Contents

1. Purpose
2. Why Not Multiple Paired t-Tests?
3. When to Use
4. Data Requirements
5. Assumptions
6. Hypotheses
7. Example Dataset
8. Step 1 – Enter the Data
9. Step 2 – Explore the Data
10. Step 3 – Check Assumptions
11. Step 4 – Run Repeated-Measures ANOVA
12. Understanding the Output
13. Pairwise Comparisons
14. Reporting Results
15. Common Mistakes
16. Related Tests
17. Decision Workflow
18. Quick R Cheat Sheet

---

# 🎯 Purpose

Repeated-Measures ANOVA compares **three or more measurements from the same subjects**.

Each participant acts as **their own control**, reducing variability caused by differences between individuals.

Typical questions:

- Does blood pressure change after three treatments?
- Does exercise performance improve over time?
- Does a drug produce different effects at different time points?

---

# 🤔 Why Not Multiple Paired t-Tests?

Suppose four patients are measured:

```text
Before
Drug A
Drug B
```

You could compare:

- Before vs Drug A
- Before vs Drug B
- Drug A vs Drug B

This would require **three paired t-tests**, increasing the risk of **Type I errors**.

Repeated-Measures ANOVA performs **one overall test**, keeping the overall significance level at **5%**.

---

# 🧠 When to Use

Use Repeated-Measures ANOVA when:

- ✅ Three or more related measurements
- ✅ Same subjects measured repeatedly
- ✅ Continuous outcome variable
- ✅ Data are approximately normal

Examples:

| Subject | Before | Drug A | Drug B |
|---------|---------|---------|---------|
| 1 | ✓ | ✓ | ✓ |
| 2 | ✓ | ✓ | ✓ |
| 3 | ✓ | ✓ | ✓ |

---

# ❌ When NOT to Use

Do **not** use Repeated-Measures ANOVA when:

- Groups are independent → One-Way ANOVA
- Only two repeated measurements → Paired t-test
- Repeated measurements are not normally distributed → Friedman Test

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Groups | ≥ 3 |
| Relationship | Same subjects |
| Outcome | Continuous |

---

# 📋 Assumptions

Before performing Repeated-Measures ANOVA:

- Continuous outcome
- Same subjects measured repeatedly
- Approximately normal data
- Independent subjects
- Sphericity (important for larger studies)

For small introductory examples, normality is the main assumption checked.

---

# 🧪 Hypotheses

Suppose blood pressure is measured:

- Before treatment
- After Drug A
- After Drug B

### Null Hypothesis

\[
H_0:\mu_{Before}=\mu_{DrugA}=\mu_{DrugB}
\]

All means are equal.

---

### Alternative Hypothesis

\[
H_1:
\]

At least one measurement differs.

---

# 📂 Example Dataset

```r
y <- c(
64,77,63,71,
81,82,77,80,
79,76,78,76
)

Group <- factor(c(
"Before","Before","Before","Before",
"DrugA","DrugA","DrugA","DrugA",
"DrugB","DrugB","DrugB","DrugB"
))

Subject <- factor(rep(1:4,3))

df <- data.frame(y, Group, Subject)
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
"Before","Before","Before","Before",
"DrugA","DrugA","DrugA","DrugA",
"DrugB","DrugB","DrugB","DrugB"
))

Subject <- factor(rep(1:4,3))

df <- data.frame(y, Group, Subject)
```

---

# 💻 Step 2 – Explore the Data

Summary

```r
summary(df)
```

Means

```r
tapply(df$y, df$Group, mean)
```

Standard deviations

```r
tapply(df$y, df$Group, sd)
```

---

## Boxplot

```r
boxplot(
y ~ Group,
data=df,
main="Measurements by Treatment",
xlab="Treatment",
ylab="Response"
)
```

---

# 💻 Step 3 – Check Assumptions

Histogram

```r
hist(df$y)
```

---

Q-Q Plot

```r
qqnorm(df$y)

qqline(df$y)
```

---

Shapiro–Wilk Test

```r
by(df$y,
df$Group,
shapiro.test)
```

Interpretation:

- p > 0.05 → Approximately normal
- p ≤ 0.05 → Consider Friedman Test

---

# 💻 Step 4 – Run Repeated-Measures ANOVA

```r
fit <- aov(
y ~ Group +
Error(Subject/Group),
data=df
)

summary(fit)
```

---

# 📊 Example Output

```text
Error: Subject

Error: Subject:Group

Df  Sum Sq Mean Sq F value Pr(>F)

Group
2
132
66
8.30
0.02
```

---

# 📈 Understanding the Output

Suppose

```text
F = 8.30

p = 0.02
```

Since

```text
0.02 < 0.05
```

Reject H₀.

The treatments produced significantly different responses.

---

# 👤 Why Is Repeated-Measures ANOVA More Powerful?

Repeated-Measures ANOVA removes variation caused by differences between people.

Imagine:

```text
Patient A naturally has high blood pressure.

Patient B naturally has low blood pressure.
```

Since each patient is compared **with themselves**, this natural variation is removed from the error term.

Result:

- Smaller error
- Larger F-value
- Greater statistical power

---

# 🔍 Pairwise Comparisons

After a significant Repeated-Measures ANOVA, determine which treatments differ.

```r
pairwise.t.test(
df$y,
df$Group,
paired=TRUE
)
```

---

## Bonferroni Correction

```r
pairwise.t.test(
df$y,
df$Group,
paired=TRUE,
p.adjust.method="bonferroni"
)
```

Bonferroni reduces the chance of false positives when making multiple comparisons.

---

# 📝 Reporting Results

Example

> A repeated-measures ANOVA showed a significant effect of treatment on blood pressure, *F*(2,6)=8.30, *p*=0.02.

If pairwise comparisons were performed:

> Bonferroni-adjusted pairwise comparisons showed that Drug A significantly reduced blood pressure compared with the baseline measurement.

---

# ⚠️ Common Mistakes

❌ Using One-Way ANOVA for repeated measurements.

---

❌ Forgetting the `Subject` term.

Without

```r
Error(Subject/Group)
```

R performs the wrong analysis.

---

❌ Performing several paired t-tests instead of ANOVA.

---

❌ Ignoring multiple-comparison correction.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| Two repeated measurements | Paired t-test |
| ≥3 repeated measurements | ✅ Repeated-Measures ANOVA |
| ≥3 repeated non-normal measurements | Friedman Test |
| ≥3 independent groups | One-Way ANOVA |

---

# 🌳 Decision Workflow

```text
Continuous outcome
        │
        ▼
Three or more groups?
        │
        ▼
Same subjects measured?
      │        │
     YES       NO
      │        │
      ▼        ▼
Check normality  One-Way ANOVA
      │
      ▼
Normal?
   │      │
  YES     NO
   │      │
   ▼      ▼
Repeated-   Friedman
Measures    Test
ANOVA
```

---

# ⚡ Quick R Cheat Sheet

| Task | R Code |
|------|--------|
| Mean by group | `tapply(y, Group, mean)` |
| SD by group | `tapply(y, Group, sd)` |
| Boxplot | `boxplot(y ~ Group)` |
| Histogram | `hist(y)` |
| Shapiro–Wilk | `by(y, Group, shapiro.test)` |
| Run Repeated ANOVA | `aov(y ~ Group + Error(Subject/Group))` |
| Pairwise comparisons | `pairwise.t.test(..., paired=TRUE)` |
| Bonferroni correction | `p.adjust.method="bonferroni"` |

---

# 🎯 Key Takeaways

- 🔄 Repeated-Measures ANOVA compares **three or more related measurements**.
- 👤 The **same subjects** are measured multiple times.
- 📊 It is the extension of the **Paired t-test**.
- 📈 It removes variability between subjects, increasing statistical power.
- 🔍 If the ANOVA is significant, perform **pairwise comparisons** with a correction such as **Bonferroni**.
- 📉 If assumptions are not met, use the **Friedman Test**.
