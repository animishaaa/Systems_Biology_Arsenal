# 📕  Statistics Handbook
# Chapter 4: Correlation & Regression

---

# 📖 Introduction

Sometimes we **do not want to compare groups**.

Instead, we want to know:

- 📈 Are two variables related?
- 📊 Can one variable predict another?

This is where **Correlation** and **Regression** are used.

---

# 📚 Topics Covered

| Topic | Purpose |
|--------|----------|
| Pearson Correlation | Measure linear relationship |
| Spearman Correlation | Measure monotonic relationship |
| Simple Linear Regression | Predict one variable from another |
| Multiple Linear Regression | Predict using multiple variables |
| R² | Measures model quality |
| Residuals | Model errors |
| Correlation vs Regression | Know the difference |

---

# 🌳 Decision Tree

```text
Continuous Variables?

│

├── Interested only in relationship?
│         │
│         ├── Normal
│         │      ↓
│         │ Pearson Correlation
│         │
│         └── Non-normal / Ordinal
│                ↓
│          Spearman Correlation
│
└── Want Prediction?
        │
        ├── One Predictor
        │      ↓
        │ Simple Linear Regression
        │
        └── Multiple Predictors
               ↓
        Multiple Linear Regression
```

---

# 📊 Correlation

## What is Correlation?

Correlation measures

> **The strength and direction of a relationship between two variables.**

It **does not prove causation**.

---

## Examples

✅ Height vs Weight

✅ Exercise vs Cholesterol

❌ Ice cream sales vs Drowning

(Confounded by summer.)

---

# Pearson Correlation

## Purpose

Measures the strength of a **linear relationship**.

---

## Requirements

- Continuous variables
- Approximately normal
- Linear relationship

---

## Correlation Coefficient (r)

Range

```text
-1 ←──────────────→ +1
```

| r | Interpretation |
|---|---------------|
| +1 | Perfect positive relationship |
| +0.8 | Strong positive |
| +0.5 | Moderate positive |
| 0 | No linear relationship |
| -0.5 | Moderate negative |
| -0.8 | Strong negative |
| -1 | Perfect negative |

---

## Example

Height increases

↓

Weight also increases

↓

Positive correlation

---

## Interpretation

The closer |r| is to 1,

the stronger the relationship.

---

# Spearman Correlation

## Purpose

Measures **monotonic relationships** using ranks.

---

## Use When

- Ordinal data
- Non-normal data
- Many outliers

---

## Example

Pain score

↓

Disease severity

Both ranked

↓

Spearman

---

# Pearson vs Spearman

| Pearson | Spearman |
|----------|-----------|
| Continuous | Ordinal or Continuous |
| Normal | Non-normal |
| Linear | Monotonic |
| Raw values | Ranks |

---

# 📝 Question 41

## ❓ Scenario

Researchers investigate whether height and weight are related.

Both variables are normally distributed.

### ✅ Answer

**Pearson Correlation**

### 💡 Why?

- Continuous
- Normal
- Relationship only

---

# 📝 Question 42

## ❓ Scenario

Researchers investigate whether disease severity increases with pain score.

Both variables are ordinal.

### ✅ Answer

**Spearman Correlation**

---

# 📝 Question 43

## ❓ Scenario

Researchers want to predict body weight from height.

### ✅ Answer

**Simple Linear Regression**

### 💡 Why?

Prediction.

---

# 📝 Question 44

## ❓ Scenario

Researchers want to predict cholesterol using

- Age
- BMI
- Smoking
- Exercise

### ✅ Answer

**Multiple Linear Regression**

---

# 📊 Regression

Regression answers

> "Can X predict Y?"

---

## Simple Linear Regression

Uses

One predictor

Equation

```
y = b₀ + b₁x
```

Where

- y = response
- x = predictor
- b₀ = intercept
- b₁ = slope

---

## Interpretation

Suppose

```
Weight = 0.4 × Height
```

Means

Each extra cm

↓

Weight increases by

0.4 kg

---

# Multiple Linear Regression

Uses

More than one predictor.

Example

Predict cholesterol using

- Age
- Exercise
- Smoking
- BMI

---

# Hypothesis

H₀

```
β₁ = 0
```

No relationship.

H₁

```
β₁ ≠ 0
```

Relationship exists.

---

# R² (Coefficient of Determination)

## Purpose

Measures how much variation is explained by the model.

---

## Range

```
0 → 1
```

---

## Interpretation

| R² | Meaning |
|----|---------|
|0|Model explains nothing|
|0.25|25% explained|
|0.50|50% explained|
|0.90|Excellent model|
|1.00|Perfect fit|

---

Example

```
R² = 0.80
```

↓

80% of variation explained.

---

# Residuals

Residual

=

Observed

−

Predicted

---

Example

Observed weight

70 kg

Predicted

68 kg

Residual

2 kg

---

Good regression

↓

Small residuals

---

# Correlation vs Regression

| Correlation | Regression |
|-------------|------------|
| Relationship | Prediction |
| No dependent variable | Dependent & independent variables |
| r | Regression equation |
| No prediction | Prediction |

---

# 🧠 Memory Tricks

## Pearson

```
Normal

↓

Relationship

↓

Pearson
```

---

## Spearman

```
Ordinal

↓

Relationship

↓

Spearman
```

---

## Regression

```
Want Prediction?

↓

Regression
```

---

# ⭐ Favourite Traps

## Trap 1

Question says

"Relationship"

↓

Correlation

NOT Regression

---

## Trap 2

Question says

"Predict"

↓

Regression

NOT Correlation

---

## Trap 3

Ordinal variables

↓

Spearman

NOT Pearson

---

## Trap 4

Continuous

Normal

↓

Pearson

NOT Spearman

---

## Trap 5

More than one predictor

↓

Multiple Regression

---

# 📋 Summary Table

| Situation | Test |
|-----------|------|
| Normal continuous relationship | Pearson |
| Non-normal / Ordinal relationship | Spearman |
| Predict with one variable | Simple Regression |
| Predict with many variables | Multiple Regression |

---

# 🎯 Ultimate Memory Flow

```text
Want Relationship?

↓

Normal?

↓

YES → Pearson

↓

NO

↓

Spearman

──────────────────

Want Prediction?

↓

One Predictor?

↓

Simple Regression

↓

Multiple Predictors?

↓

Multiple Regression
```

---

# ⭐ Checklist

Before choosing Correlation or Regression ask:

1. 📊 Relationship or Prediction?
2. 📈 Continuous or Ordinal?
3. 🔔 Normal or Non-normal?
4. 👥 One predictor or many?

---

# 🎯 Golden Rule

> **Correlation measures relationships.**

> **Regression predicts outcomes.**

Never confuse them.
