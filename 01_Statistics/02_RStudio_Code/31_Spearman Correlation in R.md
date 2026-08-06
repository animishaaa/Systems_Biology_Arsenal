# 📈 Spearman Correlation in R

> **Data Analysis for Life Science**

The **Spearman Rank Correlation (ρ or rs)** measures the **strength and direction of a monotonic relationship** between two variables.

It is the **non-parametric alternative to Pearson Correlation**.

Unlike Pearson correlation, Spearman correlation **does not require normally distributed data** and is **less sensitive to outliers** because it uses **ranks instead of raw values**.

> **Important:** Like Pearson correlation, **Spearman correlation measures association, not causation.**

---

# 📚 Table of Contents

1. Purpose
2. Why Use Spearman Correlation?
3. When to Use
4. Pearson vs Spearman
5. Data Requirements
6. Assumptions
7. Hypotheses
8. Understanding Monotonic Relationships
9. How Spearman Works
10. Example Dataset
11. Step 1 – Visualize the Data
12. Step 2 – Run Spearman Correlation
13. Understanding the Output
14. Interpretation
15. Reporting Results
16. Common Mistakes
17. Related Tests
18. Decision Workflow
19. Quick R Cheat Sheet
20. Key Takeaways

---

# 🎯 Purpose

Spearman correlation measures the:

- **Strength**
- **Direction**

of a **monotonic relationship** between two variables.

Instead of using the actual values, it compares the **ranks** of the observations.

---

# 🤔 Why Use Spearman Correlation?

Use Spearman correlation when:

- Data are **not normally distributed**
- Data are **ordinal**
- Outliers are present
- The relationship is **monotonic** but not necessarily linear

---

## Examples

- Pain score vs recovery
- Disease stage vs survival
- BMI vs disease severity
- Age vs cholesterol (non-normal data)

---

# 📌 When to Use

Use Spearman Correlation when:

- ✅ Variables are ordinal or continuous
- ✅ Data are not normally distributed
- ✅ Relationship is monotonic
- ✅ Outliers are present

---

# ⚖️ Pearson vs Spearman

| Pearson | Spearman |
|----------|-----------|
| Parametric | Non-parametric |
| Uses raw values | Uses ranks |
| Linear relationship | Monotonic relationship |
| Requires normality | No normality required |
| Sensitive to outliers | Robust to outliers |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Variables | Continuous or Ordinal |
| Relationship | Monotonic |
| Observations | Independent |

---

# 📋 Assumptions

Spearman correlation assumes:

- Independent observations
- Variables are ordinal or continuous
- Relationship is monotonic

Unlike Pearson:

- ❌ Normality is NOT required
- ❌ Linearity is NOT required

---

# 🧪 Hypotheses

Example:

Age vs Cholesterol

### Null Hypothesis

\[
H_0:
\]

There is **no monotonic correlation**.

\[
\rho_s = 0
\]

---

### Alternative Hypothesis

\[
H_1:
\]

A monotonic correlation exists.

\[
\rho_s \neq 0
\]

---

# 🧠 Understanding Monotonic Relationships

A monotonic relationship means:

As one variable increases,

the other variable:

- Always increases

or

- Always decreases

It **does not have to form a straight line**.

---

## Positive Monotonic

```text
•

  •

    •

      •

        •
```

---

## Negative Monotonic

```text
        •

      •

    •

  •

•
```

---

## Non-linear but Monotonic

```text
          •

       •

    •

  •

 •

•
```

Even though the curve is not straight,

Spearman correlation can still detect the relationship.

---

# 🧠 How Spearman Works

Instead of comparing:

```text
Height

160

170

180
```

Spearman converts them into:

```text
Rank

1

2

3
```

The same is done for the second variable.

Correlation is then calculated using the **ranks**, making the test resistant to outliers.

---

# 📂 Example Dataset

```r
Age <- c(
18,22,24,27,30,
35,40,45,50,60
)

Chol <- c(
3.9,4.0,4.1,4.3,4.6,
5.0,5.2,5.4,5.6,6.2
)
```

---

# 💻 Step 1 – Visualize the Data

```r
plot(
Age,
Chol,
xlab = "Age (years)",
ylab = "Cholesterol (mmol/L)",
main = "Age vs Cholesterol"
)
```

Always inspect the scatter plot first.

---

# 💻 Step 2 – Run Spearman Correlation

```r
cor.test(
Age,
Chol,
method = "spearman",
exact = FALSE
)
```

---

# 📊 Example Output

```text
Spearman's rank correlation rho

S = 10

p-value = 0.002

rho = 0.93
```

---

# 🔍 Understanding the Output

## Spearman's rho (ρ)

```text
ρ = 0.93
```

Very strong positive monotonic relationship.

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
ρ = 0.93

p = 0.002
```

Interpretation:

- Strong positive monotonic relationship.
- As age increases, cholesterol generally increases.
- The relationship is statistically significant.

---

# ⚠️ Correlation ≠ Causation

Suppose:

Exercise ↑

↓

Heart disease ↓

Does exercise alone cause lower heart disease?

Not necessarily.

Other factors may exist:

- Diet
- Smoking
- Genetics
- Age

These are **confounding variables**.

---

# 📝 Reporting Results

Example

> Spearman's rank correlation showed a strong positive association between age and cholesterol, **ρ = 0.93, p = 0.002**.

---

# ⚠️ Common Mistakes

❌ Using Spearman when Pearson assumptions are met.

Pearson generally has greater statistical power.

---

❌ Thinking Spearman measures linearity.

It measures **monotonicity**, not linearity.

---

❌ Ignoring scatter plots.

Always visualize the data first.

---

❌ Assuming correlation proves causation.

It does not.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| Continuous, linear, normal | Pearson Correlation |
| Continuous/Ordinal, monotonic | ✅ Spearman Correlation |
| Prediction | Linear Regression |

---

# 🌳 Decision Workflow

```text
Two Variables
      │
      ▼
Continuous or Ordinal?
      │
      ▼
Check Normality
      │
 ┌────┴────┐
 │         │
 ▼         ▼
Normal   Not Normal
 │         │
 ▼         ▼
Linear? Spearman
 │
 ▼
Pearson
```

---

# ⚡ Quick R Cheat Sheet

```r
# Scatter plot
plot(
Age,
Chol
)

# Spearman Correlation
cor.test(
Age,
Chol,
method = "spearman",
exact = FALSE
)

# Spearman coefficient only
cor(
Age,
Chol,
method = "spearman"
)
```

---

# 📊 Pearson vs Spearman

| Feature | Pearson | Spearman |
|----------|----------|-----------|
| Parametric | ✅ | ❌ |
| Uses raw values | ✅ | ❌ |
| Uses ranks | ❌ | ✅ |
| Normality required | ✅ | ❌ |
| Linear relationship | ✅ | ❌ |
| Monotonic relationship | ❌ | ✅ |
| Outlier resistant | ❌ | ✅ |
| Data | Continuous | Continuous or Ordinal |

---

# 🎯 Key Takeaways

- 📈 Spearman correlation is the **non-parametric alternative to Pearson correlation**.
- 🏆 It measures the **strength and direction of a monotonic relationship**.
- 📊 It uses **ranks instead of raw values**, making it robust to outliers.
- 📋 It is appropriate for **ordinal data** or **continuous data that are not normally distributed**.
- 💻 In R, use `cor.test(..., method = "spearman")`.
- ⚠️ Like Pearson correlation, **Spearman correlation does not imply causation**.
