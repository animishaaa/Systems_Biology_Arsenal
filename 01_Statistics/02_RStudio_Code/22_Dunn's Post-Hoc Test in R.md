# 🔍 Dunn's Post-Hoc Test in R

> **Data Analysis for Life Science**

Dunn's Test is the **post-hoc test used after a significant Kruskal–Wallis Test**.

Just like **Tukey HSD** follows a significant **One-Way ANOVA**, **Dunn's Test** follows a significant **Kruskal–Wallis Test**.

---

# 📚 Table of Contents

1. Purpose
2. Why Do We Need Dunn's Test?
3. When to Use
4. Relationship with Kruskal–Wallis
5. Assumptions
6. Example Dataset
7. Step 1 – Perform Kruskal–Wallis
8. Step 2 – Run Dunn's Test
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

The **Kruskal–Wallis Test** tells us:

> **"At least one group is different."**

However, it **does not tell us which groups differ**.

Dunn's Test performs **pairwise comparisons** to identify the specific groups that are significantly different.

---

# 🤔 Why Do We Need Dunn's Test?

Imagine three treatment groups:

- Control
- Drug A
- Drug B

A Kruskal–Wallis Test gives:

```text
p = 0.01
```

This means:

✅ At least one group differs.

But it does **not** tell us whether:

- Control vs Drug A ❓
- Control vs Drug B ❓
- Drug A vs Drug B ❓

Dunn's Test answers these questions.

---

# 📌 When to Use

Use Dunn's Test **only if**:

- Kruskal–Wallis Test is significant.
- You have three or more independent groups.
- Data are not normally distributed.

---

# 🔄 Relationship with Kruskal–Wallis

```text
Three or more independent groups
            │
            ▼
   Kruskal–Wallis Test
            │
     Significant?
            │
       Yes (p < 0.05)
            │
            ▼
       Dunn's Test
            │
            ▼
 Identify which groups differ
```

---

# 📋 Assumptions

Same assumptions as Kruskal–Wallis:

- Independent observations
- Independent groups
- Continuous or ordinal data
- Similar distribution shapes if comparing medians

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

# 💻 Step 1 – Perform Kruskal–Wallis

```r
kruskal.test(
y ~ Group,
data = df
)
```

Example output:

```text
Chi-squared = 7.64

p = 0.02
```

Since

```text
p < 0.05
```

continue with Dunn's Test.

---

# 💻 Step 2 – Run Dunn's Test

Install package (once):

```r
install.packages("FSA")
```

Load package:

```r
library(FSA)
```

Run Dunn's Test:

```r
dunnTest(
y ~ Group,
data = df,
method = "bonferroni"
)
```

---

# 🔒 Multiple Comparison Corrections

Since many pairwise tests are performed, the p-values should be adjusted.

Common correction methods include:

| Method | Description |
|---------|-------------|
| Bonferroni | Very conservative |
| Holm | Less conservative, commonly recommended |
| Benjamini-Hochberg (BH) | Controls false discovery rate |

Example:

```r
dunnTest(
y ~ Group,
data = df,
method = "holm"
)
```

or

```r
dunnTest(
y ~ Group,
data = df,
method = "bh"
)
```

---

# 📊 Example Output

```text
Comparison                 Adjusted p-value

Control - Neurohib              0.041

Control - Mitostop              0.008

Neurohib - Mitostop             0.260
```

---

# 🔍 Understanding the Output

Each row represents one pairwise comparison.

Example:

```text
Control vs Neurohib
```

If

```text
Adjusted p < 0.05
```

↓

Those two groups are significantly different.

---

# 📈 Interpretation

Suppose the output is:

| Comparison | Adjusted p-value |
|------------|-----------------|
| Control vs Neurohib | 0.041 |
| Control vs Mitostop | 0.008 |
| Neurohib vs Mitostop | 0.260 |

Interpretation:

- ✅ Control differs from Neurohib.
- ✅ Control differs from Mitostop.
- ❌ Neurohib and Mitostop do not differ.

---

# 📝 Reporting Results

Example

> A Kruskal–Wallis Test revealed significant differences among the treatment groups (χ²(2) = 7.64, p = 0.02). Dunn's post-hoc test with Bonferroni correction showed that the Control group differed significantly from both Neurohib and Mitostop, whereas Neurohib and Mitostop did not differ significantly.

---

# ⚠️ Common Mistakes

❌ Running Dunn's Test without first performing a Kruskal–Wallis Test.

---

❌ Ignoring multiple comparison correction.

Always report the adjusted p-values.

---

❌ Using Dunn's Test after ANOVA.

Use **Tukey HSD** after One-Way ANOVA.

---

# 🌳 Decision Workflow

```text
Three or more groups
        │
        ▼
Independent?
        │
        ▼
Normal?
   │          │
  Yes         No
   │          │
One-Way   Kruskal–
 ANOVA     Wallis
   │          │
   ▼          ▼
Tukey      Dunn's
 HSD        Test
```

---

# ⚡ Quick R Cheat Sheet

```r
# Kruskal-Wallis Test
kruskal.test(
y ~ Group,
data = df
)

# Install package
install.packages("FSA")

# Load package
library(FSA)

# Dunn's Test
dunnTest(
y ~ Group,
data = df,
method = "bonferroni"
)

# Holm correction
dunnTest(
y ~ Group,
data = df,
method = "holm"
)

# Benjamini-Hochberg correction
dunnTest(
y ~ Group,
data = df,
method = "bh"
)
```

---

# 📊 Tukey HSD vs Dunn's Test

| Feature | Tukey HSD | Dunn's Test |
|----------|-----------|-------------|
| Used after | One-Way ANOVA | Kruskal–Wallis |
| Data | Normally distributed | Non-normal |
| Groups | ≥3 independent | ≥3 independent |
| Uses | Means | Ranked observations |
| Multiple comparison correction | Built-in | Bonferroni, Holm, BH, etc. |

---

# 🎯 Key Takeaways

- 🔍 Dunn's Test is the **post-hoc test for the Kruskal–Wallis Test**.
- 📊 It identifies **which specific groups differ** after a significant Kruskal–Wallis result.
- ⚠️ Always use **adjusted p-values** (Bonferroni, Holm, or BH).
- 💻 In R, use `dunnTest()` from the **FSA** package.
- 🚫 Do **not** use Dunn's Test after One-Way ANOVA; use **Tukey HSD** instead.
