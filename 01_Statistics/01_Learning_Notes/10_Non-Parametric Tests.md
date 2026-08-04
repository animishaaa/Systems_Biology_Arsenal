# 📙 Statistics Handbook
# Chapter 2: Non-Parametric Tests

---

# 📖 What are Non-Parametric Tests?

Non-parametric tests are statistical tests that **do not assume a normal distribution**.

They are mainly used when:

- 📉 Data are **not normally distributed**
- 📊 Data are **ordinal (ranked)**
- 📏 Sample size is very small
- ⚠️ Data contain many outliers
- 📈 Parametric assumptions are violated

Unlike parametric tests, most non-parametric tests compare **ranks** instead of the actual values.

---

# 📚 Non-Parametric Tests Covered

| Test | Parametric Alternative | Purpose |
|------|------------------------|---------|
| Mann-Whitney U Test | Independent t-test | Compare two independent groups |
| Wilcoxon Signed-Rank Test | Paired t-test | Compare two paired groups |
| Sign Test | Paired t-test | Compare paired data using only signs (+/-) |
| Kruskal-Wallis Test | One-Way ANOVA | Compare ≥3 independent groups |
| Friedman Test | Repeated Measures ANOVA | Compare ≥3 paired measurements |
| Spearman Correlation | Pearson Correlation | Correlation for ordinal/non-normal data |

---

# 🌳 Decision Tree

```text
Continuous / Ordinal Data
│
├── Two Groups?
│      │
│      ├── Independent?
│      │      └── Mann-Whitney U
│      │
│      └── Paired?
│             │
│             ├── Symmetric Differences?
│             │       └── Wilcoxon Signed-Rank
│             │
│             └── Not Symmetric?
│                     └── Sign Test
│
└── More Than Two Groups?
       │
       ├── Independent?
       │      └── Kruskal-Wallis
       │
       └── Same Subjects?
              └── Friedman Test
```

---

# 📝 Question 16

## ❓ Scenario

Pain scores (0–10) are compared between **two independent treatment groups**.

The data are highly skewed.

### ✅ Answer

**Mann-Whitney U Test**

### 💡 Why?

- Two independent groups
- Non-normal distribution
- Ordinal / skewed continuous data

### ❌ Why NOT?

**Independent t-test**

Requires approximately normal data.

### 🧠 Memory Trick

```
Independent
+
Not Normal

↓

Mann-Whitney U
```

---

# 📝 Question 17

## ❓ Scenario

Pain scores are measured **before and after treatment** in the same patients.

The differences are symmetric but not normally distributed.

### ✅ Answer

**Wilcoxon Signed-Rank Test**

### 💡 Why?

- Same patients
- Non-normal
- Differences are symmetric

### ❌ Why NOT?

**Paired t-test**

Requires normally distributed differences.

### 🧠 Memory Trick

```
Paired
+
Symmetric

↓

Wilcoxon
```

---

# 📝 Question 18

## ❓ Scenario

Blood pressure is measured before and after treatment.

The differences are **extremely asymmetric**.

### ✅ Answer

**Sign Test**

### 💡 Why?

The Sign Test only considers whether values increased or decreased.

It does **not** use the magnitude of change.

### ❌ Why NOT?

**Wilcoxon Signed-Rank**

Wilcoxon assumes approximately symmetric differences.

### 🧠 Memory Trick

```
Only +

or -

↓

Sign Test
```

---

# 📝 Question 19

## ❓ Scenario

Five hospitals compare patient satisfaction scores.

The outcome is ordinal.

Groups are independent.

### ✅ Answer

**Kruskal-Wallis Test**

### 💡 Why?

- More than two groups
- Independent
- Ordinal data

### 🧠 Memory Trick

```
3+

Independent

↓

Kruskal-Wallis
```

---

# 📝 Question 20

## ❓ Scenario

The same patients rate pain at:

- Visit 1
- Visit 2
- Visit 3
- Visit 4

The data are ordinal.

### ✅ Answer

**Friedman Test**

### 💡 Why?

- Same patients
- More than two measurements
- Ordinal / non-normal

### 🧠 Memory Trick

```
Repeated Measurements

↓

Friedman
```

---

# 📝 Question 21

## ❓ Scenario

Researchers study whether **education level** is associated with **income rank**.

Both variables are ordinal.

### ✅ Answer

**Spearman Rank Correlation**

### 💡 Why?

Spearman measures monotonic relationships using ranks.

### ❌ Why NOT?

Pearson requires normally distributed continuous variables.

### 🧠 Memory Trick

```
Ordinal

↓

Spearman
```

---

# 📝 Question 22

## ❓ Scenario

Researchers compare two independent groups.

The data contain many extreme outliers.

### ✅ Answer

**Mann-Whitney U Test**

### 💡 Why?

Ranks are much less affected by outliers.

---

# 📝 Question 23

## ❓ Scenario

Antibody concentrations are measured before and after vaccination.

Differences are not normal but are symmetric.

### ✅ Answer

**Wilcoxon Signed-Rank Test**

---

# 📝 Question 24

## ❓ Scenario

Depression scores are compared among three independent clinics.

The scores are highly skewed.

### ✅ Answer

**Kruskal-Wallis Test**

---

# 📝 Question 25

## ❓ Scenario

Anxiety scores are recorded at five follow-up visits in the same patients.

The data are non-normal.

### ✅ Answer

**Friedman Test**

---

# 📝 Question 26

## ❓ Scenario

Tumor sizes are compared between two independent groups.

Sample size = 8 per group.

The data are highly skewed.

### ✅ Answer

**Mann-Whitney U Test**

---

# 📝 Question 27

## ❓ Scenario

Researchers compare before-and-after pain scores.

Only the **direction of change (+/-)** is considered.

### ✅ Answer

**Sign Test**

### 💡 Why?

Magnitude of change is ignored.

---

# 📝 Question 28

## ❓ Scenario

Researchers investigate whether age and disease severity (ordinal ranking) increase together.

### ✅ Answer

**Spearman Rank Correlation**

---

# 📝 Question 29

## ❓ Scenario

Researchers compare two independent groups using ordinal data.

### ✅ Answer

**Mann-Whitney U Test**

---

# 📝 Question 30

## ❓ Scenario

Researchers compare two related measurements using ordinal data.

The differences are symmetric.

### ✅ Answer

**Wilcoxon Signed-Rank Test**

---

# 📊 Parametric vs Non-Parametric

| Parametric | Non-Parametric |
|------------|----------------|
| Uses raw values | Uses ranks |
| Compares means | Compares distributions/ranks |
| Assumes normal distribution | No normality assumption |
| More powerful | More robust |

---

# 📊 Comparison Table

| Situation | Parametric | Non-Parametric |
|-----------|------------|----------------|
| Two independent groups | Independent t-test | Mann-Whitney U |
| Two paired groups | Paired t-test | Wilcoxon Signed-Rank |
| Paired (not symmetric) | — | Sign Test |
| ≥3 independent groups | One-Way ANOVA | Kruskal-Wallis |
| ≥3 paired measurements | Repeated Measures ANOVA | Friedman |
| Correlation | Pearson | Spearman |

---

# 🧠 Memory Tricks

## Mann-Whitney U

```
Different People

↓

Independent

↓

Not Normal

↓

Mann-Whitney
```

---

## Wilcoxon Signed-Rank

```
Same Person

↓

Symmetric Differences

↓

Wilcoxon
```

---

## Sign Test

```
Only +

or -

↓

Sign Test
```

---

## Kruskal-Wallis

```
3+

Independent

↓

Kruskal-Wallis
```

---

## Friedman

```
3+

Same Subjects

↓

Friedman
```

---

## Spearman

```
Ordinal

or

Not Normal

↓

Spearman
```

---

# 📌 Wilcoxon vs Sign Test

| Wilcoxon Signed-Rank | Sign Test |
|-----------------------|-----------|
| Uses signs (+/-) | Uses signs (+/-) |
| Uses ranks | Does NOT use ranks |
| Uses magnitude | Ignores magnitude |
| Requires symmetric differences | No symmetry assumption |
| Higher statistical power | Lower statistical power |

---

# ⭐  Checklist

Before choosing a **non-parametric test**, ask yourself:

1. 📊 Is the data non-normal or ordinal?
2. 👥 Are the groups independent or paired?
3. 🔢 Are there two groups or more than two groups?
4. 📈 If paired, are the differences symmetric?
5. 🔗 Am I comparing groups or measuring a relationship?

---

# 🎯 Ultimate Memory Flow

```text
Not Normal?

↓

Two Groups?

│

├── Independent
│      ↓
│ Mann-Whitney U
│
└── Paired
       │
       ├── Symmetric
       │      ↓
       │ Wilcoxon Signed-Rank
       │
       └── Not Symmetric
              ↓
           Sign Test

↓

Three or More Groups?

│

├── Independent
│      ↓
│ Kruskal-Wallis
│
└── Same Subjects
       ↓
    Friedman

↓

Relationship?

↓

Ordinal or Non-normal

↓

Spearman Correlation
```

---

# 🎓 Favourite Traps

⚠️ **Trap 1**

Two groups + Non-normal

✅ Mann-Whitney

NOT Independent t-test

---

⚠️ **Trap 2**

Paired + Non-normal

✅ Wilcoxon

NOT Mann-Whitney

---

⚠️ **Trap 3**

Paired + Differences NOT symmetric

✅ Sign Test

NOT Wilcoxon

---

⚠️ **Trap 4**

Three groups + Non-normal

✅ Kruskal-Wallis

NOT One-Way ANOVA

---

⚠️ **Trap 5**

Repeated measurements + Non-normal

✅ Friedman

NOT Repeated Measures ANOVA

---

## 🎯 Golden Rule

> **Parametric tests compare means using raw values.**
>
> **Non-parametric tests compare ranks when parametric assumptions are violated.**
