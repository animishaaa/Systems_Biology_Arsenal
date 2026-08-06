# 🔍 Pairwise Wilcoxon Post-Hoc Test in R

> **Data Analysis for Life Science**

The **Pairwise Wilcoxon Signed-Rank Test** is the **post-hoc test used after a significant Friedman Test**.

Just like:

- **Tukey HSD** follows **One-Way ANOVA**
- **Dunn's Test** follows **Kruskal–Wallis**

the **Pairwise Wilcoxon Signed-Rank Test** follows a **Friedman Test**.

---

# 📚 Table of Contents

1. Purpose
2. Why Do We Need Pairwise Wilcoxon Tests?
3. When to Use
4. Relationship with Friedman Test
5. Assumptions
6. Example Dataset
7. Step 1 – Perform Friedman Test
8. Step 2 – Run Pairwise Wilcoxon Tests
9. Multiple Comparison Corrections
10. Understanding the Output
11. Interpretation
12. Reporting Results
13. Common Mistakes
14. Decision Workflow
15. Quick R Cheat Sheet
16. Key Takeaways

---

# 🎯 Purpose

A **Friedman Test** only tells us:

> **"At least one treatment is different."**

It **does not identify which treatments differ**.

The **Pairwise Wilcoxon Signed-Rank Test** compares every pair of treatments to identify the specific differences.

---

# 🤔 Why Do We Need Pairwise Wilcoxon Tests?

Suppose you measured blood pressure:

- Before treatment
- After Drug A
- After Drug B

A Friedman Test returns:

```text
p = 0.008
```

This tells us:

✅ At least one treatment differs.

But we still don't know:

- Before vs Drug A ❓
- Before vs Drug B ❓
- Drug A vs Drug B ❓

The Pairwise Wilcoxon Test answers these questions.

---

# 📌 When to Use

Use this test when:

- ✅ Friedman Test is significant.
- ✅ Three or more paired groups.
- ✅ Same subjects measured repeatedly.
- ✅ Data are not normally distributed.

---

# 🔄 Relationship with Friedman Test

```text
Three or more paired groups
            │
            ▼
      Friedman Test
            │
     Significant?
            │
       Yes (p < 0.05)
            │
            ▼
 Pairwise Wilcoxon Tests
            │
            ▼
 Identify which treatments differ
```

---

# 📋 Assumptions

Same assumptions as the Friedman Test:

- Related observations
- Same subjects measured repeatedly
- Continuous or ordinal data

No normality assumption is required.

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

# 💻 Step 1 – Perform Friedman Test

```r
friedman.test(
y ~ Group | Subject,
data = df
)
```

Example output

```text
Chi-squared = 11.83

p = 0.008
```

Since

```text
p < 0.05
```

continue with pairwise comparisons.

---

# 💻 Step 2 – Run Pairwise Wilcoxon Tests

```r
pairwise.wilcox.test(
df$y,
df$Group,
paired = TRUE,
p.adjust.method = "bonferroni"
)
```

---

# 🔒 Multiple Comparison Corrections

Always adjust p-values because multiple comparisons increase the risk of Type I error.

Common methods:

| Method | Description |
|---------|-------------|
| Bonferroni | Very conservative |
| Holm | Less conservative (recommended) |
| Benjamini-Hochberg (BH) | Controls false discovery rate |

Example:

```r
pairwise.wilcox.test(
df$y,
df$Group,
paired = TRUE,
p.adjust.method = "holm"
)
```

or

```r
pairwise.wilcox.test(
df$y,
df$Group,
paired = TRUE,
p.adjust.method = "BH"
)
```

---

# 📊 Example Output

```text
Pairwise comparisons

                Before  DrugA

DrugA           0.031

DrugB           0.016    0.270
```

---

# 🔍 Understanding the Output

Each cell compares two treatments.

Example:

```text
Before vs DrugA
```

If

```text
Adjusted p < 0.05
```

↓

Those two treatments are significantly different.

---

# 📈 Interpretation

Suppose the output is:

| Comparison | Adjusted p-value |
|------------|-----------------|
| Before vs DrugA | 0.031 |
| Before vs DrugB | 0.016 |
| DrugA vs DrugB | 0.270 |

Interpretation:

- ✅ Before differs from Drug A.
- ✅ Before differs from Drug B.
- ❌ Drug A and Drug B do not differ significantly.

---

# 📝 Reporting Results

Example

> A Friedman Test showed a significant difference among treatment conditions (χ²(2) = 11.83, p = 0.008). Pairwise Wilcoxon Signed-Rank Tests with Bonferroni correction showed significant differences between the Before condition and both Drug A and Drug B, whereas Drug A and Drug B did not differ significantly.

---

# ⚠️ Common Mistakes

❌ Running pairwise Wilcoxon tests without first performing a Friedman Test.

---

❌ Forgetting `paired = TRUE`.

Without it, R performs the Mann–Whitney U Test instead.

---

❌ Ignoring p-value correction.

Always report adjusted p-values.

---

❌ Using Pairwise Wilcoxon after One-Way ANOVA.

Use Tukey HSD instead.

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
Repeated Friedman One-way Kruskal–
ANOVA     Test    ANOVA   Wallis
    │         │
    ▼         ▼
Pairwise    Dunn's
t-tests     Test
      │
      ▼
Pairwise Wilcoxon
```

---

# ⚡ Quick R Cheat Sheet

```r
# Friedman Test
friedman.test(
y ~ Group | Subject,
data = df
)

# Pairwise Wilcoxon
pairwise.wilcox.test(
df$y,
df$Group,
paired = TRUE,
p.adjust.method = "bonferroni"
)

# Holm correction
pairwise.wilcox.test(
df$y,
df$Group,
paired = TRUE,
p.adjust.method = "holm"
)

# Benjamini-Hochberg correction
pairwise.wilcox.test(
df$y,
df$Group,
paired = TRUE,
p.adjust.method = "BH"
)
```

---

# 📊 Post-Hoc Test Comparison

| Main Test | Post-Hoc Test |
|------------|---------------|
| One-Way ANOVA | Tukey HSD |
| Repeated-Measures ANOVA | Pairwise t-tests |
| Kruskal–Wallis | Dunn's Test |
| Friedman Test | Pairwise Wilcoxon Signed-Rank |

---

# 🎯 Key Takeaways

- 🔍 Pairwise Wilcoxon Signed-Rank Tests are the **post-hoc tests for the Friedman Test**.
- 👥 They compare **every pair of related groups** after a significant Friedman Test.
- ⚠️ Always use **`paired = TRUE`**.
- 🔒 Always apply a **multiple-comparison correction** (Bonferroni, Holm, or BH).
- 💻 Use `pairwise.wilcox.test()` in R.
- 🚫 Do not use this test after ANOVA or Kruskal–Wallis.
