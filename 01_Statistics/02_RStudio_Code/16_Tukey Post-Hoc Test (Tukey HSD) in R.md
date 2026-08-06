# 🔬 Tukey Post-Hoc Test (Tukey HSD) in R

> **Data Analysis for Life Science**

The **Tukey Honestly Significant Difference (HSD)** test is a **post-hoc test** performed **after a significant One-Way ANOVA** to identify **which specific group means are different**.

---

# 📚 Table of Contents

1. What is a Post-Hoc Test?
2. Why Do We Need Tukey's Test?
3. When to Use
4. Assumptions
5. Example Dataset
6. Step 1 – Run One-Way ANOVA
7. Step 2 – Run Tukey HSD
8. Understanding the Output
9. Interpreting Confidence Intervals
10. Reporting Results
11. Visualizing Tukey Results
12. Common Mistakes
13. Related Tests
14. Decision Workflow
15. Quick R Cheat Sheet

---

# 🎯 What is a Post-Hoc Test?

A **post-hoc test** is performed **after ANOVA** when the ANOVA result is significant.

ANOVA answers:

> **"Is there at least one difference?"**

A post-hoc test answers:

> **"Which groups are different?"**

---

# 🤔 Why Do We Need Tukey's Test?

Suppose we compare three treatments:

```text
Control
Drug A
Drug B
```

ANOVA tells us:

✅ At least one group differs.

But it does **not** tell us whether the difference is:

```text
Control vs Drug A

Control vs Drug B

Drug A vs Drug B
```

Tukey HSD performs **all pairwise comparisons** while controlling the **overall Type I error rate**.

---

# 🧠 When to Use

Use Tukey HSD when:

- ✅ One-Way ANOVA is significant
- ✅ Three or more independent groups
- ✅ You want to compare every pair of groups
- ✅ ANOVA assumptions are satisfied

---

# ❌ When NOT to Use

Do **not** use Tukey HSD:

- Before ANOVA
- If ANOVA is not significant
- For repeated-measures ANOVA
- For non-parametric data

Instead use:

- Pairwise t-tests (paired)
- Dunn's Test
- Pairwise Wilcoxon tests

---

# 📋 Assumptions

Tukey HSD has the same assumptions as One-Way ANOVA:

- Independent observations
- Continuous outcome
- Approximately normal data
- Equal variances

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

# 💻 Step 1 – Run One-Way ANOVA

```r
fit <- aov(
y ~ Group,
data=df
)

summary(fit)
```

Suppose the output is:

```text
F = 10.8

p = 0.004
```

Since

```text
0.004 < 0.05
```

Proceed with Tukey HSD.

---

# 💻 Step 2 – Run Tukey HSD

```r
TukeyHSD(fit)
```

---

# 📊 Example Output

```text
                      diff      lwr      upr     p adj

Neurohib-Control   -3.0   -5.90   -0.10    0.041

Mitostop-Control   -6.0   -8.90   -3.10    0.002

Mitostop-Neurohib  -3.0   -5.90   -0.10    0.038
```

---

# 🔍 Understanding the Output

Each row compares **two groups**.

Example:

```text
Neurohib - Control
```

Means:

Neurohib mean − Control mean

---

## diff

```text
-3.0
```

The average difference between the two groups.

Negative value

↓

Neurohib has a lower mean than Control.

---

## lwr

Lower confidence interval.

---

## upr

Upper confidence interval.

---

## p adj

Adjusted p-value.

This is the p-value after correcting for multiple comparisons.

Interpretation:

- p adj < 0.05 → Significant difference
- p adj ≥ 0.05 → No significant difference

---

# 📈 Confidence Interval Interpretation

Suppose:

```text
-5.9 to -0.1
```

Zero is **not** inside the interval.

↓

Significant difference.

---

Suppose:

```text
-2.5 to 1.8
```

Zero lies inside the interval.

↓

No significant difference.

---

# 📊 Plot the Results

```r
plot(TukeyHSD(fit))
```

R produces confidence interval plots for each comparison.

Interpretation:

If the horizontal line crosses **0**

↓

No significant difference.

If the line does **not** cross 0

↓

Significant difference.

---

# 📝 Reporting Results

Example

> One-way ANOVA showed a significant treatment effect, *F*(2,9)=10.8, *p*=0.004. Tukey's HSD test revealed that Mitostop produced significantly smaller tumor sizes than both the Control and Neurohib groups.

---

Another example

> Tukey's post-hoc test showed that Drug A differed significantly from the Control group (*p*=0.01), whereas Drug B did not differ significantly from either group.

---

# ⚠️ Common Mistakes

❌ Running Tukey before ANOVA.

Always perform ANOVA first.

---

❌ Ignoring ANOVA assumptions.

Tukey assumes the same assumptions as ANOVA.

---

❌ Looking only at the difference.

Always check the **adjusted p-value**.

---

❌ Forgetting multiple testing correction.

Tukey automatically adjusts for multiple comparisons.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| Independent t-test | Two groups |
| One-Way ANOVA | ≥3 independent groups |
| ✅ Tukey HSD | Pairwise comparisons after ANOVA |
| Repeated-Measures ANOVA | Same subjects |
| Dunn's Test | After Kruskal–Wallis |
| Pairwise Wilcoxon | After Friedman |

---

# 🌳 Decision Workflow

```text
Three or more groups
        │
        ▼
One-Way ANOVA
        │
        ▼
Is p < 0.05?
      │        │
     NO       YES
      │        │
      ▼        ▼
     Stop   Tukey HSD
                │
                ▼
      Which groups differ?
```

---

# ⚡ Quick R Cheat Sheet

| Task | R Code |
|------|--------|
| Run ANOVA | `fit <- aov(y ~ Group, data=df)` |
| View ANOVA | `summary(fit)` |
| Run Tukey HSD | `TukeyHSD(fit)` |
| Plot results | `plot(TukeyHSD(fit))` |

---

# 🎯 Key Takeaways

- 🔬 Tukey HSD is a **post-hoc test** performed **after a significant One-Way ANOVA**.
- 📊 It compares **every pair of group means**.
- 🛡️ It controls the **Type I error rate** when making multiple comparisons.
- 📉 Use the **adjusted p-value (`p adj`)** to determine significance.
- 📈 If the confidence interval **does not include 0**, the groups differ significantly.
- ❌ Do not perform Tukey HSD if the ANOVA is not significant.
