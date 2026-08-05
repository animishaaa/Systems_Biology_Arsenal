# 📊 One-Way ANOVA in R

> **Data Analysis for Life Science**

The **One-Way Analysis of Variance (ANOVA)** compares the **means of three or more independent groups** to determine whether at least one group mean is different.

---

# 📚 Table of Contents

1. Purpose
2. Why Not Multiple t-Tests?
3. When to Use
4. Data Requirements
5. Assumptions
6. Hypotheses
7. Example Dataset
8. Step 1 – Enter the Data
9. Step 2 – Explore the Data
10. Step 3 – Check Assumptions
11. Step 4 – Run One-Way ANOVA
12. Understanding the ANOVA Table
13. Understanding the F-Statistic
14. Reporting the Results
15. What If ANOVA Is Significant?
16. Common Mistakes
17. Related Tests
18. Decision Workflow
19. Quick R Cheat Sheet

---

# 🎯 Purpose

One-Way ANOVA compares the **means of three or more independent groups**.

Typical questions:

- Do three drugs have different effects?
- Do different fertilizers produce different plant heights?
- Do diets affect cholesterol differently?

---

# 🤔 Why Not Multiple t-Tests?

Suppose you have **3 groups**:

- Control
- Drug A
- Drug B

You could perform:

- Control vs Drug A
- Control vs Drug B
- Drug A vs Drug B

That's **3 t-tests**.

Each t-test has a **5% chance of a Type I error**.

As the number of comparisons increases, the overall false-positive rate also increases.

👉 ANOVA performs **one overall test**, keeping the Type I error at **5%**.

---

# 🧠 When to Use

Use One-Way ANOVA when:

- ✅ Three or more independent groups
- ✅ Continuous outcome variable
- ✅ Groups are independent
- ✅ Data are approximately normal
- ✅ Variances are similar

---

# ❌ When NOT to Use

Do **NOT** use One-Way ANOVA when:

- Only two groups → Independent t-test
- Same subjects measured repeatedly → Repeated-Measures ANOVA
- Data are not normal → Kruskal–Wallis Test

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Groups | ≥ 3 |
| Relationship | Independent |
| Outcome | Continuous |

---

# 📋 Assumptions

Before performing ANOVA:

- Continuous outcome
- Independent observations
- Approximately normal distribution
- Equal variances
- No serious outliers

---

# 🧪 Hypotheses

Suppose we compare three treatments.

### Null Hypothesis

\[
H_0:\mu_1=\mu_2=\mu_3
\]

All group means are equal.

---

### Alternative Hypothesis

\[
H_1:
\]

At least **one** group mean is different.

⚠️ Notice:

ANOVA **does not tell us which group differs.**

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

Sample sizes

```r
table(df$Group)
```

---

# 📊 Visualize the Data

## Boxplot

```r
boxplot(
y ~ Group,
data=df,
main="Tumor Size by Treatment",
xlab="Treatment",
ylab="Tumor Size"
)
```

---

## Stripchart

```r
stripchart(
y ~ Group,
data=df,
vertical=TRUE,
method="jitter",
add=TRUE,
pch=16
)
```

---

# 💻 Step 3 – Check Assumptions

## Histogram

```r
hist(df$y)
```

---

## Q-Q Plot

```r
qqnorm(df$y)

qqline(df$y)
```

---

## Shapiro–Wilk Test

Check each group separately.

```r
by(df$y,
df$Group,
shapiro.test)
```

---

## Equal Variances

```r
library(car)

leveneTest(
y ~ Group,
data=df
)
```

Interpretation

- p > 0.05 → Equal variances
- p ≤ 0.05 → Variances differ

---

# 💻 Step 4 – Run One-Way ANOVA

```r
fit <- aov(
y ~ Group,
data=df
)

summary(fit)
```

---

# 📊 Understanding the ANOVA Table

Example

```text
             Df Sum Sq Mean Sq F value Pr(>F)

Group         2   72    36.0    10.8   0.004

Residuals     9   30     3.3
```

---

## Degrees of Freedom

Between groups

```text
k − 1
```

Example

```text
3−1=2
```

Within groups

```text
N−k
```

Example

```text
12−3=9
```

---

## Sum of Squares (SS)

Measures variation.

Two sources:

- Variation **between groups**
- Variation **within groups**

---

## Mean Square (MS)

Calculated as

\[
MS=\frac{SS}{df}
\]

---

## F Statistic

\[
F=\frac{MS_{Between}}{MS_{Within}}
\]

Large F

↓

Groups differ much more than expected by random variation.

---

# 🎯 Understanding the F-Statistic

ANOVA compares two sources of variation.

```text
Total Variation

│

├── Between Groups

└── Within Groups
```

If

```text
Between Groups
```

is much larger than

```text
Within Groups
```

↓

F becomes large.

↓

Small p-value.

↓

Reject H₀.

---

# 📈 Example Interpretation

Suppose

```text
F = 10.8

p = 0.004
```

Since

```text
0.004 < 0.05
```

Reject H₀.

There is evidence that at least one treatment mean differs.

---

# 📝 Reporting the Results

Example

> A one-way ANOVA showed a significant effect of treatment on tumor size, *F*(2,9)=10.8, *p*=0.004.

---

# ❓ What If ANOVA Is Significant?

ANOVA tells us

✅ A difference exists.

It **does not tell us which groups differ**.

Example

```text
Control

Drug A

Drug B
```

Possible differences:

- Control vs Drug A
- Control vs Drug B
- Drug A vs Drug B

To identify them, perform a **post-hoc test**.

Most commonly:

- Tukey HSD
- Bonferroni
- Holm

👉 Tukey HSD will be covered in the next chapter.

---

# ⚠️ Common Mistakes

❌ Performing multiple t-tests instead of ANOVA.

---

❌ Forgetting to check equal variances.

---

❌ Assuming ANOVA tells which groups differ.

It only tells that **at least one group differs**.

---

❌ Ignoring outliers.

Extreme observations can strongly influence ANOVA.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| One sample | One-Sample t-test |
| Two independent groups | Independent t-test |
| Two paired groups | Paired t-test |
| ≥3 independent groups | ✅ One-Way ANOVA |
| ≥3 repeated measurements | Repeated-Measures ANOVA |
| ≥3 non-normal groups | Kruskal–Wallis Test |

---

# 🌳 Decision Workflow

```text
Continuous outcome
        │
        ▼
How many groups?
        │
   ┌────┴────┐
   │         │
  Two      Three or more
   │             │
   ▼             ▼
Independent?   Independent?
   │             │
YES │ NO      YES │ NO
   ▼             ▼
Independent    One-Way
t-test         ANOVA
                 │
                 ▼
          Significant?
                 │
          ┌──────┴──────┐
          │             │
         YES            NO
          │             │
          ▼             ▼
     Post-hoc tests   Stop
```

---

# ⚡ Quick R Cheat Sheet

| Task | R Code |
|------|----------|
| Mean by group | `tapply(y, Group, mean)` |
| SD by group | `tapply(y, Group, sd)` |
| Sample size | `table(Group)` |
| Boxplot | `boxplot(y ~ Group)` |
| Histogram | `hist(y)` |
| Q-Q plot | `qqnorm(y); qqline(y)` |
| Shapiro–Wilk | `by(y, Group, shapiro.test)` |
| Levene's test | `leveneTest(y ~ Group)` |
| Run ANOVA | `aov(y ~ Group)` |
| View ANOVA table | `summary(fit)` |

---

# 🎯 Key Takeaways

- 📊 One-Way ANOVA compares **three or more independent group means**.
- 🧪 It replaces multiple independent t-tests.
- 📈 The F-statistic compares **between-group variation** with **within-group variation**.
- 📉 If **p < 0.05**, reject the null hypothesis.
- ❓ ANOVA tells you **a difference exists**, but **not which groups differ**.
- 🔍 Use a **post-hoc test (e.g., Tukey HSD)** after a significant ANOVA.
- 🔄 If assumptions are not met, consider the **Kruskal–Wallis test**.
