# 📊 Statistical Distributions 

## 🤔 What is a Distribution?

A **distribution** describes **how data or probabilities are spread across possible values**.

It answers questions like:

- 📍 Where are most values?
- 📏 How spread out are they?
- 📈 Are extreme values common?
- 📉 What shape does the data have?

💡 Think of a distribution as the **fingerprint of a dataset**.

---
---

# Types of Distributions

There are two broad categories:

```
Distributions
│
├── Frequency Distribution
│
└── Probability Distributions
      │
      ├── Normal
      ├── Z
      ├── t
      ├── Binomial
      ├── Poisson
      ├── Chi-Square
      └── F
```

---

# 🗂️ Two Types of Distributions

## 1️⃣ 📋 Frequency Distribution

### 📖 Definition

A **frequency distribution** simply counts **how many times each value occurred** in your data.

It describes **observed data**.

### 📝 Example

Observed exam scores:

| Score | Frequency |
|------:|----------:|
| 60 | 2 |
| 70 | 5 |
| 80 | 8 |
| 90 | 5 |

### ❓ Question Answered

> **"What did I observe?"**

---

## 2️⃣ 🎲 Probability Distribution

### 📖 Definition

A **probability distribution** gives the **probability of each possible outcome** before observing the data.

It describes **what is likely to happen**.

### 🎲 Example

Rolling a fair die:

| Outcome | Probability |
|---------:|------------:|
| 1 | 1/6 |
| 2 | 1/6 |
| 3 | 1/6 |
| 4 | 1/6 |
| 5 | 1/6 |
| 6 | 1/6 |

### ❓ Question Answered

> **"What is likely to happen?"**

---

# 📚 Common Probability Distributions

## 🔔 1. Normal Distribution

### 🎯 Purpose

Used for **continuous measurements** where most observations cluster around the average.

### 📈 Shape

```
        *
      *   *
    *       *
  *           *
 *             *
--------------------
```

### 🌍 Common Examples

- 📏 Height
- ⚖️ Weight
- ❤️ Blood pressure
- 🧠 IQ
- 📝 Exam scores

### 🧪 Used In

- Z-test
- t-test (large samples)
- Regression
- Many statistical methods

---

## 📍 2. Standard Normal (Z) Distribution

### 🎯 Purpose

The normal distribution after **standardization**.

Instead of measuring actual values, it measures

> **How many standard deviations a value is from the mean.**

### 🧮 Formula

```
Z = (Value − Mean) / Standard Deviation
```

### 📝 Example

Average exam score = **70**

Student score = **80**

Standard deviation = **5**

```
Z = (80 − 70) / 5 = 2
```

Meaning:

📈 The student scored **2 standard deviations above average.**

### 🧪 Used In

- Z-tests
- Probability calculations
- Confidence intervals

---

## 📐 3. t Distribution

### 🎯 Purpose

Used when

- 👥 Sample size is small
- ❓ Population standard deviation is unknown

It looks similar to the normal distribution but has **heavier tails**, reflecting greater uncertainty.

### 🧪 Used In

- One-sample t-test
- Independent t-test
- Paired t-test

---

## 🪙 4. Binomial Distribution

### 🎯 Purpose

Used when there are only **two possible outcomes**.

### 🌍 Examples

- ✅ Yes / ❌ No
- ✔️ Pass / ❌ Fail
- 🎯 Success / Failure
- 🪙 Heads / Tails

### 📝 Example

Flip a coin **10 times**.

Question:

> **What is the probability of getting exactly 7 heads?**

### 🧪 Used In

- Binary experiments
- Success/failure probabilities

---

## 📬 5. Poisson Distribution

### 🎯 Purpose

Used for **counting how many events occur** during a fixed time or space.

### 🌍 Examples

- 📧 Emails per hour
- 🛒 Customers entering a store
- ☎️ Calls received per minute
- 🚗 Accidents per day
- 🧬 DNA mutations

### ❓ Question Answered

> **"How many events are likely to occur?"**

### 🧪 Used In

- Count data
- Rare event analysis

---

## 🧩 6. Chi-square Distribution

### 🎯 Purpose

Used for **categorical data (counts)**.

Measures **how different the observed counts are from the expected counts.**

### 📝 Example

Expected:

| Color | Expected |
|------|---------:|
| 🔴 Red | 25 |
| 🔵 Blue | 25 |
| 🟢 Green | 25 |
| 🟡 Yellow | 25 |

Observed:

| Color | Observed |
|------|---------:|
| 🔴 Red | 18 |
| 🔵 Blue | 32 |
| 🟢 Green | 20 |
| 🟡 Yellow | 30 |

### ❓ Question

> **Are these differences larger than expected by chance?**

### 🧪 Used In

- Chi-square goodness-of-fit test
- Chi-square test of independence
- Tests involving categorical variables

---

## ⚖️ 7. F Distribution

### 🎯 Purpose

Used to compare **variation**.

Specifically,

```
Between-group variation
-----------------------
Within-group variation
```

### 📝 Example

Average exam scores

```
📚 Class A = 72

📚 Class B = 74

📚 Class C = 90
```

Question

> **Are the class averages really different?**

The F distribution compares

- 📊 Variation inside each class
- 📈 Variation between classes

### 🧪 Used In

- ANOVA
- Regression
- Comparing variances

---

# 📝 Summary Table

| 📊 Distribution | 🎯 Used For | 📂 Data Type | ❓ Main Question |
|----------------|------------|-------------|----------------|
| 📋 Frequency | Count observations | Any | What did I observe? |
| 🎲 Probability | Probability of outcomes | Any | What is likely to happen? |
| 🔔 Normal | Continuous measurements | Continuous | How are values distributed around the mean? |
| 📍 Z | Standardized values | Continuous | How far from the mean is a value? |
| 📐 t | Small samples | Continuous | Is the sample mean significantly different? |
| 🪙 Binomial | Two possible outcomes | Discrete | How likely are a certain number of successes? |
| 📬 Poisson | Counting events | Discrete | How many events are likely to occur? |
| 🧩 Chi-square | Categorical counts | Categorical | Are observed counts different from expected? |
| ⚖️ F | Comparing variances | Continuous | Are differences between groups larger than normal variation? |

---

# 🚦 Which Distribution Should I Use?

| 📌 If your data is... | 📊 Use... |
|----------------------|----------|
| Raw observations | 📋 Frequency Distribution |
| Probabilities | 🎲 Probability Distribution |
| Heights, weights, exam scores | 🔔 Normal Distribution |
| Standardized scores | 📍 Z Distribution |
| Small sample means | 📐 t Distribution |
| Yes/No outcomes | 🪙 Binomial Distribution |
| Event counts | 📬 Poisson Distribution |
| Category counts | 🧩 Chi-square Distribution |
| Comparing multiple group means | ⚖️ F Distribution (ANOVA) |

---

#  📊 Distribution + Statistical Tests

| Distribution | Used For | Main Statistical Tests |
|-------------|----------|------------------------|
| Frequency | Counting observations | Data summarization |
| Probability | Probability of outcomes | Foundation of all hypothesis tests |
| Normal | Continuous measurements | Basis for parametric tests |
| Z | Standardized values | Z-test |
| t | Small samples, unknown SD | t-tests, regression coefficients, Pearson correlation |
| Binomial | Yes/No outcomes | Binomial test |
| Poisson | Count data | Poisson regression |
| Chi-Square | Categorical data | Chi-square, McNemar, Kruskal-Wallis, Friedman |
| F | Comparing variances | ANOVA, overall regression |

---

# 🧠 One Sentence to Remember

> **📌 A frequency distribution describes what happened, while probability distributions model what could happen. Statistical tests choose the probability distribution that best matches the type of data and the question being asked.**
