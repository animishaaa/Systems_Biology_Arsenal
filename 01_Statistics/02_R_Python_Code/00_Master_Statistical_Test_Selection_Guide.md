# 🎯 Master Statistical Test Selection Guide

> **Systems Biology Arsenal**
>
> **The Ultimate Decision Tree for Choosing Statistical Tests**
>
> This guide summarizes every statistical test covered in **SY768A**, including:
>
> - Parametric tests
> - Non-parametric tests
> - Categorical tests
> - Correlation
> - Regression
> - Assumption checks

---

# 📚 Table of Contents

1. Complete Statistical Decision Tree
2. Test Selection Flowchart
3. Parametric vs Non-Parametric
4. Continuous Data
5. Categorical Data
6. Correlation & Regression
7. Assumption Checklist
8. Complete Comparison Tables
9. R Function Cheat Sheet
10. Which Test Should I Use?

---

# 🌳 Complete Statistical Decision Tree

```text
START
│
├── What is your objective?
│
├── Compare Groups
│   │
│   ├── Continuous Outcome
│   │   │
│   │   ├── One Group
│   │   │      │
│   │   │      ├── Normal?
│   │   │      │      ├── Yes → One-sample t-test
│   │   │      │      └── No  → One-sample Wilcoxon
│   │   │
│   │   ├── Two Groups
│   │   │      │
│   │   │      ├── Independent?
│   │   │      │      │
│   │   │      │      ├── Yes
│   │   │      │      │     │
│   │   │      │      │     ├── Normal?
│   │   │      │      │     │      ├── Yes → Independent t-test
│   │   │      │      │     │      └── No  → Mann–Whitney U
│   │   │      │
│   │   │      └── Paired
│   │   │             │
│   │   │             ├── Normal differences?
│   │   │             │      ├── Yes → Paired t-test
│   │   │             │      └── No
│   │   │             │            │
│   │   │             │            ├── Symmetric? → Wilcoxon Signed-Rank
│   │   │             │            └── Not Symmetric → Sign Test
│   │   │
│   │   └── Three or More Groups
│   │          │
│   │          ├── Independent?
│   │          │      │
│   │          │      ├── Normal?
│   │          │      │      ├── Yes → One-way ANOVA
│   │          │      │      └── No  → Kruskal–Wallis
│   │          │
│   │          └── Repeated Measures
│   │                 │
│   │                 ├── Normal?
│   │                 │      ├── Yes → Repeated Measures ANOVA
│   │                 │      └── No  → Friedman Test
│
├── Categorical Outcome
│   │
│   ├── One Variable
│   │      └── Chi-square Goodness-of-Fit
│   │
│   ├── Two Independent Variables
│   │      │
│   │      ├── Expected counts ≥5?
│   │      │      ├── Yes → Chi-square Independence
│   │      │      └── No  → Fisher's Exact Test
│   │
│   ├── Two Paired Variables
│   │      └── McNemar's Test
│   │
│   └── Compare Two Proportions
│          └── Two-Proportion Z-Test
│
└── Relationship Between Variables
    │
    ├── Want Association?
    │      │
    │      ├── Linear + Normal
    │      │      └── Pearson Correlation
    │      │
    │      └── Monotonic / Non-normal
    │             └── Spearman Correlation
    │
    └── Want Prediction?
           │
           ├── One Predictor
           │      └── Simple Linear Regression
           │
           └── Multiple Predictors
                  └── Multiple Linear Regression
```

---

# 🚦 Statistical Test Selection Flowchart

```text
                DATA
                  │
     ┌────────────┴────────────┐
     │                         │
Continuous                 Categorical
     │                         │
     ▼                         ▼
Compare?                 Compare?
     │                         │
     ▼                         ▼
Relationship?          Frequencies?
```

---

## Continuous Data

```text
One Group
      │
      ▼
Normal?
 │         │
Yes       No
 │         │
 ▼         ▼
One-sample t-test
One-sample Wilcoxon
```

---

```text
Two Groups
      │
      ▼
Independent?
 │          │
Yes        No
 │          │
 ▼          ▼
Independent Paired
t-test      t-test
 │           │
Not Normal? Not Normal?
 │           │
 ▼           ▼
Mann-        Wilcoxon
Whitney      Signed-Rank
             │
             ▼
         Sign Test
```

---

```text
Three or More Groups
      │
      ▼
Independent?
 │            │
Yes          No
 │            │
 ▼            ▼
ANOVA    Repeated ANOVA
 │            │
 ▼            ▼
Kruskal    Friedman
Wallis
```

---

# 📊 Parametric vs Non-Parametric

| Parametric | Non-parametric |
|------------|----------------|
| One-sample t-test | One-sample Wilcoxon |
| Independent t-test | Mann–Whitney U |
| Paired t-test | Wilcoxon Signed-Rank |
| — | Sign Test |
| One-way ANOVA | Kruskal–Wallis |
| Repeated Measures ANOVA | Friedman |
| Pearson Correlation | Spearman Correlation |

---

# 📊 Continuous Data

| Situation | Parametric | Non-parametric |
|-----------|------------|----------------|
| One sample | One-sample t-test | One-sample Wilcoxon |
| Two independent | Independent t-test | Mann–Whitney U |
| Two paired | Paired t-test | Wilcoxon Signed-Rank |
| Two paired (non-symmetric) | — | Sign Test |
| ≥3 independent | One-way ANOVA | Kruskal–Wallis |
| ≥3 paired | Repeated Measures ANOVA | Friedman |

---

# 📊 Categorical Data

| Situation | Test |
|------------|------|
| One categorical variable | Chi-square Goodness-of-Fit |
| Two independent variables | Chi-square Independence |
| Small expected frequencies | Fisher's Exact Test |
| Two paired variables | McNemar's Test |
| Compare two proportions | Two-Proportion Z-Test |

---

# 📊 Correlation & Regression

| Goal | Test |
|------|------|
| Linear association | Pearson Correlation |
| Monotonic association | Spearman Correlation |
| Predict using one variable | Simple Linear Regression |
| Predict using several variables | Multiple Linear Regression |

---

# 🔍 Assumption Checklist

| Assumption | Test |
|------------|------|
| Normality | Shapiro–Wilk |
| Equal variances | Levene's Test |
| Linearity | Scatter Plot |
| Monotonicity | Scatter Plot |
| Symmetry | Boxplot of Differences |
| Residual Normality | Q–Q Plot |
| Homoscedasticity | Residual Plot |
| Multicollinearity | VIF |
| Independence of Errors | Durbin–Watson |
| Influential Observations | Cook's Distance |

---

# 🛠 R Function Cheat Sheet

| Test | Function |
|------|----------|
| One-sample t-test | `t.test(x, mu=)` |
| Independent t-test | `t.test(y ~ group)` |
| Paired t-test | `t.test(x, y, paired=TRUE)` |
| One-way ANOVA | `aov()` |
| Tukey | `TukeyHSD()` |
| One-sample Wilcoxon | `wilcox.test(mu=)` |
| Mann–Whitney | `wilcox.test(x,y)` |
| Wilcoxon Signed-Rank | `wilcox.test(..., paired=TRUE)` |
| Sign Test | `binom.test()` |
| Kruskal–Wallis | `kruskal.test()` |
| Friedman | `friedman.test()` |
| Dunn | `dunnTest()` |
| Pairwise Wilcoxon | `pairwise.wilcox.test()` |
| Chi-square | `chisq.test()` |
| McNemar | `mcnemar.test()` |
| Fisher | `fisher.test()` |
| Two-Proportion | `prop.test()` |
| Pearson | `cor.test(method="pearson")` |
| Spearman | `cor.test(method="spearman")` |
| Linear Regression | `lm()` |
| Multiple Regression | `lm()` |

---

# 🎯 Which Test Should I Use?

| If your data are... | Use... |
|----------------------|--------|
| One normal sample | One-sample t-test |
| One non-normal sample | One-sample Wilcoxon |
| Two independent normal groups | Independent t-test |
| Two independent non-normal groups | Mann–Whitney U |
| Two paired normal groups | Paired t-test |
| Two paired non-normal groups | Wilcoxon Signed-Rank |
| Two paired non-symmetric groups | Sign Test |
| ≥3 independent normal groups | One-way ANOVA |
| ≥3 independent non-normal groups | Kruskal–Wallis |
| ≥3 repeated normal measurements | Repeated Measures ANOVA |
| ≥3 repeated non-normal measurements | Friedman |
| Two categorical variables | Chi-square Independence |
| One categorical variable | Chi-square Goodness-of-Fit |
| Small 2×2 table | Fisher's Exact Test |
| Paired categorical data | McNemar's Test |
| Compare two proportions | Two-Proportion Z-Test |
| Linear relationship | Pearson Correlation |
| Monotonic relationship | Spearman Correlation |
| Predict one variable | Simple Linear Regression |
| Predict multiple variables | Multiple Linear Regression |

---

# 🏆 Complete Statistical Workflow

```text
Collect Data
      │
      ▼
Identify Variable Type
      │
      ├──────────────┐
      │              │
      ▼              ▼
Continuous     Categorical
      │              │
      ▼              ▼
Compare?       Compare?
      │              │
      ▼              ▼
Relationship? Frequencies?
      │              │
      ▼              ▼
Check Assumptions
      │
      ▼
Choose Statistical Test
      │
      ▼
Run Analysis in R
      │
      ▼
Interpret p-value
      │
      ▼
Report Results
```

---

# 🎓 Final Exam Strategy

Ask yourself these questions **in order**:

1. ❓ Is my outcome **continuous** or **categorical**?
2. ❓ Am I **comparing groups** or looking for a **relationship**?
3. ❓ How many groups do I have?
4. ❓ Are the groups **independent** or **paired**?
5. ❓ Does my data satisfy **parametric assumptions**?
6. ❓ If not, what is the **non-parametric equivalent**?
7. ❓ Do I need **post-hoc tests**?
8. ❓ Can I interpret the **effect size** and **confidence interval**?

---

# 🏆 Master Summary

```text
Means
│
├── 1 Group
│      ├── t-test
│      └── Wilcoxon
│
├── 2 Groups
│      ├── Independent → t-test / Mann–Whitney
│      └── Paired → Paired t-test / Wilcoxon / Sign
│
└── ≥3 Groups
       ├── Independent → ANOVA / Kruskal
       └── Paired → RM-ANOVA / Friedman

Categorical
│
├── One Variable → χ² Goodness-of-Fit
├── Two Variables → χ² Independence
├── Small Samples → Fisher
├── Paired → McNemar
└── Two Proportions → Z-test

Relationship
│
├── Pearson
├── Spearman
├── Linear Regression
└── Multiple Regression
```

---

# 🎯 Final Takeaways

- ✅ Start by identifying your **data type** (continuous vs categorical).
- ✅ Determine whether you are **comparing groups** or studying **relationships**.
- ✅ Check assumptions **before** choosing a parametric test.
- ✅ Switch to the appropriate **non-parametric alternative** when assumptions are violated.
- ✅ For ANOVA or Kruskal–Wallis, remember that a significant overall test is often followed by **post-hoc tests**.
- ✅ Use this guide as your first stop before any statistical analysis.
