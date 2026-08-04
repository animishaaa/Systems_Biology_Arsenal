# 📘 Statistics Handbook
# Chapter 1: Parametric Tests

---

# 📖 What are Parametric Tests?

Parametric tests are statistical tests that make assumptions about the population.

## ✅ Assumptions

- 📈 Continuous (Interval/Ratio) data
- 🔔 Data is approximately **normally distributed**
- 👥 Observations are independent (unless using paired tests)
- 📊 Equal variances (for some tests)

---

# 📚 Parametric Tests Covered

| Test | Purpose |
|------|---------|
| One-Sample t-test | Compare one sample mean with a known value |
| Independent Two-Sample t-test | Compare two independent groups |
| Paired t-test | Compare two related groups |
| One-Way ANOVA | Compare 3 or more independent groups |
| Repeated Measures ANOVA | Compare 3 or more related measurements |
| Pearson Correlation | Measure relationship between two continuous variables |
| Linear Regression | Predict one variable using another |
| Post-hoc Tests | Identify which groups differ after ANOVA |

---

# 🌳 Decision Tree

```text
Continuous Data?
│
├── One Group?
│      └── One-Sample t-test
│
├── Two Groups?
│      │
│      ├── Independent?
│      │      └── Independent Two-Sample t-test
│      │
│      └── Paired?
│             └── Paired t-test
│
└── More Than Two Groups?
       │
       ├── Independent?
       │      └── One-Way ANOVA
       │
       └── Same Subjects?
              └── Repeated Measures ANOVA
```

---

# 📝 Question 1

## ❓ Scenario

Researchers compare the average cholesterol level between **40 smokers** and **40 non-smokers**.

The cholesterol values are normally distributed.

### ✅ Answer

**Independent Two-Sample t-test**

### 💡 Why?

- Continuous variable ✅
- Two groups ✅
- Independent participants ✅
- Normal distribution ✅

### ❌ Why NOT?

**Paired t-test**

- Same people measured twice.
- Not true.

**One-Way ANOVA**

- Used for three or more groups.

**Mann-Whitney U**

- Only when data is not normally distributed.

### 🧠 Memory Trick

```
Different People
        ↓
Independent
        ↓
Independent t-test
```

---

# 📝 Question 2

## ❓ Scenario

Twenty patients have their blood pressure measured **before** and **after** taking a new drug.

The differences are normally distributed.

### ✅ Answer

**Paired t-test**

### 💡 Why?

- Same patients
- Before vs After
- Measurements are related

### ❌ Why NOT?

**Independent t-test**

Needs different participants.

**One-Way ANOVA**

Only two measurements.

**Wilcoxon Signed-Rank Test**

Used when differences are not normally distributed.

### 🧠 Memory Trick

```
Same Person
     ↓
Before vs After
     ↓
Paired t-test
```

---

# 📝 Question 3

## ❓ Scenario

The WHO states that the average vitamin D level is **50 nmol/L**.

A researcher measures vitamin D in **25 people** and wants to know whether their average differs from 50.

Data is normally distributed.

### ✅ Answer

**One-Sample t-test**

### 💡 Why?

- One sample
- Compare against one known value

### ❌ Why NOT?

**Independent t-test**

Requires two groups.

**ANOVA**

Requires three or more groups.

### 🧠 Memory Trick

```
One Group
     ↓
Known Value
     ↓
One-Sample t-test
```

---

# 📝 Question 4

## ❓ Scenario

Researchers compare weight loss among patients following:

- Mediterranean diet
- Keto diet
- Vegan diet
- Low-fat diet

All groups are independent.

Data is normal.

### ✅ Answer

**One-Way ANOVA**

### 💡 Why?

- More than two independent groups

### ❌ Why NOT?

Multiple t-tests increase the Type I error rate.

### 🧠 Memory Trick

```
3+ Independent Groups
          ↓
     One-Way ANOVA
```

---

# 📝 Question 5

## ❓ Scenario

Researchers weigh the same mice:

- Week 1
- Week 2
- Week 3
- Week 4

Data is normally distributed.

### ✅ Answer

**Repeated Measures ANOVA**

### 💡 Why?

- Same subjects
- Measured more than twice

### ❌ Why NOT?

One-Way ANOVA requires different subjects.

### 🧠 Memory Trick

```
Same Subjects
Measured Many Times
        ↓
Repeated Measures ANOVA
```

---

# 📝 Question 6

## ❓ Scenario

A scientist wants to know whether **height is related to weight**.

Both variables are continuous and normally distributed.

### ✅ Answer

**Pearson Correlation**

### 💡 Why?

Measures the strength and direction of a relationship.

### ❌ Why NOT?

Regression predicts one variable from another.

Correlation only measures association.

### 🧠 Memory Trick

```
Relationship Only
       ↓
Pearson Correlation
```

---

# 📝 Question 7

## ❓ Scenario

A doctor wants to predict **body weight from height**.

### ✅ Answer

**Simple Linear Regression**

### 💡 Why?

Regression is used for prediction.

- Independent variable (X): Height
- Dependent variable (Y): Weight

### 🧠 Memory Trick

```
Want Prediction?
       ↓
Regression
```

---

# 📝 Question 8

## ❓ Scenario

A One-Way ANOVA comparing four cancer treatments gives:

**p = 0.003**

The researcher now wants to know **which treatments differ**.

### ✅ Answer

**Post-hoc Test**

Examples:

- Tukey
- Bonferroni
- Fisher's LSD

### 💡 Why?

ANOVA only tells us that a difference exists.

Post-hoc tests identify **where** the difference is.

### 🧠 Memory Trick

```
ANOVA Significant?
        ↓
Post-hoc Test
```

---

# 📝 Question 9

## ❓ Scenario

A researcher compares five exercise programs.

Participants are independent.

Data is normally distributed.

### ✅ Answer

**One-Way ANOVA**

### 💡 Why?

More than two independent groups.

---

# 📝 Question 10

## ❓ Scenario

After ANOVA, the researcher wants a **conservative correction** for multiple comparisons.

### ✅ Answer

**Bonferroni Post-hoc Test**

### 💡 Why?

Bonferroni strongly controls Type I error.

---

# 📝 Question 11

## ❓ Scenario

Compare blood glucose levels between healthy people and diabetic patients.

Groups are independent.

Data is normal.

### ✅ Answer

**Independent Two-Sample t-test**

---

# 📝 Question 12

## ❓ Scenario

Researchers compare IQ between boys and girls.

Data is normally distributed.

### ✅ Answer

**Independent Two-Sample t-test**

---

# 📝 Question 13

## ❓ Scenario

Researchers measure cholesterol before and after six months of exercise.

Same people.

Data is normal.

### ✅ Answer

**Paired t-test**

---

# 📝 Question 14

## ❓ Scenario

Researchers compare blood pressure among:

- Drug A
- Drug B
- Drug C
- Placebo

Different participants.

### ✅ Answer

**One-Way ANOVA**

---

# 📝 Question 15

## ❓ Scenario

Researchers want to predict blood pressure from age.

### ✅ Answer

**Linear Regression**

---

# 📊 Summary Table

| Situation | Test |
|-----------|------|
| One group vs known value | ✅ One-Sample t-test |
| Two independent groups | ✅ Independent Two-Sample t-test |
| Two related groups | ✅ Paired t-test |
| Three or more independent groups | ✅ One-Way ANOVA |
| Three or more repeated measurements | ✅ Repeated Measures ANOVA |
| Relationship only | ✅ Pearson Correlation |
| Prediction | ✅ Linear Regression |
| ANOVA significant | ✅ Post-hoc Test |

---

# 🧠 Ultimate Memory Flow

```text
Continuous Data?
│
├── One Group
│      ↓
│   One-Sample t-test
│
├── Two Groups
│      │
│      ├── Different People
│      │      ↓
│      │ Independent t-test
│      │
│      └── Same People
│             ↓
│        Paired t-test
│
└── Three or More Groups
       │
       ├── Different People
       │      ↓
       │ One-Way ANOVA
       │
       └── Same People
              ↓
       Repeated Measures ANOVA

Relationship?
      ↓
Pearson Correlation

Prediction?
      ↓
Linear Regression

ANOVA Significant?
      ↓
Post-hoc Test
```

---

# ⭐  Checklist

Before choosing a **parametric test**, ask yourself:

1. 📊 Is the data continuous?
2. 🔔 Is it approximately normally distributed?
3. 👥 How many groups are there?
4. 🔗 Are the groups independent or paired?
5. 🎯 Am I comparing groups, measuring a relationship, or making a prediction?

If you answer these five questions correctly, you'll almost always choose the correct parametric test.
