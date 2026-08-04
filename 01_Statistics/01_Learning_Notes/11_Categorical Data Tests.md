# 📗 Statistics Handbook
# Chapter 3: Categorical Data Tests

---

# 📖 What are Categorical Data Tests?

Categorical data tests analyze **counts (frequencies)** rather than numerical measurements.

Instead of comparing **means**, these tests compare:

- 📊 Frequencies
- 📈 Proportions
- 📦 Categories

Examples:

- Male / Female
- Smoker / Non-smoker
- Disease / No Disease
- Blood Group
- Vaccine Yes / No

---

# 📚 Categorical Tests Covered

| Test | Purpose |
|------|---------|
| Chi-Square Test of Independence | Association between two categorical variables |
| Chi-Square Goodness-of-Fit Test | Compare observed frequencies with expected frequencies |
| Fisher's Exact Test | Small sample alternative to Chi-square |
| McNemar's Test | Paired categorical data |
| Two-Proportion Z-Test | Compare two population proportions |

---

# 🌳 Decision Tree

```text
Categorical Data
│
├── One Variable?
│      │
│      └── Compare with expected frequencies
│              ↓
│      Chi-Square Goodness-of-Fit
│
├── Two Variables?
│      │
│      ├── Independent?
│      │       │
│      │       ├── Large Sample
│      │       │       ↓
│      │       │  Chi-Square Independence
│      │       │
│      │       └── Small Expected Counts
│      │               ↓
│      │         Fisher's Exact Test
│      │
│      └── Same Subjects?
│              ↓
│         McNemar's Test
│
└── Compare Two Proportions?
        ↓
   Two-Proportion Z-Test
```

---

# 📊 Quick Comparison

| Situation | Test |
|------------|------|
| One categorical variable | Chi-Square Goodness-of-Fit |
| Two categorical variables | Chi-Square Independence |
| Small expected counts | Fisher's Exact Test |
| Paired categorical data | McNemar's Test |
| Compare two proportions | Two-Proportion Z-Test |

---

# 📝 Question 31

## ❓ Scenario

Researchers investigate whether **smoking status** is associated with **lung cancer**.

### ✅ Answer

**Chi-Square Test of Independence**

### 💡 Why?

- Two categorical variables
- Independent observations
- Looking for an association

### Example Table

| | Cancer | No Cancer |
|---|---:|---:|
| Smoker | 35 | 15 |
| Non-Smoker | 10 | 40 |

### ❌ Why NOT?

**Goodness-of-Fit**

Only one categorical variable.

### 🧠 Memory Trick

```
Two Variables

↓

Association

↓

Chi-Square Independence
```

---

# 📝 Question 32

## ❓ Scenario

A coin is tossed **100 times**.

Researchers want to know whether the coin is fair.

Expected:

- Heads = 50
- Tails = 50

### ✅ Answer

**Chi-Square Goodness-of-Fit Test**

### 💡 Why?

One categorical variable.

Observed frequencies are compared with expected frequencies.

### ❌ Why NOT?

Chi-Square Independence

Requires two variables.

### 🧠 Memory Trick

```
Observed

vs

Expected

↓

Goodness-of-Fit
```

---

# 📝 Question 33

## ❓ Scenario

Researchers compare the proportion of vaccinated individuals between **two cities**.

Sample size = 5,000.

### ✅ Answer

**Two-Proportion Z-Test**

### 💡 Why?

Comparing two independent proportions.

Large sample size.

### Example

| City | Vaccinated |
|------|-----------:|
| A | 80% |
| B | 74% |

### 🧠 Memory Trick

```
Two Percentages

↓

Z-Test
```

---

# 📝 Question 34

## ❓ Scenario

Researchers evaluate a diagnostic test **before and after calibration** using the **same patients**.

### ✅ Answer

**McNemar's Test**

### 💡 Why?

- Same participants
- Before vs After
- Categorical outcome

### Example

Positive / Negative

Before

↓

After

### ❌ Why NOT?

Chi-Square Independence

Requires independent observations.

### 🧠 Memory Trick

```
Same Patients

+

Before/After

↓

McNemar
```

---

# 📝 Question 35

## ❓ Scenario

Researchers compare blood group frequencies

(A, B, AB, O)

with national expected frequencies.

### ✅ Answer

**Chi-Square Goodness-of-Fit**

### 💡 Why?

One categorical variable.

Observed frequencies compared with expected frequencies.

---

# 📝 Question 36

## ❓ Scenario

Researchers have a 2×2 contingency table.

Several expected counts are **less than 5**.

### ✅ Answer

**Fisher's Exact Test**

### 💡 Why?

Chi-square assumptions are violated.

Expected frequencies are too small.

### ❌ Why NOT?

Chi-Square

Needs expected frequency ≥5.

### 🧠 Memory Trick

```
Expected Count

<5

↓

Fisher Exact
```

---

# 📝 Question 37

## ❓ Scenario

Researchers compare smoking rates between males and females.

Sample size = 3,000.

### ✅ Answer

**Two-Proportion Z-Test**

### 💡 Why?

Comparing two independent population proportions.

Large sample.

---

# 📝 Question 38

## ❓ Scenario

Researchers investigate whether

Gender

is associated with

Disease Status.

### ✅ Answer

**Chi-Square Test of Independence**

---

# 📝 Question 39

## ❓ Scenario

Researchers compare COVID test results

before vaccination

and

after vaccination

using the same people.

### ✅ Answer

**McNemar's Test**

---

# 📝 Question 40

## ❓ Scenario

Researchers compare observed genotype frequencies with expected Mendelian ratios.

### ✅ Answer

**Chi-Square Goodness-of-Fit Test**

---

# 📊 Chi-Square Independence vs Goodness-of-Fit

| Feature | Independence | Goodness-of-Fit |
|----------|-------------|-----------------|
| Variables | Two | One |
| Purpose | Association | Observed vs Expected |
| Example | Smoking vs Cancer | Fair Coin |
| Output | Association? | Fits expected distribution? |

---

# 📊 Chi-Square vs Fisher's Exact

| Chi-Square | Fisher's Exact |
|------------|----------------|
| Large samples | Small samples |
| Expected count ≥5 | Expected count <5 |
| Approximation | Exact probability |

---

# 📊 McNemar vs Chi-Square

| McNemar | Chi-Square |
|----------|-----------|
| Same subjects | Different subjects |
| Paired | Independent |
| Before vs After | Association |

---

# 📊 Two-Proportion Z-Test

## Purpose

Compare **two independent population proportions**.

### Example

| Group | Success Rate |
|--------|-------------:|
| Male | 15% |
| Female | 20% |

### Assumptions

- Independent samples
- Large sample size

- np ≥ 5
- n(1-p) ≥ 5

---

# 📊 Fisher's Exact Test

## Purpose

Alternative to Chi-Square for **small samples**.

### Example

| | Disease | Healthy |
|---|---:|---:|
| Drug | 2 | 3 |
| Placebo | 1 | 4 |

Expected frequencies are very small.

↓

Use Fisher's Exact Test.

---

# 🧠 Memory Tricks

## Chi-Square Independence

```
Two Variables

↓

Association
```

---

## Goodness-of-Fit

```
Observed

vs

Expected
```

---

## Fisher's Exact

```
Small Sample

↓

Fisher
```

---

## McNemar

```
Before

↓

After

Same Person
```

---

## Two-Proportion Z-Test

```
Two Percentages

↓

Z-Test
```

---

# ⭐ Favourite Traps

## ⚠️ Trap 1

Smoking

↓

Cancer

↓

**Two variables**

✅ Chi-Square Independence

NOT Goodness-of-Fit

---

## ⚠️ Trap 2

Fair Coin

↓

Expected 50 Heads

↓

One variable

✅ Goodness-of-Fit

---

## ⚠️ Trap 3

Expected frequencies <5

↓

Fisher's Exact

NOT Chi-Square

---

## ⚠️ Trap 4

Same patients

↓

Before

↓

After

↓

McNemar

---

## ⚠️ Trap 5

Compare percentages

↓

Male 15%

Female 20%

↓

Two-Proportion Z-Test

---

# 📋 Summary Table

| Situation | Test |
|-----------|------|
| One categorical variable | Chi-Square Goodness-of-Fit |
| Two categorical variables | Chi-Square Independence |
| Expected counts <5 | Fisher's Exact Test |
| Same people (Before/After) | McNemar's Test |
| Compare two proportions | Two-Proportion Z-Test |

---

# 🎯 Ultimate Memory Flow

```text
Categorical Data?

↓

One Variable?

↓

Observed vs Expected

↓

Chi-Square Goodness-of-Fit

────────────────────

Two Variables?

↓

Independent?

↓

Expected Count ≥5 ?

↓

YES → Chi-Square Independence

NO → Fisher's Exact

────────────────────

Same Subjects?

↓

McNemar

────────────────────

Comparing Two Percentages?

↓

Two-Proportion Z-Test
```

---

# ⭐ Checklist

Before choosing a **categorical test**, ask yourself:

1. 📊 Is the outcome categorical?
2. 🔢 Is there **one variable** or **two variables**?
3. 👥 Are the observations independent or paired?
4. 📉 Are the expected cell counts ≥5?
5. 📈 Are you comparing **counts**, **associations**, or **proportions**?

---

# 🎯 Golden Rule

> **Chi-Square tests compare frequencies (counts), not means.**

- 📊 **Independence** → Two categorical variables
- 🎯 **Goodness-of-Fit** → One categorical variable (Observed vs Expected)
- 🐟 **Fisher's Exact** → Small sample sizes
- 🔄 **McNemar** → Paired categorical data
- 📈 **Two-Proportion Z-Test** → Compare two independent proportions
