# 📈 Simple Linear Regression in R

> **Data Analysis for Life Science**

Simple Linear Regression is used to **model** and **predict** the relationship between **one independent variable (X)** and **one dependent variable (Y)**.

Unlike **correlation**, which only measures association, **regression predicts how Y changes as X changes**.

> **Example:** Predict cholesterol level from body weight.

---

# 📚 Table of Contents

1. Purpose
2. Why Use Linear Regression?
3. Correlation vs Regression
4. When to Use
5. Data Requirements
6. Assumptions
7. Regression Equation
8. Understanding the Regression Line
9. Interpreting the Coefficients
10. Example Dataset
11. Step 1 – Visualize the Data
12. Step 2 – Fit the Model
13. Step 3 – View the Model Summary
14. Step 4 – Add the Regression Line
15. Step 5 – Confidence Intervals
16. Step 6 – Make Predictions
17. Understanding the Output
18. Interpretation
19. Reporting Results
20. Common Mistakes
21. Related Tests
22. Decision Workflow
23. Quick R Cheat Sheet
24. Key Takeaways

---

# 🎯 Purpose

Simple Linear Regression answers two questions:

1. **Is there a relationship?**
2. **Can we predict Y from X?**

Unlike Pearson correlation,

Regression gives us an equation.

---

# 🤔 Why Use Linear Regression?

Suppose you want to know:

- Does body weight predict cholesterol?
- Does age predict blood pressure?
- Does temperature predict enzyme activity?
- Does exercise predict BMI?

Correlation only tells you whether the variables are related.

Regression tells you:

> **How much Y changes when X changes.**

---

# 📊 Correlation vs Regression

| Correlation | Regression |
|-------------|------------|
| Measures association | Predicts Y from X |
| No dependent variable | Has dependent & independent variables |
| Output = r | Output = equation |
| Symmetric | Not symmetric |

Example

Correlation asks:

> Are weight and cholesterol related?

Regression asks:

> If weight increases by 1 kg, how much does cholesterol increase?

---

# 📌 When to Use

Use Simple Linear Regression when:

- ✅ One predictor (X)
- ✅ One response (Y)
- ✅ Relationship is linear
- ✅ Continuous variables

---

## Examples

| X | Y |
|---|---|
| Weight | Cholesterol |
| Age | Blood Pressure |
| Height | Weight |
| Temperature | Enzyme Activity |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Predictor | Continuous |
| Response | Continuous |
| Relationship | Linear |
| Observations | Independent |

---

# 📋 Assumptions

Simple Linear Regression assumes:

- Independent observations
- Linear relationship
- Homoscedasticity (constant variance)
- Normally distributed residuals
- No influential outliers

These assumptions should always be checked after fitting the model.

---

# 📐 Regression Equation

The population regression equation is

\[
Y=\beta_0+\beta_1X+\varepsilon
\]

For a fitted sample model:

\[
\hat{Y}=b_0+b_1X
\]

where

| Symbol | Meaning |
|----------|---------|
| Ŷ | Predicted value |
| b₀ | Intercept |
| b₁ | Slope |
| X | Predictor |

---

# 📈 Understanding the Regression Line

```text
Y

│            •
│         •
│      •
│   •
│•
└────────────────────── X
```

The line is chosen so that it best fits the data.

It is called the **Least Squares Regression Line**.

---

# 🧠 Least Squares Method

Regression fits the line that minimizes

> **The sum of squared residuals (SSE)**

Residual

```text
Residual = Observed − Predicted
```

Small residuals

↓

Good model

Large residuals

↓

Poor model

---

# 📏 Interpreting the Coefficients

Suppose

```text
Cholesterol = 1.5 + 0.05 × Weight
```

Intercept

```text
1.5
```

Predicted cholesterol when weight = 0.

Usually not biologically meaningful.

---

Slope

```text
0.05
```

Every

```text
1 kg
```

increase in weight

↓

cholesterol increases by

```text
0.05 mmol/L
```

---

# 📂 Example Dataset

```r
Weight <- c(
55,60,63,65,68,
70,73,75,78,82
)

Chol <- c(
3.8,4.0,4.2,4.3,4.5,
4.8,5.0,5.2,5.4,5.7
)

df <- data.frame(
Weight,
Chol
)
```

---

# 💻 Step 1 – Visualize the Data

```r
plot(
df$Weight,
df$Chol,
xlab="Weight (kg)",
ylab="Cholesterol (mmol/L)",
main="Weight vs Cholesterol"
)
```

Always inspect the scatter plot first.

---

# 💻 Step 2 – Fit the Model

```r
fit <- lm(
Chol ~ Weight,
data=df
)
```

---

# 💻 Step 3 – View the Model Summary

```r
summary(fit)
```

---

# 📊 Example Output

```text
Coefficients:

Intercept

1.20

Weight

0.055

R² = 0.91

p < 0.001
```

---

# 💻 Step 4 – Add the Regression Line

```r
plot(
df$Weight,
df$Chol
)

abline(
fit,
col="red",
lwd=2
)
```

---

# 💻 Step 5 – Confidence Intervals

```r
confint(fit)
```

Example

```text
Intercept

0.82 1.58

Weight

0.045 0.066
```

---

# 💻 Step 6 – Make Predictions

Predict cholesterol for

```text
Weight = 72 kg
```

```r
new_data <- data.frame(
Weight = 72
)

predict(
fit,
newdata=new_data
)
```

Output

```text
4.86 mmol/L
```

---

# 🔍 Understanding the Output

## Intercept

Starting value of Y when X = 0.

---

## Slope

Amount Y changes for every

```text
1-unit
```

increase in X.

---

## p-value

Tests

\[
H_0:\beta_1=0
\]

If

```text
p < 0.05
```

↓

Slope is significantly different from zero.

---

## R²

Measures how much variation in Y is explained by X.

Example

```text
R² = 0.91
```

↓

91% of the variation is explained.

---

# 📈 Interpretation

Suppose

```text
Slope = 0.055

p < 0.001

R² = 0.91
```

Interpretation

- Weight significantly predicts cholesterol.
- Every kilogram increases cholesterol by

```text
0.055 mmol/L
```

- The model explains

```text
91%
```

of the variation.

---

# 📝 Reporting Results

Example

> Simple linear regression showed that body weight significantly predicted cholesterol levels (β = 0.055, t = 10.2, p < 0.001, R² = 0.91).

---

# ⚠️ Common Mistakes

❌ Confusing regression with correlation.

Regression predicts.

Correlation measures association.

---

❌ Assuming a significant model proves causation.

It does not.

---

❌ Ignoring assumptions.

Residuals should always be checked.

---

❌ Extrapolating beyond the data.

Never predict far outside the observed range.

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| Association | Pearson Correlation |
| Non-normal association | Spearman Correlation |
| Prediction (one predictor) | ✅ Simple Linear Regression |
| Prediction (multiple predictors) | Multiple Linear Regression |

---

# 🌳 Decision Workflow

```text
Relationship?
      │
      ▼
Want prediction?
      │
 ┌────┴────┐
 │         │
 ▼         ▼
 No       Yes
 │         │
 ▼         ▼
Correlation Regression
```

---

# ⚡ Quick R Cheat Sheet

```r
# Scatter plot
plot(Weight, Chol)

# Fit model
fit <- lm(
Chol ~ Weight,
data=df
)

# Model summary
summary(fit)

# Confidence intervals
confint(fit)

# Predictions
predict(
fit,
newdata=data.frame(
Weight=72
)
)

# Regression line
abline(
fit,
col="red",
lwd=2
)
```

---

# 📊 Correlation vs Regression

| Feature | Correlation | Regression |
|----------|-------------|------------|
| Goal | Association | Prediction |
| Output | r | Equation |
| Variables | Equal | X predicts Y |
| R² | Not directly reported | Reported |
| Prediction | ❌ | ✅ |

---

# 🎯 Key Takeaways

- 📈 Simple Linear Regression predicts one continuous variable from another.
- 📐 The regression equation is **Ŷ = b₀ + b₁X**.
- 📊 The **slope (b₁)** represents the expected change in Y for a one-unit increase in X.
- 📋 **R²** measures how much of the variation in Y is explained by X.
- 💻 Use `lm()` to fit the model and `summary()` to interpret the results.
- ⚠️ Always check regression assumptions before interpreting the model.
