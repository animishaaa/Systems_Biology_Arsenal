# 🔬 Post-Hoc Tests in R

> **Data Analysis for Life Science**

Post-hoc tests are performed **after a significant overall statistical test** (such as ANOVA, Kruskal–Wallis, or Friedman) to determine **which specific groups differ** while controlling the risk of **Type I errors**.

---

# 📚 Table of Contents

1. [What Are Post-Hoc Tests?](#-what-are-post-hoc-tests)
2. [Why Are Post-Hoc Tests Needed?](#-why-are-post-hoc-tests-needed)
3. [Family-Wise Error Rate](#-family-wise-error-rate)
4. [When Should You Use a Post-Hoc Test?](#-when-should-you-use-a-post-hoc-test)
5. [Tukey HSD Test](#-tukey-hsd-test)
6. [Bonferroni Correction](#-bonferroni-correction)
7. [Holm Correction](#-holm-correction)
8. [Fisher's LSD Test](#-fishers-lsd-test)
9. [Dunnett's Test](#-dunnetts-test)
10. [Dunn's Test](#-dunns-test)
11. [Pairwise Wilcoxon Test](#-pairwise-wilcoxon-test)
12. [Which Post-Hoc Test Should I Choose?](#-which-post-hoc-test-should-i-choose)
13. [Decision Workflow](#-decision-workflow)
14. [Summary Table](#-summary-table)
15. [Quick R Cheat Sheet](#-quick-r-cheat-sheet)
16. [Key Takeaways](#-key-takeaways)

---

# 📖 What Are Post-Hoc Tests?

A **post-hoc test** is performed **after a significant overall statistical test**.

The overall test tells you:

> **"A difference exists."**

The post-hoc test tells you:

> **"Which groups are different?"**

---

## Example

Suppose we compare three treatments.

```text
Control

Drug A

Drug B
```

A One-Way ANOVA gives:

```text
p = 0.003
```

This tells us:

✅ At least one group is different.

But it **does not tell us**:

- Is Drug A different from Control?
- Is Drug B different from Control?
- Is Drug A different from Drug B?

A post-hoc test answers these questions.

---

# ❓ Why Are Post-Hoc Tests Needed?

Suppose we compare four groups.

```text
Control
Drug A
Drug B
Drug C
```

Possible comparisons are:

```text
Control vs Drug A

Control vs Drug B

Control vs Drug C

Drug A vs Drug B

Drug A vs Drug C

Drug B vs Drug C
```

That's **6 comparisons**.

If each comparison uses **α = 0.05**, the overall probability of making at least one false positive increases.

Post-hoc tests correct for this problem.

---

# ⚠️ Family-Wise Error Rate

The **Family-Wise Error Rate (FWER)** is the probability of making **one or more Type I errors** when performing multiple statistical tests.

Example:

- One comparison → 5% Type I error
- Six comparisons → greater than 5% overall risk

Post-hoc tests adjust p-values so the overall error rate stays under control.

---

# 📌 When Should You Use a Post-Hoc Test?

Use a post-hoc test **only if** the overall test is significant.

Examples:

| Overall Test | Perform Post-Hoc? |
|--------------|------------------|
| One-Way ANOVA | ✅ Yes (if significant) |
| Repeated-Measures ANOVA | ✅ Yes (if significant) |
| Kruskal–Wallis Test | ✅ Yes (if significant) |
| Friedman Test | ✅ Yes (if significant) |
| Non-significant ANOVA | ❌ No |

---

# 🧪 Tukey HSD Test

## Purpose

Compare **all possible pairs of group means** after a significant One-Way ANOVA.

## Best Used For

- Three or more **independent** groups
- Parametric data
- Equal variances

## R Code

```r
fit <- aov(y ~ Group, data = df)

TukeyHSD(fit)
```

---

## Example Output

```text
                     diff   lwr    upr   p adj

DrugA-Control     -2.8   -5.1  -0.5   0.01

DrugB-Control     -5.2   -7.4  -3.0   0.001

DrugB-DrugA       -2.4   -4.6  -0.2   0.03
```

### Interpretation

- **diff** → Difference between group means
- **lwr** → Lower confidence limit
- **upr** → Upper confidence limit
- **p adj** → Adjusted p-value

If **p adj < 0.05**, the groups differ significantly.

---

# 🧮 Bonferroni Correction

Bonferroni is a simple correction for multiple comparisons.

## Formula

\[
p_{\text{adjusted}} = p \times \text{Number of Comparisons}
\]

---

## Example

Original p-value:

```text
0.02
```

Three comparisons:

```text
0.02 × 3 = 0.06
```

Adjusted p-value:

```text
0.06
```

No longer significant.

---

## R Code

```r
pairwise.t.test(
  y,
  Group,
  p.adjust.method = "bonferroni"
)
```

---

## Advantages

- Easy to understand
- Strong control of Type I error

## Disadvantages

- Very conservative
- Lower statistical power

---

# 📊 Holm Correction

Holm correction is an improved version of Bonferroni.

Instead of multiplying every p-value by the same number, Holm adjusts them **step by step**.

## Advantages

- Controls Type I error
- More powerful than Bonferroni
- Commonly recommended

---

## R Code

```r
pairwise.t.test(
  y,
  Group,
  p.adjust.method = "holm"
)
```

---

# 🧪 Fisher's LSD Test

**LSD = Least Significant Difference**

Fisher's LSD performs pairwise t-tests using the pooled variance from ANOVA.

## Best Used For

- Small number of comparisons
- Exploratory analyses

---

## Advantages

- High statistical power

## Disadvantages

- Weak control of Type I error
- Not recommended when many groups are compared

---

## R Code

```r
library(agricolae)

LSD.test(fit, "Group")
```

---

# 🎯 Dunnett's Test

Dunnett's test compares **every treatment** with **one control group**.

Example:

```text
Control

Drug A

Drug B

Drug C
```

Comparisons performed:

```text
Drug A vs Control

Drug B vs Control

Drug C vs Control
```

Comparisons **not** performed:

```text
Drug A vs Drug B

Drug A vs Drug C

Drug B vs Drug C
```

---

## Advantages

- More powerful than Tukey when only control comparisons are needed

---

## R Code

```r
library(multcomp)

summary(
  glht(
    fit,
    linfct = mcp(Group = "Dunnett")
  )
)
```

---

# 📉 Dunn's Test

Dunn's test is the **non-parametric post-hoc test** used after a significant **Kruskal–Wallis Test**.

---

## R Code

```r
library(FSA)

dunnTest(
  y ~ Group,
  data = df,
  method = "bonferroni"
)
```

---

# 🔁 Pairwise Wilcoxon Test

Used after a significant **Friedman Test** (or sometimes after Kruskal–Wallis).

It compares every pair of groups using the Wilcoxon Signed-Rank Test.

---

## R Code

```r
pairwise.wilcox.test(
  df$y,
  df$Group,
  paired = TRUE,
  p.adjust.method = "bonferroni"
)
```

---

# 🧭 Which Post-Hoc Test Should I Choose?

| Situation | Recommended Test |
|------------|------------------|
| One-Way ANOVA | Tukey HSD |
| One-Way ANOVA (control vs treatments only) | Dunnett |
| Few planned comparisons | Bonferroni |
| Better alternative to Bonferroni | Holm |
| Exploratory ANOVA | Fisher's LSD |
| Kruskal–Wallis | Dunn's Test |
| Friedman | Pairwise Wilcoxon |

---

# 🌳 Decision Workflow

```text
Significant overall test?
          │
          ▼
     Which test?
          │
 ┌────────┼─────────┐
 │        │         │
 ▼        ▼         ▼
ANOVA  Kruskal  Friedman
 │        │         │
 ▼        ▼         ▼
Need all  Dunn   Pairwise
pairs?            Wilcoxon
 │
 ├─────────────┐
 ▼             ▼
YES         Control only?
 │             │
 ▼             ▼
Tukey      Dunnett
 │
 ▼
Few planned comparisons?
 │
 ├─────────────┐
 ▼             ▼
Bonferroni   Holm
```

---

# 📋 Summary Table

| Test | Used After | Compares | Data Type |
|------|------------|-----------|-----------|
| Tukey HSD | One-Way ANOVA | All pairs | Parametric |
| Bonferroni | Many tests | Selected pairs | Parametric / Non-parametric |
| Holm | Many tests | Selected pairs | Parametric / Non-parametric |
| Fisher's LSD | One-Way ANOVA | All pairs | Parametric |
| Dunnett | One-Way ANOVA | Treatment vs Control | Parametric |
| Dunn | Kruskal–Wallis | All pairs | Non-parametric |
| Pairwise Wilcoxon | Friedman | All pairs | Non-parametric |

---

# ⚡ Quick R Cheat Sheet

```r
# Tukey HSD
TukeyHSD(fit)

# Bonferroni
pairwise.t.test(
  y,
  Group,
  p.adjust.method = "bonferroni"
)

# Holm
pairwise.t.test(
  y,
  Group,
  p.adjust.method = "holm"
)

# Fisher's LSD
library(agricolae)

LSD.test(fit, "Group")

# Dunnett
library(multcomp)

summary(
  glht(
    fit,
    linfct = mcp(Group = "Dunnett")
  )
)

# Dunn
library(FSA)

dunnTest(
  y ~ Group,
  data = df,
  method = "bonferroni"
)

# Pairwise Wilcoxon
pairwise.wilcox.test(
  df$y,
  df$Group,
  paired = TRUE,
  p.adjust.method = "bonferroni"
)
```

---

# 🎯 Key Takeaways

- 🔬 Post-hoc tests are performed **after a significant overall statistical test**.
- 📊 They identify **which specific groups differ**.
- ⚠️ They control the **Type I error rate** caused by multiple comparisons.
- 🧪 Choose the post-hoc test based on the **overall test** and the **study design**.
- 📈 Tukey HSD is the standard choice after One-Way ANOVA.
- 🎯 Dunnett's test is ideal when comparing treatments only against a control.
- 📋 Dunn's test follows a significant Kruskal–Wallis Test.
- 🔄 Pairwise Wilcoxon comparisons follow a significant Friedman Test.
