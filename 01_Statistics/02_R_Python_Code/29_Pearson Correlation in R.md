# 📈 Pearson Correlation in R

> **Data Analysis for Life Science**

The **Pearson Correlation Coefficient (r)** measures the **strength and direction of a linear relationship** between **two continuous variables**.

It is the **most commonly used correlation test** in biology, medicine, engineering, and data science.

> **Important:** Correlation measures **association**, **not causation**.

---

# 📚 Table of Contents

1. Purpose
2. Why Use Pearson Correlation?
3. When to Use
4. Correlation vs Regression
5. Data Requirements
6. Assumptions
7. Hypotheses
8. Understanding Correlation
9. Interpreting r
10. Example Dataset
11. Step 1 – Visualize the Data
12. Step 2 – Run Pearson Correlation
13. Understanding the Output
14. Confidence Interval
15. Interpretation
16. Reporting Results
17. Common Mistakes
18. Related Tests
19. Decision Workflow
20. Quick R Cheat Sheet
21. Key Takeaways

---

# 🎯 Purpose

Pearson correlation measures:

- The **strength**
- The **direction**

of a **linear relationship** between two continuous variables.

---

# 🤔 Why Use Pearson Correlation?

Suppose we want to know:

- Does height increase with weight?
- Does exercise reduce cholesterol?
- Does age increase blood pressure?
- Does temperature affect enzyme activity?

Rather than comparing group means, we want to know whether **two variables move together**.

---

# 📌 When to Use

Use Pearson Correlation when:

- ✅ Both variables are continuous
- ✅ Relationship is linear
- ✅ Variables are approximately normally distributed
- ✅ No major outliers

---

## Examples

| Variable X | Variable Y |
|------------|------------|
| Height | Weight |
| Age | Blood Pressure |
| Exercise Hours | Cholesterol |
| Temperature | Enzyme Activity |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Variables | Two continuous variables |
| Relationship | Linear |
| Distribution | Approximately normal |
| Observations | Independent |

---

# 📋 Assumptions

Pearson correlation assumes:

- Independent observations
- Continuous variables
- Linear relationship
- Approximately normal distribution
- No influential outliers

If these assumptions are violated:

➡️ Use **Spearman Correlation**.

---

# 🧪 Hypotheses

Example:

Height vs Weight

### Null Hypothesis

\[
H_0:
\]

There is **no linear correlation**.

\[
\rho = 0
\]

---

### Alternative Hypothesis

\[
H_1:
\]

There is a **linear correlation**.

\[
\rho \neq 0
\]

---

# 🧠 Understanding Correlation

Correlation measures **how closely two variables change together**.

If:

- X increases
- Y also increases

↓

Positive correlation

---

If:

- X increases
- Y decreases

↓

Negative correlation

---

If:

- No consistent pattern exists

↓

No correlation

---

# 📈 Interpreting r

The correlation coefficient ranges from:

```text
-1  ≤  r  ≤  +1
```

---

## Perfect Positive

```text
•

  •

    •

      •

        •

r = +1
```

---

## Strong Positive

```text
•      •

   •

      •

         •

r ≈ +0.8
```

---

## Moderate Positive

```text
•   •

      •

 •

        •

r ≈ +0.5
```

---

## No Correlation

```text
•      •

     •

•

        •

r ≈ 0
```

---

## Strong Negative

```text
        •

     •

   •

 •

r ≈ -0.8
```

---

## Perfect Negative

```text
        •

      •

    •

  •

•

r = -1
```

---

# 📖 General Interpretation

| r | Interpretation |
|---|---------------|
| +1 | Perfect positive |
| +0.8 | Strong positive |
| +0.5 | Moderate positive |
| 0 | No linear correlation |
| -0.5 | Moderate negative |
| -0.8 | Strong negative |
| -1 | Perfect negative |

---

# 📂 Example Dataset

Suppose we measure:

- Weight (kg)
- Cholesterol (mmol/L)

```r
Weight <- c(
55,60,63,65,68,
70,73,75,78,82
)

Chol <- c(
3.8,4.0,4.2,4.3,4.5,
4.8,5.0,5.2,5.4,5.7
)
```

---

# 💻 Step 1 – Visualize the Data

```r
plot(
Weight,
Chol,
xlab="Weight (kg)",
ylab="Cholesterol (mmol/L)",
main="Weight vs Cholesterol"
)
```

Always inspect the scatter plot before calculating the correlation.

---

# 💻 Step 2 – Run Pearson Correlation

```r
cor.test(
Weight,
Chol,
method="pearson"
)
```

---

# 📊 Example Output

```text
Pearson's product-moment correlation

t = 8.25

df = 8

p-value < 0.001

cor = 0.95

95% confidence interval

0.79 0.99
```

---

# 🔍 Understanding the Output

## Correlation Coefficient

```text
r = 0.95
```

Very strong positive relationship.

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

## Confidence Interval

Example

```text
95% CI

0.79 to 0.99
```

This estimates the plausible range for the true population correlation.

---

# 📈 Interpretation

Suppose

```text
r = 0.95

p < 0.001
```

Interpretation:

- Strong positive linear relationship.
- As weight increases, cholesterol tends to increase.
- The relationship is statistically significant.

---

# ⚠️ Correlation ≠ Causation

Correlation **does not prove** that one variable causes the other.

Example:

Ice cream sales ↑

↓

Drowning deaths ↑

Does ice cream cause drowning?

❌ No.

Both increase because of **summer**.

Summer is a **confounding variable**.

---

# 📝 Reporting Results

Example

> Pearson's correlation showed a strong positive association between weight and cholesterol, **r(8) = 0.95, p < 0.001**.

---

# ⚠️ Common Mistakes

❌ Using Pearson correlation for ordinal data.

Use **Spearman Correlation**.

---

❌ Ignoring scatter plots.

Always visualize the data first.

---

❌ Using Pearson for curved relationships.

Pearson measures **linear** relationships only.

---

❌ Assuming correlation implies causation.

It does not.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| Two continuous variables (linear) | ✅ Pearson Correlation |
| Two continuous variables (monotonic, non-normal) | Spearman Correlation |
| Predict one variable from another | Linear Regression |

---

# 🌳 Decision Workflow

```text
Two Variables
      │
      ▼
Continuous?
      │
      ▼
Check normality
      │
 ┌────┴────┐
 │         │
 ▼         ▼
Normal   Not Normal
 │         │
 ▼         ▼
Linear?  Spearman
 │
 ▼
Pearson
Correlation
```

---

# ⚡ Quick R Cheat Sheet

```r
# Scatter plot
plot(
Weight,
Chol
)

# Pearson correlation
cor.test(
Weight,
Chol,
method="pearson"
)

# Correlation coefficient only
cor(
Weight,
Chol
)
```

---

# 📊 Pearson vs Spearman

| Feature | Pearson | Spearman |
|----------|----------|-----------|
| Data | Continuous | Continuous or Ordinal |
| Relationship | Linear | Monotonic |
| Normality | Required | Not required |
| Outliers | Sensitive | Robust |
| Uses | Raw values | Ranks |

---

# 🎯 Key Takeaways

- 📈 Pearson correlation measures the **strength and direction of a linear relationship**.
- 📊 The correlation coefficient (**r**) ranges from **-1 to +1**.
- ✅ Positive values indicate positive relationships, while negative values indicate negative relationships.
- 📋 Pearson correlation requires **continuous, approximately normal data** and a **linear relationship**.
- 💻 In R, use `cor.test(..., method = "pearson")`.
- ⚠️ Correlation does **not** imply causation.
