# 🔬 Assumption Checks and Diagnostics in R

> **Data Analysis for Life Science**

Statistical tests rely on assumptions. Before interpreting any p-value, confidence interval, or regression coefficient, you should verify that the assumptions of the chosen test are satisfied.

Ignoring assumptions may lead to:

- ❌ Incorrect p-values
- ❌ Increased Type I or Type II errors
- ❌ Invalid conclusions

This chapter summarizes the most important assumption checks used throughout statistical analysis.

---

# 📚 Table of Contents

1. Why Check Assumptions?
2. Statistical Workflow
3. Which Assumptions Belong to Which Test?
4. Normality
5. Shapiro–Wilk Test
6. Histograms
7. Q–Q Plots
8. Equality of Variances (Levene's Test)
9. Symmetry of Paired Differences
10. Linearity
11. Monotonic Relationships
12. Homoscedasticity
13. Residual Normality
14. Influential Observations (Cook's Distance)
15. Independence of Errors (Durbin–Watson)
16. Multicollinearity (VIF)
17. Complete Decision Workflow
18. Quick R Cheat Sheet
19. Key Takeaways

---

# 🎯 Why Check Assumptions?

Every statistical test is based on mathematical assumptions.

Example:

Independent t-test assumes

- Normal data
- Independent groups
- Equal variances

If these assumptions fail,

↓

the test may produce misleading results.

---

# 🔄 Recommended Statistical Workflow

```text
Collect Data
      │
      ▼
Visualize Data
      │
      ▼
Check Assumptions
      │
      ▼
Choose Statistical Test
      │
      ▼
Run Analysis
      │
      ▼
Interpret Results
      │
      ▼
Report Findings
```

---

# 📊 Which Assumptions Belong to Which Test?

| Test | Normality | Equal Variance | Linearity | Symmetry | Homoscedasticity |
|------|-----------|----------------|-----------|-----------|------------------|
| One-sample t-test | ✅ | ❌ | ❌ | ❌ | ❌ |
| Independent t-test | ✅ | ✅ | ❌ | ❌ | ❌ |
| Paired t-test | Differences only | ❌ | ❌ | ❌ | ❌ |
| One-way ANOVA | ✅ | ✅ | ❌ | ❌ | ❌ |
| Repeated Measures ANOVA | Residuals | ❌ | ❌ | ❌ | ❌ |
| Pearson Correlation | ✅ | ❌ | ✅ | ❌ | ❌ |
| Spearman Correlation | ❌ | ❌ | Monotonic | ❌ | ❌ |
| Simple Regression | Residuals | ❌ | ✅ | ❌ | ✅ |
| Multiple Regression | Residuals | ❌ | ✅ | ❌ | ✅ |

---

# 📈 1. Normality

## Why?

Many parametric tests assume data are approximately normally distributed.

Applies to:

- One-sample t-test
- Independent t-test
- Paired t-test (differences)
- ANOVA
- Pearson correlation
- Regression residuals

---

## Visual Check

```r
hist(data)
```

A roughly bell-shaped histogram suggests approximate normality.

---

# 🧪 2. Shapiro–Wilk Test

Tests whether data follow a normal distribution.

```r
shapiro.test(data)
```

### Hypotheses

H₀:

Data are normally distributed.

H₁:

Data are not normally distributed.

---

Interpretation

```text
p > 0.05
```

↓

Normality assumption satisfied.

---

```text
p < 0.05
```

↓

Evidence against normality.

Consider:

- Transformation
- Non-parametric test

---

# 📉 3. Q–Q Plot

A Q–Q plot compares sample quantiles with theoretical normal quantiles.

```r
qqnorm(data)
qqline(data)
```

Interpretation:

- Points close to the line → approximately normal
- Large deviations → non-normal

---

# ⚖️ 4. Equality of Variances (Levene's Test)

Used before:

- Independent t-test
- One-way ANOVA

```r
library(car)

leveneTest(
Response ~ Group,
data = df
)
```

### Hypotheses

H₀:

Variances are equal.

H₁:

Variances differ.

---

Interpretation

```text
p > 0.05
```

↓

Equal variances assumed.

---

```text
p < 0.05
```

↓

Variances differ.

Use:

- Welch's t-test
- Welch's ANOVA

---

# 🔄 5. Symmetry of Paired Differences

Needed for:

- Wilcoxon Signed-Rank Test

Calculate differences.

```r
diff <- Before - After

boxplot(diff)
```

A roughly symmetric boxplot supports the assumption.

If differences are highly asymmetric,

↓

Use the **Sign Test** instead.

---

# 📈 6. Linearity

Required for:

- Pearson Correlation
- Linear Regression

Check using a scatter plot.

```r
plot(X, Y)
```

Relationship should follow a straight-line trend.

---

# 📊 7. Monotonic Relationship

Required for:

- Spearman Correlation

A monotonic relationship means Y consistently increases or decreases as X increases.

Curved relationships are acceptable as long as the direction does not reverse.

---

# 📉 8. Homoscedasticity

Required for:

- Linear Regression
- Multiple Regression

Residuals should have constant variance.

```r
plot(
fitted(fit),
residuals(fit)
)
```

Good:

```text
----------------
• • • • • • •
----------------
```

Bad:

```text
•
 •
  •
   ••
     •••
```

The second pattern indicates heteroscedasticity.

---

# 📊 9. Residual Normality

Regression assumes residuals are normally distributed.

```r
hist(
residuals(fit)
)

qqnorm(
residuals(fit)
)

qqline(
residuals(fit)
)
```

Residuals should appear approximately normal.

---

# 📍 10. Influential Observations (Cook's Distance)

Some observations have an unusually large influence on the regression model.

Calculate Cook's Distance.

```r
cook <- cooks.distance(fit)

plot(cook)
```

A common guideline:

```text
Cook's Distance > 1
```

↓

Investigate the observation.

Do not remove observations without justification.

---

# 🔄 11. Independence of Errors

Required for:

- Linear Regression
- Multiple Regression

Test using Durbin–Watson.

```r
library(car)

durbinWatsonTest(fit)
```

Interpretation

```text
≈ 2
```

↓

Independent errors.

Values close to:

```text
0
```

Positive autocorrelation.

Values close to:

```text
4
```

Negative autocorrelation.

---

# 📈 12. Multicollinearity

Multiple predictors should not be highly correlated.

Check using Variance Inflation Factor.

```r
library(car)

vif(fit)
```

Interpretation

| VIF | Interpretation |
|-----|----------------|
| < 5 | Acceptable |
| 5–10 | Moderate concern |
| > 10 | Serious multicollinearity |

High VIF values indicate unstable regression coefficients.

---

# 🌳 Complete Decision Workflow

```text
Continuous Data
      │
      ▼
Check Histogram
      │
      ▼
Shapiro–Wilk
      │
 ┌────┴────┐
 │         │
 ▼         ▼
Normal   Not Normal
 │         │
 ▼         ▼
Parametric Non-parametric
```

---

For Independent t-test / ANOVA

```text
Normal?
      │
      ▼
Levene's Test
      │
 ┌────┴────┐
 │         │
 ▼         ▼
Equal    Unequal
Variance Variance
 │         │
 ▼         ▼
Classic   Welch
```

---

For Regression

```text
Scatter Plot
      │
      ▼
Linear?
      │
      ▼
Fit Model
      │
      ▼
Residual Plot
      │
      ▼
QQ Plot
      │
      ▼
Cook's Distance
      │
      ▼
Durbin-Watson
      │
      ▼
VIF
```

---

# ⚡ Quick R Cheat Sheet

```r
# Histogram
hist(data)

# Shapiro-Wilk
shapiro.test(data)

# QQ Plot
qqnorm(data)
qqline(data)

# Levene
library(car)
leveneTest(Y ~ Group)

# Symmetry
boxplot(diff)

# Scatter plot
plot(X, Y)

# Regression
fit <- lm(Y ~ X)

# Residual plot
plot(fitted(fit), residuals(fit))

# Residual QQ Plot
qqnorm(residuals(fit))
qqline(residuals(fit))

# Cook's Distance
plot(cooks.distance(fit))

# Durbin-Watson
durbinWatsonTest(fit)

# VIF
vif(fit)
```

---

# 📋 Which Test Should I Use?

| Assumption Fails | Recommended Action |
|------------------|--------------------|
| Normality | Use non-parametric test or transform data |
| Equal variances | Welch's t-test / Welch's ANOVA |
| Symmetry | Sign Test instead of Wilcoxon |
| Linearity | Spearman correlation or nonlinear model |
| Homoscedasticity | Transform data or robust regression |
| Multicollinearity | Remove predictors or combine variables |

---

# 🎯 Key Takeaways

- 🔬 Always check assumptions before interpreting statistical tests.
- 📈 Use **Shapiro–Wilk**, histograms, and Q–Q plots to assess normality.
- ⚖️ Use **Levene's Test** to evaluate equality of variances.
- 📊 Check **scatter plots** before Pearson correlation or regression.
- 📉 Inspect **residual plots** and **Q–Q plots** after fitting regression models.
- 📍 Use **Cook's Distance** to identify influential observations.
- 🔄 Check **Durbin–Watson** for independence of errors.
- 📈 Use **VIF** to detect multicollinearity in multiple regression.
- ✅ Choosing the correct statistical test begins with checking assumptions.
