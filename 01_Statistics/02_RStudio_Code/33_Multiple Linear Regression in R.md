# 📈 Multiple Linear Regression in R

> **Data Analysis for Life Science**

Multiple Linear Regression is used to **predict one continuous response variable (Y)** using **two or more predictor variables (X₁, X₂, X₃, ...)**.

Unlike **Simple Linear Regression**, which uses only one predictor, Multiple Linear Regression allows us to study the effect of **multiple variables simultaneously**.

> **Example:** Predict cholesterol using **BMI, Age, and Smoking Status**.

---

# 📚 Table of Contents

1. Purpose
2. Why Use Multiple Regression?
3. Simple vs Multiple Regression
4. When to Use
5. Data Requirements
6. Assumptions
7. Regression Equation
8. Understanding the Coefficients
9. Example Dataset
10. Step 1 – Import/Create the Data
11. Step 2 – Fit the Model
12. Step 3 – View the Model Summary
13. Step 4 – Confidence Intervals
14. Step 5 – Make Predictions
15. Understanding the Output
16. R² vs Adjusted R²
17. Interpreting Categorical Variables
18. Model Simplification
19. Reporting Results
20. Common Mistakes
21. Related Tests
22. Decision Workflow
23. Quick R Cheat Sheet
24. Key Takeaways

---

# 🎯 Purpose

Multiple Linear Regression predicts **one continuous outcome** using **multiple predictor variables**.

It answers questions like:

- Which predictors significantly affect the response?
- How much does each predictor contribute?
- Can multiple variables together improve prediction?

---

# 🤔 Why Use Multiple Regression?

Most biological outcomes depend on **more than one factor**.

Examples:

- Cholesterol depends on:
  - BMI
  - Smoking
  - Age

- Blood pressure depends on:
  - Age
  - Weight
  - Exercise

- Crop yield depends on:
  - Rainfall
  - Fertilizer
  - Temperature

Using only one predictor ignores the effects of the others.

---

# 📊 Simple vs Multiple Regression

| Simple Linear Regression | Multiple Linear Regression |
|---------------------------|----------------------------|
| One predictor | Two or more predictors |
| One slope | Multiple slopes |
| One independent variable | Multiple independent variables |
| Example: Weight → Cholesterol | BMI + Smoking + Age → Cholesterol |

---

# 📌 When to Use

Use Multiple Linear Regression when:

- ✅ One continuous response variable
- ✅ Two or more predictors
- ✅ Linear relationships
- ✅ Independent observations

---

## Examples

| Response (Y) | Predictors (X) |
|--------------|----------------|
| Cholesterol | BMI + Smoking |
| Blood Pressure | Age + Weight |
| Tumor Size | Drug + Time |
| Crop Yield | Rainfall + Fertilizer |

---

# 📊 Data Requirements

| Requirement | Description |
|-------------|-------------|
| Response | Continuous |
| Predictors | Continuous and/or Categorical |
| Relationship | Linear |
| Observations | Independent |

---

# 📋 Assumptions

Multiple Linear Regression assumes:

- Independent observations
- Linear relationship
- Homoscedasticity
- Normally distributed residuals
- No influential outliers
- No severe multicollinearity

---

# 📐 Regression Equation

Population model

\[
Y=\beta_0+\beta_1X_1+\beta_2X_2+\cdots+\beta_kX_k+\varepsilon
\]

Sample model

\[
\hat{Y}=b_0+b_1X_1+b_2X_2+\cdots+b_kX_k
\]

---

# 🧠 Understanding the Coefficients

Suppose

```text
Cholesterol =
1.157
+
0.076 × BMI
+
0.759 × Smoker
```

Interpretation

Intercept

```text
1.157
```

Predicted cholesterol when BMI = 0 and the subject belongs to the reference smoking category.

---

BMI coefficient

```text
0.076
```

Each additional BMI unit increases cholesterol by

```text
0.076 mmol/L
```

while keeping smoking status constant.

---

Smoking coefficient

```text
0.759
```

Smokers have cholesterol

```text
0.759 mmol/L
```

higher than non-smokers,

assuming the same BMI.

---

# 📂 Example Dataset

```r
df <- data.frame(

Cholesterol=c(
5.1,5.4,4.8,6.0,5.7,
6.2,4.9,5.5,5.8,6.1
),

BMI=c(
22,24,21,28,26,
30,23,25,27,29
),

Smoker=factor(c(
"No","No","No","Yes","Yes",
"Yes","No","No","Yes","Yes"
))
)
```

---

# 💻 Step 1 – Fit the Model

```r
fit <- lm(
Cholesterol ~ BMI + Smoker,
data=df
)
```

---

# 💻 Step 2 – View the Summary

```r
summary(fit)
```

---

# 📊 Example Output

```text
Coefficients

Intercept

1.157

BMI

0.076

SmokerYes

0.759

Multiple R-squared

0.84

Adjusted R-squared

0.81

F-statistic

18.4

p-value

<0.001
```

---

# 💻 Step 3 – Confidence Intervals

```r
confint(fit)
```

---

# 💻 Step 4 – Make Predictions

Suppose

BMI = 25

Smoker = Yes

```r
new_data <- data.frame(

BMI=25,

Smoker="Yes"
)

predict(
fit,
newdata=new_data
)
```

---

# 🔍 Understanding the Output

## Intercept

Starting value of Y when every predictor equals zero.

Often not biologically meaningful.

---

## Regression Coefficients

Each coefficient represents the effect of **one predictor while keeping all other predictors constant**.

This is the biggest advantage over simple regression.

---

## p-values

Each predictor has its own hypothesis.

Example

\[
H_0:\beta_{BMI}=0
\]

If

```text
p < 0.05
```

↓

BMI is a significant predictor.

---

# 📊 Multiple R²

Measures

```text
Variation explained by ALL predictors.
```

Example

```text
R² = 0.84
```

↓

84% of the variation is explained.

---

# 📊 Adjusted R²

Adjusted R² corrects for the number of predictors.

Unlike R²,

it penalizes unnecessary variables.

Always report:

```text
Adjusted R²
```

when comparing models.

---

# 📈 Overall F-test

The F-test evaluates the overall model.

Null hypothesis

All regression coefficients are zero.

If

```text
p < 0.05
```

↓

At least one predictor contributes significantly.

---

# 🏷️ Categorical Predictors

Regression can include factors.

Example

```r
df$Smoker <- factor(df$Smoker)
```

R automatically creates dummy variables.

Example

```text
SmokerYes
```

compares smokers against the reference category

```text
No
```

---

# 🧹 Model Simplification

Suppose

```text
BMI

p < 0.001

Smoking

p = 0.62
```

Smoking is not significant.

Simplify the model.

```r
fit2 <- lm(
Cholesterol ~ BMI,
data=df
)
```

Prefer simpler models when they perform equally well.

---

# 📝 Reporting Results

Example

> Multiple linear regression showed that BMI significantly predicted cholesterol (β = 0.076, p < 0.001), whereas smoking status was not a significant predictor (p = 0.62). The overall model explained 84% of the variance (Adjusted R² = 0.81).

---

# ⚠️ Common Mistakes

❌ Including too many predictors.

More variables do not always improve the model.

---

❌ Ignoring multicollinearity.

Highly correlated predictors can produce unstable coefficients.

---

❌ Interpreting the intercept biologically when X = 0 is impossible.

---

❌ Forgetting to convert categorical variables to factors.

Always use

```r
factor()
```

---

# 🔗 Related Tests

| Situation | Test |
|------------|------|
| One predictor | Simple Linear Regression |
| Multiple predictors | ✅ Multiple Linear Regression |
| Association only | Pearson Correlation |
| Non-normal association | Spearman Correlation |

---

# 🌳 Decision Workflow

```text
Predict Y?
      │
      ▼
How many predictors?
      │
 ┌────┴────┐
 │         │
 ▼         ▼
 One      Two or More
 │         │
 ▼         ▼
Simple   Multiple
Linear    Linear
Regression Regression
```

---

# ⚡ Quick R Cheat Sheet

```r
# Fit model
fit <- lm(
Cholesterol ~ BMI + Smoker,
data=df
)

# Summary
summary(fit)

# Confidence intervals
confint(fit)

# Predictions
predict(
fit,
newdata=data.frame(
BMI=25,
Smoker="Yes"
)
)
```

---

# 📊 Simple vs Multiple Regression

| Feature | Simple | Multiple |
|----------|---------|-----------|
| Predictors | 1 | 2 or more |
| Equation | Y = b₀ + b₁X | Y = b₀ + b₁X₁ + b₂X₂ + ... |
| R² | Yes | Yes |
| Adjusted R² | No | ✅ Yes |
| Controls for other variables | ❌ | ✅ |

---

# 🎯 Key Takeaways

- 📈 Multiple Linear Regression predicts one continuous response using **multiple predictors**.
- 📊 Each coefficient represents the effect of one predictor **while holding the others constant**.
- 📋 Always examine the **overall F-test**, **individual p-values**, **R²**, and **Adjusted R²**.
- 🏷️ Categorical predictors should be converted to **factors** before fitting the model.
- 💻 Use `lm()` to fit the model and `summary()` to interpret the results.
- ⚠️ Always check model assumptions, including multicollinearity and residual diagnostics.
